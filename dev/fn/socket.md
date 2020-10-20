# 长连接

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
