# API接口

## 机制
* secret：用于双方后端间通讯，token初始化时使用。
* token：用于前端，有有效期
* 业务都是由前端发起，安全方案如下：
  1. 前端发起，域名绑定
    * 微信公众号授权的输入参数是appid和返回URL(非配置域名url会提示无效输入)。返回参数是token。后续通讯都通过token
  1. 客户端原生加密
    * QQ授权：id和secret持久化在客户端。有泄密风险
  1. 前端发起，后端加密
    * 微信JSSDK：jsconfig由后端签名生成，secret和随机数时间戳等

## 安全级别

| 级别 | 机制 | 接口实例 | 说明 |
| :----: | ---- | ---- | ---- |
| 无 | 无 | 获取商品明细 |  |
| 普通 | 白名单，设置域名或者IP | 获取商品明细 | 黑客可以模拟攻击 |
| 高级 | 商户：商户授权 | 商户账单获取 |  |
| 高级 | 用户：商户授权+用户令牌 | 订单获取 |  |  |

### 商户授权
1. 存储位置
  1. 后端（客户端被攻击成功也是临时的，提供前端暂时使用的令牌）
  1. 前端（客户端被攻击成功就是永久获取）
1. 安全级别
  1. 普通(key，可以存储在前端，如百度地图)
  1. 高级(key+secret，只能存储在后端，如淘宝)

## 渠道的安全机制

| 渠道 | 机制 | 说明 |
| :----: | ---- | ---- |
| 自有网站 | 普通安全级别 |  |
| 第三方后端直连 | 高级安全级别，后端存储 |  |
| 原生APP | 高级安全级别，前端存储 | 大部分app采用的方案，前端要确保秘钥安全 |
| 混合型APP TODO | 高级安全级别，前端存储不安全啊？？？ | 调用原生函数实现签名？ |

# 文件签名
## 3种方案
1. 路径签名，如图片网址
1. 特征取样签名，按照文件尺寸等间隔取16个点，合并点值，签名。[参考](https://github.com/MashiMaroLjc/Learn-to-identify-similar-images/blob/master/Chinese.md)
1. 全部内容签名，[参考](http://blog.csdn.net/wayfoon322/article/details/2394991)

## 签名URI
* 格式：类型/签名。
* 类型有p(路径), t(特征), a(内容)
* 如：p/guid，a/guid。

# 用户账号安全
## token盗用
### 概要
* 情况：无法判断真实用户和黑客谁是假冒的
* 常用登录方案

| 风险级别 | 方案 | 实例 | 说明 |
| :----: | ---- | ---- |
| 高 | 单点登录 | 支付宝 |  |
| 中 | 多点登录 | 淘宝 |  |

* 设计思路
  1. 在被盗用的情况下通过请求制造冲突，失效token
  1. 登录安全和资金安全是不同等级的需求：登录为了便利可以牺牲一定的安全，终端缓存。而资金必须是每次验证，终端不缓存
* 建议只在正式环境生效。测试等环境可不启用本安全机制，便于测试

1. 方案和风险
  * 共同潜在风险：真实用户后续如没操作请求，则黑客就成了真实用户

| 方案 | 复杂度 | 说明 |
| :----: | ---- | ---- |
| 请求序列 | 简单 | 推荐 |
| 周期时间 | 复杂 |  |

### 方案 - 请求序列
* 设计
  1. key：账号+终端+token(每次登录都会改变)+请求序列(每次请求都会改变)
  1. 请求序列超过了允许范围，就说明有多个终端在使用同一个token。则无效token
  1. 即使黑客知道更新请求序列的逻辑，但因真实用户的操作的不可控性，其请求序列超过了允许范围的概率很大。所以基本没有风险
  1. 终端是可以伪造的，暂不生效
* 多点登录流程

```java
function(token, seq) {
  data = getDataByToken(token); // token内容

  span = Math.abs(seq - data.seq); // 终端请求序列和服务端请求序列的距离
  if (span > 30) { // 允许范围(就是并发请求时间范围)
    失效 token;
    return 异常码;
  } else {
    new_seq = increaseTokenSeq(token);  // 独立缓存
    return new_seq; // 终端收到后更新seq
  }
}
```

### 方案 - 周期时间
* 设计
  1. 一个账号每登录一次就有一个token链，一个账号在单点登录情况下存在一个token链，一个账号在多点登录情况下存在多个token链
  1. token在客户端是时间周期有效的(服务端时间为准)，比如1小时。时间周期到了后，当有请求发起时，后端重新生成新token并返回终端
  1. 当有老token来请求时，如超过新token生成时间3分钟(确保在token更新期间，真实用户发起的老token请求也能顺利过渡，而不会冲突)，则整个token链都失效
* 说明
  * token链：新token生成后，放在老token的后面，组成了一个链表
* 多点登录流程

```java
function(token) {
  data = getDataByToken(token); // token内容

  if (token is new) {
    if (current_time - data.createtime > 1H) {
      lock("user_token_link", data.user, data.list) {
        if (token is new) {
          生成新token;
          return 新token; // 终端收到后更新token
        } else { // 锁的时候有新token生成了
          return; // 正常返回
        }
      }
    } else {
      return; // 正常返回
    }
  } else {
    new_token = getNewToken(data.list);
    new_data = getDataByToken(new_token);
    if (current_time - new_data.createtime > 3M) {
      失效 data.list
      return 异常码;
    } else {
      return; // 正常返回
    }
  }
}
```
