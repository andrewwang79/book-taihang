# 长连接

## 理解
* Socket和WebSocket，不是RPC模式(请求响应模式)。本质上用于通知和请求。
* 有两种场景：
  1. 无需返回结果的通知：请求
  1. 需返回结果的请求：请求，请求结果(异步返回)。
* 请求和请求结果必须要有唯一对应的key，可以异步处理。比如pos机的流水号。
* http模式(API)本质是一次短连接，也是异步返回请求结果，只是这个返回结果无需做key关联，因为当前连接只有一个请求。

## 实现
1. 在API层定义WebSocketConfig类，注册WebSocket业务类的mapping
1. 教程
  * [Spring Web Socket 客户端 服务端实现 握手时传递参数](http://lippeng.iteye.com/blog/2299509)
  * [spring-boot websocket 配置和实现](http://blog.csdn.net/clementad/article/details/64444606)
1. 服务端设置
如使用了nginx，需配置读超时时间
```
# proxy_connect_timeout 60s;
proxy_read_timeout 86400s; // 一天
# proxy_send_timeout 60s;
```
1. [前端测试文件](/s/websocket_test.html)

## 资料
* [看完让你彻底搞懂Websocket原理](http://blog.csdn.net/frank_good/article/details/50856585)
* [Netty-WebSocket长连接推送服务](http://blog.csdn.net/z69183787/article/details/52505249)
* [WebSocket与TCP、Http的关系](http://blog.csdn.net/linwei_1029/article/details/47836249)：发起连接是http，传输是tcp，所以要开TCP的80端口
