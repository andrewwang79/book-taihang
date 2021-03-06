# 基于微服务的架构
![](https://tech.wangyaqi.cn/s/distarch/arch.jpg)

# 目标
1. 适用于中大型产品开发
1. 支持私有化部署和云部署
1. 可不停机加入/降级服务功能
1. 系统可治理：配置，日志，报警等
1. 技术
  1. 现代化
  1. 微服务
  1. 大数据
  1. UT测试

# 思路
* 无依赖的通用服务做成一个基础微服务
* 有行业微服务

# 结构组成
* SpringCloud是总线，连接起每个微服务

## 基础设施
* Redis，Zookeeper...
* Spring Cloud

## 基础库
* 基础库
* Spring增强库：防攻击，分布式支持(锁，MQ，缓存)

## 组件
### 分布式组件

### 服务治理组件

### 业务服务组件
* 权限服务

### 行业服务组件
* 商城

## TBD
* 功能：组织机构、参数设置、字典管理
* 用户权限：角色用户、菜单及按钮授权、数据权限
* 用户：第三方登录、单点登录
* 其他功能：内容管理、任务计划、消息和通知
* 接入：支付、微信、存储
* 技术：唯一号生成、长连接(websocket)

* 操作日志
* excel处理：如何交换文件，如果大了很不好。还是做成jar
* 文件读写压力：预处理
* 多数据源连接，连接池

# 治理
* Spring Cloud admin
* 服务的可视化管理，如redis

## 资料
* [架构设计](https://tech.wangyaqi.cn/#/distarch/SUMMARY)
* [表参考](https://github.com/shuzheng/zheng/blob/master/project-datamodel/zheng.png)
