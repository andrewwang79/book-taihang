# 示例
## 文档
```
### 用户下一个任务(/v1/task/user/next)
输入

| 名称 | 字段1 | 字段2 | 类型 | 必须 | 说明 |
| :----: | -- | -- | -- | -- | -- |
| 用户 | userId |  | INT | Y |  |

输出

| 名称 | 字段1 | 字段2 | 类型 | 必须 | 说明 |
| :----: | -- | -- | -- | -- | -- |
| 序列列表 | list |  | LIST(STRING) | Y |  |

返回码
```

## 代码
```
@RequestMapping("/create")
public ApiOutput create(@RequestBody String json) {
  log.info(LogUtil.gen("create", "json", json)); // log
  String name = ArrayUtil.getMapString(map, "name"); // 获取输入参数
  if (Strings.isNullOrEmpty(name) || name.length() > 50) { // 检查输入参数
      return new ApiOutput(ApiCodeEnum.PARAM_ERROR, "name");  // 基础返回码
  }

  ... 业务处理

  return new ApiOutput(SysApiCodeEnum.NO_SERIES_IN_TASK);  // 业务返回码

  int apiCode = annotationResultManager.submitSeriesAnnotationResult(id); // 业务层结果的返回码
  return new ApiOutput(apiCode);
}
```
