# 其他规约

## sql查询
1. 查询条件和信息分离：尽量减少多表联查，只有属于查询条件的表才做关联。信息通过逻辑层获取
1. 粒度：都是原子级操作(类似API)

## 时间日期格式

| 项 | post传输 | get传输(url) |
| :----: | ---- | ---- |
| 日期时间 | 2017-07-31 11:01:23 | 20170731110123 |
| 日期 | 2017-07-31 | 20170731 |
| 时间 | 11:01:23 | 110123 |

## 异常
* 业务异常类：CustomBizException
* Preconditions自动返回PARAM_ERROR，错误字段是第二个参数
  * Preconditions.checkNotNull(code, "code");
  * Preconditions.checkArgument(isMobile(mobile), "mobile");
