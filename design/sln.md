# 系统

## 层级
| 名称 | 说明 | 实例 |
| :----: | ---- | ---- |
| XXDao | 数据库 | 修改状态字段 |
| XXService | 实体对象的逻辑 | 停止服务 |
| XXManager | 业务逻辑，允许有其他Service | 商品上架 |
| BizManager | 业务板块逻辑，是业务板块间的唯一出入口 | 获取订单 |

* 函数归属名称，由作用用途决定。如数据库用途的就在dao层