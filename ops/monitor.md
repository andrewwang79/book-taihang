# 业务监控
* 推荐使用第三方监控
* 监控表结构：监控url，监控内容(没有内容则监控http200)，监控状态(正常，异常，确定异常)，异常次数，目标类型，目标编号

* 异常次数越多，查询间隔时间越长，超过次数则确定异常。
* 确定异常后，周期查询是否正常，正常则恢复正常。
* 恢复正常：重置异常次数
* 当监控确定异常或者恢复正常时，通知目标。
