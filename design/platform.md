# 系统平台化
## 内容项
1. appid,appsecret
1. 跳转url
1. 资源授权

## 安全机制
双方提前约好秘钥，传输加密信息

## appsecret安全性
1. 定期换
1. 绑定IP

## 两方和三方
| 名称 | 实例 | 实现机制 |
| - |  |  |
| 两方 | OSS | appsecret加密跳转url，资源授权scope是系统预置的。 |
| 三方 | 腾讯开放平台 | OAuth |

# OAuth
## 介绍
### 角色
资源拥有者 (Resource Owner)
客户端 (Client)
资源服务器 (Resource Server)
授权服务器 (Authorization Server)

### 其他
* https://zhuanlan.zhihu.com/p/30720675
* https://insights.thoughtworks.cn/api-2/
* 授权长期有效：refresh_token
* access token用来客户端和资源服务器之间交互，refresh token用来客户端和授权服务器之间交互

## 流程
### 初始化
1. 平台定义[资源scopes](https://cloud.tencent.com/developer/ask/89231)，放到资源服务器
1. 应用创建时填写appsecret等，选择所需的资源scope

### 授权
1. 商户在启用应用时授权同意应用的资源scope，客户端会把【用户授权凭证和应用秘钥】提交给授权服务器产生access_token。授权服务器会有该access_token对应的资源scope

### 资源请求
1. 客户端请求资源服务器的资源(access_token+appsecret)
1. 资源服务器请求授权服务器的Introspection接口(access_token+资源)，授权服务器查看对应的资源scope，有则返回授权成功
