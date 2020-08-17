# 任务计划

---
### 命名规范

1. jobName唯一 尽量以bizType_bizId为规则命名
2. jobGroup 尽量以操作类型__业务模块_业务类型为规则命名
3. 时刻和cron的转换方法（DateUtils.date2cron()）
4. quartz的运行结果,查询boss的定时任务

```
例：
jobName:  资源分发-资源包分发id
jobGorup:  disposable_终端分发_分发

jobName： 创建资源包/立即创建资源包
jobGroup: 终端分发-资源包创建/立即创建

jobName： 报表类型
jobGroup: 电商-报表

jobName： 商品-商品id
jobGroup: 电商-上架

jobName： 天气
jobGroup :系统-天气
```
