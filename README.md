# 编程框架-太行

## 框架
![](/s/framework.jpg)
* 服务：基础服务 + 公共服务
* 行业业务方案
* 周边技术：前端 + 运维 + 测试

## 解决
1. 提升开发效率
1. 提升产品质量
1. 提升问题定位和解决能力
1. 降低维护成本

## 准则
1. 渐进式架构设计，具有快速迭代能力。解决需求和痛点
1. 分布式架构，可扩展性，模块化组件
1. 全API开发模式
1. [管理系统的快速配置开发](https://qiya365.gitbooks.io/longgang/)，通过配置和自定义页面快速开发
1. 自动化运维，生产问题可提前/快速发现和解决
1. 服务容器化，如docker
1. 不做轮子(这世界轮子太多了)，做粘合剂整合轮子：整合方案 + 轮子使用的封装 + 小工具。
1. 提供行业业务方案

## 目标
1. 太行 = 可进化的系统架构 + 可控的技术 + 运维工具
1. 为中小型系统提供全方位J2EE企业级开发解决方案，可以应用在不同行业。参见[edas](https://www.aliyun.com/product/edas/)

# 设计

## 系统架构模式
| 模式 | 情况 | 说明 |
| :----: | ---- | ---- |
| 单机服务 | 已淘汰 |  |
| 分布式服务 | 当前采用方案 | 所有服务在一个进程，部署到多个容器 |
| [微服务](https://andrewwang79.gitbooks.io/javadev/cloud/SUMMARY.html#%E5%BE%AE%E6%9C%8D%E5%8A%A1) | 将来可无缝升级 | 每组服务独立进程，部署到多个容器 |

## 系统架构
![](/s/arch.jpg)

## 技术选型
### 开发语言
* Java
* Javascript

### 数据
* MySQL
* MongoDB
* Redis

### Java类库
* Spring
* Spring Boot
* Guava
* Swagger2
* SpringCloud(大型系统使用)

### 内部服务
* ActiveMQ(小型系统使用)/Kafka(中大型系统使用，依赖ZooKeeper)
* Quartz
* ElasticSearch
* ZooKeeper(中大型系统使用)

### 外部服务
* 七牛

### 运维系统
* docker
* Jenkins
* Open-Falcon

# 资料
1. [大数据](https://andrewwang79.gitbooks.io/javadev/cloud/SUMMARY.html#%E5%A4%A7%E6%95%B0%E6%8D%AE)
1. [版本发布模型](http://wangyaqi.cn/2015/05/18/git/)
1. [](http://lja.swao.cn/#/search/pageUI)(18702693501/123456)
1. [版本定义规范](https://semver.org/lang/zh-CN/)
1. [理解OAuth 2.0](http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html)
1. [WebAPI安全](http://www.cnblogs.com/developersupport/p/WebAPI-Security.html#authentication-authorization)

## 快速开发框架
* [Dubbo](http://dubbo.io/Developer+Guide-zh.htm)：RPC+ZooKeeper
* [spring-wind](https://git.oschina.net/juapk/spring-wind)：可参考代码和代码结构。
* [iBase4J](https://git.oschina.net/iBase4J/iBase4J)：采用了ZooKeeper，分布式服务理念
* [Hasor-RSF](https://www.oschina.net/p/Hasor-RSF)：分布式服务框架
* [Redkale](http://redkale.org/)：有点大。第三方接入采用插件模式
* [eova](http://git.oschina.net/eova/eova)：老了，可参考思想

## 方案
* [sharding-jdbc](http://git.oschina.net/dangdangdotcom/sharding-jdbc)
* [告别手写 API文档生成工具推荐](http://www.csdn.net/article/2013-02-20/2814189-API_DOC_TOOLS)
* [阿里完整自动化测试解决方案 macaca](https://yq.aliyun.com/articles/8310)
