# 微服务方案

## 说明
* 用于中大型产品开发
* 微服务化

## 思路
* 无依赖的通用服务做成一个基础微服务
* 有行业微服务

## 结构组成
j基础设施和基础库是基石
sc是总线，连接起每个微服务
三维图

### 基础设施
Redis，Zookeeper...
Spring Cloud

### 基础库
基础库
Spring增强库：防攻击，分布式支持(锁，MQ，缓存)

### 基础微服务
基础微服务
权限微服务

### 行业微服务
商城

## 治理
Spring Cloud admin
服务的可视化管理，如redis

### TBD
功能：组织机构、参数设置、字典管理
用户权限：角色用户、菜单及按钮授权、数据权限
用户：第三方登录、单点登录
其他功能：内容管理、任务计划、消息和通知
接入：支付、微信、存储
技术：唯一号生成、长连接(websocket)

操作日志
excel处理：如何交换文件，如果大了很不好。还是做成jar

## 资料
* [表参考](https://github.com/shuzheng/zheng/blob/master/project-datamodel/zheng.png)
