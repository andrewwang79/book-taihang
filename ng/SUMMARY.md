# 基于微服务的架构

## 目标
1. 适用于中大型产品开发
1. 支持私有化部署和云部署
1. 可不停机加入/降级服务功能
1. 系统可治理：配置，日志，报警等

## 技术
1. 现代化
1. 微服务
1. 大数据
1. UT测试

## 软件架构
![](https://tech.wangyaqi.cn/s/distarch/arch.jpg)

## 模块结构

| 层 | 模块 | 说明 |
| :-: | - | - |
| framework |  | 框架层 |
|  | lib-common | 通用库 |
|  | lib-service | 服务库，集成各种第三方服务 |
|  | lib-web | WEB库，主要是API |
|  | service-common | 中间件-通用服务 |
|  | service-oss | 中间件-OSS服务 |
|  | service-auth | 中间件-权限服务 |
|  | service-gateway | 服务治理-网关服务 |
| medical |  | 医疗行业层 |
|  | lib-common | 通用库 |
|  | service-broker | 中间件-收图服务 |
| demo |  | demo |
|  | service-gateway | framework的网关能通用吗？ |
|  | service-api | 服务 |

### service-common
* 组织机构、参数设置、字典管理、审计日志
### service-auth
* 角色用户、菜单及按钮授权、数据权限

### lib-service
* 分布式支持(锁，MQ，缓存)
* 多数据源连接，连接池
* 用户：第三方登录、单点登录
* 其他功能：内容管理、任务计划、消息和通知
* 接入：支付、微信、存储
* 技术：唯一号生成、长连接(websocket)、防攻击

### 服务治理
* SpringCloud是总线，连接起每个微服务
* Spring Cloud admin
* 服务的可视化管理，如redis

## 资料
* [架构设计](https://tech.wangyaqi.cn/#/distarch/SUMMARY)
* [表参考](https://gitee.com/shuzheng/zheng/raw/master/project-datamodel/zheng.png)
