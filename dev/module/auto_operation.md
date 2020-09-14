# 业务运营自动化

## 概要
* 是业务运营(确保业务正常运营)，不是系统运维(第三方运维监控软件，监控业务系统正常运行)
* 业务运营自动化：运营人员操作的工作，但可以通过自动化完成的
* 自动化工作

| 类型 | 实例 | 逻辑代码 |
| :----: | ---- | ---- |
| 通知 | 新订单，新退货单 | 通用 |
| 报警 | 卡充值风险，卡支付风险(如大额消费) | 定制 |
| 执行 | 商品定时上下架，未达标商品下架，第三方服务的自动关闭恢复机制 | 定制 |


## 设计
* 有通知组，收信可以是邮箱/微信/QQ。
* 通知机制，原理同信息推送【复用】
* 触发通知规则，可以很复杂，如何简单做？

### 第三方服务自动化方案
* 问题场景
  1. 第三方升级服务
  1. 网络异常
* 自动化
  1. 多次问题(规则可设置，比如1小时内3次都有问题)后关闭服务，后续如发现没有问题，则恢复服务。
  1. 关闭和恢复，都需通知