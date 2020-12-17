# 开发规约

## 代码
1. 一个函数最多80行代码，建议30行

## 结构
1. 事务只在manager层。[资料](http://www.importnew.com/19489.html)
1. json只在API层
1. 操作不能放在if里。for里可以

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
