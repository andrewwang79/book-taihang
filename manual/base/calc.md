# 自动计算
## 业务
* 通过公式计算结果
* 常用于收入计算，清分等
### 分工
* 计算方：基于对象数据计算结果
* 业务方：提供对象数据，提供时间范围内符合要求的待计算业务对象列表

## 流程
### 常规
业务方发起计算请求，计算方计算结果

### 确认
1. 确保所有的业务对象都会处理
1. 计算方周期发起请求给业务方，获取时间范围内符合要求的待计算业务对象列表，计算方重新计算

## 功能
1. 支持线性公式和阶梯式公式
1. 公式有code，支持公式嵌套
1. 不支持公式集
1. 不支持实时公式更新
1. 支持模拟计算：需提供所有的输入参数

## 系统设计
1. 第三方库有mvel、SpEL、Aviator，现采用[SpEL](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/expressions.html)。
1. 公式调用要提供：公式编码和参数列表(类型，编码)

### 表结构
公式表：编码，名称，输入参数列表(json：编码code,名称name,数据类型type)，公式

### 公式
公式定义采用占位符参数形式。比如：
* incoming1=#personCount \* 1
* incoming2=#saleFee \* #percent
* incoming=#fnCalcDecimal('incoming1', #root)+#fnCalcDecimal('incoming2', #root)
* bonus=#fnCalcDecimal('incoming', #root) \* 10%
* total=#fnCalcDecimal('incoming', #root) + #fnCalcDecimal('bonus', #root)

### 公式嵌套
```
#fnCalcDecimal('调用公式的编码', #root)
```
