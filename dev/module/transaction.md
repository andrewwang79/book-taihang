# 分布式事务
当一个程序含有多种业务时，业务之间会互相影响。现在让各个业务独立发展，每个地方都只做一件事情。只要一个地方负责了多项事情，就存在解耦的可能。

##例子
1. 支付宝转账1000元到余额宝

   常规做法：支付宝扣除1000元，余额宝增加1000元，告诉用户转账成功
   解耦做法

   (1)：支付宝扣除1000元，做扣款记录，并告诉用户扣款成功。

  (2)：余额宝增加1000元，通知用户到账成功，并做转账成功记录。

  说明：把扣除1000元，增加1000元从一个步骤分开两个步骤走，这样达到解耦的目的。

2. 到银行办理存钱，贷款，申请网盾等业务。可以先存钱，后去贷款，再去申请网盾。也可以自己去存钱的时候，通知贷款，申请网盾的工作人员先帮忙办理。这样就能大大提高效率。

##好处
1. 缩短程序运行时间，能够避免程序运行时间长
2. 主流程压力减少，避免分流程的报错影响主流程
3. 消峰填补，减少系统的压力

# 事务和并行任务
| 类型 | 顺序 | 回滚 | 说明 |
| :----: | ---- | ---- | ---- |
| 事务(串行) | 有 | 无 | 事务启动时先检查预留资源，确保必然成功 |
| 事务(并行) | 无 | 有 | 无顺序的原因：有依赖的事务job先串行做好，再并行 |
| 并行任务 | 无 | 无 | job之间相互无影响 |

## 实例
事务：
1. 服务能否提供（必然周日阿姨没有了）【实时确认成功】

并行任务：
1. 注册发优惠券【必然成功】
1. log

## 并行任务
1. checklist，业务字典
1. jobList，业务实例，有多个job
1. jobRecord，job执行情况

## 串行事务
事务【转账】，2个job【A扣钱，B加钱】
1. 转账worker(串行)：A-100，B+100【账户不存在】，A+100。
1. 转账worker(并行)：B+100，A-100。最终一致，任意一个失败都回滚。每个job都有回滚逻辑。

## 并行事务：保证最终一致【终点或者起点】
事务【下单】，3个job【创建订单，创建工单，使用优惠券(修改状态)】

## 并行事务实现
接口实现步骤
1. 根据业务字典生成业务示例
1. 通知业务执行
1. 监听器监听

##监听器要启动少，且监听不能太集中，要有针对性

通知业务执行：
1. MQ通知执行
1. jobList执行成功（如果执行失败，通知接口监听器执行失败）
1. 检查其他job有没有执行成功，全部执行成功，通知接口的监听器执行成功

## 并行任务实现
接口实现步骤
1. 根据业务字典生成业务示例
1. 通知业务执行
1. 返回前端数据


通知业务执行
1. MQ通知执行
1. jobList执行成功，执行失败
1. 定时器检查，未成功执行的重新执行一次


##相关表结构
###业务字典  th_check_list
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 业务code  | code | VARCHAR(50) | N |业务。比如下单，发货。代表一个整体的业务 |
| 业务listCode | list_code | VARCHAR(50) | N |业务明细编码 |
| 业务分类 | category | VARCHAR(50) | N |并行事务，并行任务 |
|规则 | regular | text | Y | json格式。比如{expiretime:0.5}代表过期时间30分钟|
|状态     |  status| int    |N||



###业务实例表  th_job_list
| 列名 | 字段 | 类型 | NULL | 说明 |
| -- | -- | -- | -- | -- |
| 编号 | id | LONG | N | |
| 业务字典Id |check_list_id  | LONG | N | |
| 业务分类 | category | VARCHAR(50) | N |并行事务，并行任务 。|
| 参数 |  params| text | Y | 存放参数，json格式 |
|执行结果     |  result| int    |N| 未执行，执行失败，执行成功|
| 过期时间 | expiretime | Date | Y | null代表无过期时间 |
| 创建时间 | createtime | Date | N | |
|状态     |  status| int    |N| |
