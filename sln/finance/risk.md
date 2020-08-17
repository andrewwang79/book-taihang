# 风控

## 介绍
* ** 数据，数据，数据 **
* ** 事前，事中，事后 **

### 模型
![](http://img.blog.csdn.net/20160621114107796?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 当前情况
* 由传统的“rule-base”（规则模型）发展到今天的大数据为基础的实时+离线双层识别(风险学习引擎)。Hadoop，Spark等大数据大集群分布式处理框架的不断发展为风控技术提供了有效的支撑。
* 制度：风控/财务人员的审核，复核。

## 方案
### 获取风险
* 业务定义 -> 风险定义-> 风险分解 -> 风险策略

### 分析维度定义

## 系统
* 行为和交易实时监控

### 限额控制
1. 行为：充值，支付，密码输错
1. 限额：单次金额，日支付上限，密码错误次数

### 异常交易
1. 监控异常交易并警报，允许自动锁定卡。比如高频率的刷卡，短期高额刷卡

### 可疑交易

### 黑名单

### 风险等级评估

### 反洗钱

## 参考
* [交易系统和风控系统的架构怎么设计](https://www.zhihu.com/question/20860347)
* [京东基于Spark的风控系统架构实践和技术细节](http://www.infoq.com/cn/articles/jingdong-risk-control-system-architecture-based-on-spark)
* [携程大数据实时风控的架构及实践](http://f.dataguru.cn/article-10266-1.html)
* [P2P平台是怎么做风控的](https://www.zhihu.com/question/22465832)
* [风控分类模型种类（决策、排序）比较与模型评估体系](http://blog.csdn.net/sinat_26917383/article/details/51725102)
* [基于用户画像的腾讯大数据防刷架构](http://www.woshipm.com/pd/543957.html)
