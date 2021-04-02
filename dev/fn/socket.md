# 长连接

## 实现
1. 在API层定义WebSocketConfig类，注册WebSocket业务类的mapping
1. 教程
  * [Spring Web Socket 客户端 服务端实现 握手时传递参数](http://lippeng.iteye.com/blog/2299509)
  * [spring-boot websocket 配置和实现](http://blog.csdn.net/clementad/article/details/64444606)
1. 服务端nginx设置
  * [验证Nginx的长连接(keepalive)配置](https://priesttomb.github.io/web%E6%9C%8D%E5%8A%A1%E5%99%A8/2018/11/01/%E9%AA%8C%E8%AF%81Nginx%E7%9A%84%E9%95%BF%E8%BF%9E%E6%8E%A5(keepalive)%E9%85%8D%E7%BD%AE/)
  * [nginx优化——包括https、keepalive等](https://lanjingling.github.io/2016/06/11/nginx-https-keepalived-youhua/)
  * https://skyao.gitbooks.io/learning-nginx/content/documentation/keep_alive.html

| 上下文 | 字段 | 默认值 | 说明 |
| :-: | - | - | - |
| http/upstream | keepalive_timeout | 75s | 长连接在nginx保持的最长时间（客户端未发起新请求的时长）。超过长连接关闭。一般由业务心跳保证，本值设置小点即可。 |
| http/upstream | keepalive_requests | 100 | 长连接在nginx处理的最大请求数。超过长连接关闭 |
| upstream | keepalive | 无 | 到upstream服务的**空闲**keepalive连接的最大数量[解决连接数波动]。不会限制一个worker进程到upstream服务器连接的总数量 |
| server | proxy_connect_timeout | 60s | nginx连接upstream服务的超时时间，单位秒。不能超过75秒 |
| server | proxy_read_timeout | 60s | nginx接收数据给upstream服务的超时时间，单位秒 |
| server | proxy_send_timeout | 60s | nginx发送数据给upstream服务的超时时间，单位秒 |

如使用了nginx，需配置读超时时间
```
# proxy_connect_timeout 60s;
proxy_read_timeout 86400s; // 一天
# proxy_send_timeout 60s;
```
1. [前端测试文件](/s/websocket_test.html)
