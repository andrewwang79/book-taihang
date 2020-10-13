# 服务治理

# 参考资料
https://doocs.github.io/advanced-java
http://class.imooc.com/sale/javaarchitect

https://www.rainbond.com/docs/quick-start/rainbond_overview/

#分布式组件

* 负载均衡
* 缓存
* 搜索
* 消息队列
* 分布式锁
* 读写分离，分库分表
* 分布式全局id
* 接口幂等性
* 日志收集
* 分布式存储
* 分布式文件系统
* 拓缩容
* 网关
* 服务治理 注册/发现/续约/下线/自保 (注册中心)
* 通讯
* 限流
* 服务容错:熔断，降级
* 配置中心

#解决方案
## 负载均衡
* Nginx核心原理解析
反向代理/负载均衡/动静分离
* LVS+Keepalived+Nginx实现高可用集群

##  缓存
* Redis核心原理解析
持久化机制/主从架构模式/主从复制/无磁盘化复制/哨兵机制/集群/雪崩
* 缓存雪崩的解决方案
* 缓存穿透的解决方案

## 搜索
* ES架构与原理解析
* 集成ES集群故障  节点宕机 / 脑裂问题
* ES深度分页下带来的性能问题分析与解决
* 大数据量下该如何使用scoll滚动技术进行搜索

## 消息队列
* kafka核心原理解析
* kafka高可用
* kafka如何保证消息消费的幂等性(redis bitmap)
* kafka如何保证消息的可靠性传输(回调控制)
* kafka如何保证消息的顺序性

## 分布式锁
* 基于Redis的setnx实现分布式锁
* 基于Redisson实现分布式锁
* 基于ZooKeeper的瞬时节点实现分布式锁
* 基于ZK的Curator客户端实现分布式锁

## 读写分离，分库分表
* shardingsphere
* MyCAT

##  分布式全局id
* SnowFlake算法
* UUID

## 接口幂等性
* 接口的幂等性实际上就是接口可重复调用，在调用方多次调用的情况下，接口最终得到的结果是一致的
* insert操作 唯一索引/token机制(提交的数据包含随机token)
* delete操作通过唯一索引(删除之前，先查询是否存在)
* update操作通过乐观锁(version字段控制)
* select操作无需考虑

## 日志收集
* 应用输出json格式日志
* 日志收集器filebeat
* 日志缓冲kafka
* 日志转换器logstash(从kafka读数据，输出到es)
* 日志存储 es
* 日志展示 kibana

## 分布式存储
* ceph

## 分布式文件系统
* FastDFS

## 拓缩容
* Kubernetes


## 网关
* zuul (同步Servlet，多线程阻塞模型)
* spring gateway (基于netty异步io)
* spring gateway性能比zuul更好/支持长连接/长期维护

##  注册中心
* eureka
* zk
* alibaba/nacos
* 什么是服务治理https://www.jianshu.com/p/dd818114ab4b
* 注册/发现/续约/下线/自保


## 通讯
* feign(http)
* dubbo(rpc)

##  限流
* alibaba/Sentinel
* redis限流设计

## 服务容错:熔断，降级
* Hystrix
* Hystrix Dashboard

## 配置中心
* apollo
* 配置中心功能与设计参考apollo作者文章（https://nobodyiam.com/2018/07/29/configuration-center-makes-microservices-smart/）
* 配置即控制
### 配置需要治理
* 权限控制、审计日志
* 灰度发布、配置回滚
* 不同环境、集群管理

### 配置中心核心功能
* 功能发布开关
* A/B测试
* QA测试
* 运维开关
* 限流
* 黑白名单
* 动态日志级别
* 动态网关路由
* 动态路由修改

## 链路追踪
* 客户端采集工具 sleuth
 核心原理，以及sleuth是怎么做的(traceId,spanId)
* 分布式追踪系统 zipkin(可以接入kafka缓冲，es存储)

## 需要演示的内容
###第一部分
* 演示各个组件的核心原理。
* zuul的负载均衡，前置拦截过滤，spring gateway在此基础上增加的长连接功能
* eureka和zookeeper  通过注册中心的客户端工具，显示服务在注册中心注册的数据
* 远程调用 feign的远程调用和负载均衡，dubbo暂时不做了
* 熔断 hystrix 演示熔断效果，打开hystrix的dashboard
* 链路跟踪，先演示sleuth的原理，再整合zipkin
###第二部分
* 在elk系统里可以根据返回给客户端的traceId，直接在kibana里面检索到所有请求的日志
* 演示限流，熔断，降级

##要说的顺序
先说在分布式系统中，需要什么样的功能，在说spring cloud是怎么实现的，然后说说spring cloud这些组件的核心功能和核心原理(原理尽量说，因为不一定都能会)。每个核心组件做一个演示。最后再来一个总的演示。
https://github.com/ctripcorp/apollo-use-cases
网关，限流，配置中心的整合
Spring Boot Admin

# 延伸 todo
* 限流 熔断 降级怎么做(todo)
* 网关处限流解决方案
* 远程调用的熔断，降级解决方案
* 注册中心与CAP原理
* eureka和zookeeper的区别
* 如何设计一个rpc框架
* 分布式事务原理
* 分布式事务现有框架：http://seata.io/zh-cn/docs/overview/what-is-seata.html，https://www.codingapi.com/docs/txlcn-preface/
* 分库分表
