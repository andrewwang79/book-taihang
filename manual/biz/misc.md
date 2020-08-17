# 平台服务的设计
* 平台上每个服务都是个app。
* app表结构：开发商(vendor)，用户信息要求(userInfo)，动态网址(isUrlDynamic)，是否匿名，是否启用(isOn)。
* 开发商：开发商是平台的不用加iframe（平台开发的自带标准布局），其他都加iframe
* 用户信息要求：json格式。信息如mobile，idcard，address等。
* 每个app在使用前都会检查用户状态和信息要求。不符合则要完善。

# 二维码扫描
> 扫描结果是网址（为了支持微信扫描，必须是网址），方案有2个，推荐使用方案1。

## 方案1：
静态，如http://www.xyz.com/item/123456，http://www.xyz.com/event/123456
处理方式：
1. 微信处理：直接跳转
1. app处理：绝对匹配“http://www.xyz.com/”，前端处理参数，跳转到指定路由。

## 方案2：
动态，如http://www.xyz.com/scan?type=item&id=123456
处理方式：
1. 微信处理：前端处理参数
1. app处理：绝对匹配“http://www.xyz.com/scan”，前端处理参数。
http://www.xyz.com/scan?type=item&id=123456转换成
http://www.xyz.com/item/123456
http://www.xyz.com/event/123456

# 短链接地址
短地址(ShortUrl)是[KV持久化](../sys/misc.html/#KV持久化)的一种应用场景。

## 转换
可使用t.cn之类的服务
## 短信注意事项
因第三方短信服务商要检查链接的域名许可。所以只能使用自己的域名。

## 方案
* 地址路径：域名/t/短地址编码
* 短地址编码：6位的字母数字

配置项：http://www.xyz.com/t/{0}

## 流程
1. 生成短地址编码，和网址一起insert到表KV

# 分组和标签
分组用于商品等，标签用于订单、活动等。TODO
