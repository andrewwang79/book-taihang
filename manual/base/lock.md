# 锁

## 配置

| 名称 | 参数 | 默认值 |
| :----: | ---- | ---- |
| 锁定超时时间(毫秒) | th.lock.timeout | 5秒 |
| 锁定最大重试次数 | th.lock.maxTryCount | 5次 |
| 锁定重试等待时间(毫秒) | th.lock.sleepMS | 200毫秒 |

## 函数
| 类 | 函数 | 输入 | 输出 | 说明 |
| :----: | ---- | ---- |
| LockService | lock | String type, String id | LyLock | 锁定 |
| LockService | lock | String type, int id | LyLock | 锁定 |

## 使用
```Java
@Autowired
private LockService lockService;

try (LyLock lock = this.lockService.lock("类型", id)) {
  ...
}
```

## 说明
