# 待整理进去的资料

## 错误和返回机制
### Preconditions.checkNotNull(id, "id"); // id是subcode

### ApiOutput的subcode
直接知道错误位置，减少看日志来定位
subcode本质是错误定位，如错误值
显示情况：if (测试环境 && subcode存在) 显示code[subcode]

非生产环境 + 非明确错误，有verbose(堆栈)

### 业务错误
  告知用户错误：无参数，参数错误，无库存
  开发错误：基础信息未配置。返回通用失败？
未知错误：堆栈

原则：每天看异常和错误，是最好的


## 权限
https://www.cnblogs.com/butterfly100/p/8698425.html
2 垂直权限（功能权限）
3 水平权限（数据权限）



# 架构
https://mp.weixin.qq.com/s/VpQvqRc8UxZLs5L3iyJoQQ。简单，适用，演化的原则
https://www.heguang-tech.com/blog/2020/architect/architect-or-framework/
## 3个：服务聚合拆分、事务、查询
http://blog.didispace.com/microservice-three-problem-1/
http://blog.didispace.com/microservice-three-problem-2/
https://www.heguang-tech.com/blog/2020/architect/how-to-design-micro-service/：事件源（Event sourcing），命令查询责任分离（CQRS）
https://www.jianshu.com/p/b264a196b177:服务下的数据一致性的几种实现方式之概述

https://edu.aliyun.com/roadmap/microservice
https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D

# 技术
深入探秘 Netty、Kafka 中的零拷贝技术！：https://c.m.163.com/news/a/F8LOAF400532447I.html
ZooKeeper 笔记(3) 实战应用之【统一配置管理】 https://www.cnblogs.com/yjmyzz/p/4604947.html




## 管理上级：https://mp.weixin.qq.com/s/zzLl5S6EgvffuDC_i-huzQ
工作项整理(不是汇报)，工作项进度，问题和风险
方案A：实施步骤，前置条件，优势，劣势，风险，结果，影响。
方案B：同上
