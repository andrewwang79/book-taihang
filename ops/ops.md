# 产品运维

## 运维接口

| 接口 | 地址 | 说明 |
| -------- | ----- | ----- |
| 心跳状态   | /ops/heartbeat | 监控为主 |
| 软件信息   | /ops/version | 所有类库的编译版本和编译时间 |
| 服务状态 | /ops/service | 开发的服务状态，如短信通道，定时任务 |
| 函数运行时间 | /ops/time | 发现运行时间过长的函数，便于优化 |

## 日常运维工作
* 检查错误：后端错误，前端错误，app的crash
* 性能

## 产品安装目录结构
配置文件需设置profile。
```
etc/产品名
	src：源代码
	cmd：命令
	bin
		jar包，配置文件(“application.properties”)
	log：/var/log/产品名
		error和debug
```

## 类库的编译版本和编译时间TODO
* 在maven编译时将版本和时间记录下来
* 建议记录在类库信息，而不是包名
