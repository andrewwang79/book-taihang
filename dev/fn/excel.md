# excel导入导出

## 资料
* [jxls](http://jxls.sourceforge.net/)
* [模板导出](http://blog.csdn.net/zdp072/article/details/30310473)
* [数据导入](http://gyl892014311.iteye.com/blog/2238764)

* Service是ExcelService

## 数据导入规则
数据导入时有强制更新选项，本选项只用于信息类的更新(如商品)。一次性信息（如单据）都不能做强制更新。
```
if (id 已存在) {
  if (强制更新)
    更新
  else
    报错
} else {
  新增
}
```

## 导入结果json格式
### 商品列表导入
#### 文档格式错误
```javascript
data: {
  errors: [
    '列不存在[价格]'
  ],
  item_errors: [
  ]
}
```

#### 商品错误
```javascript
data: {
  total: 10,
  success: 9,
  exist: 0,
  fail: 1,
  errors: [
  ],
  item_errors: [
    {
         id：'SP111',
         errors: [
           ‘价格为负[-3.5]’
         ]
    }
  ]
}
```

### 入库单列表导入
#### 入库单错误
```javascript
data: {
  total: 10,
  success: 9,
  exist: 0,
  fail: 1,
  errors: [
  ],
  item_errors: [
    {
         id：'RKD123',
         errors: [
           ‘入库时间错误’
         ],
         item_errors: [
           {
                id：'SP111',
                errors: [
                  ‘条码不存在’,
                ]
           }
         ]
    }
  ]
}
```

## 导入通用逻辑
```
ImportResult importBiz() { // 特定业务
  list = this.service.getDataList();
  ActionResult fnAction(String id) {
    return this.service.add(list[id]);
  }
  boolean fnExist(String id) {
    return this.service.exist(list[id]);
  }

  return import(list, fnAction, fnExist);
}

ImportResult import(list, fnAction, fnExist) { // 通用逻辑
  ImportResult ir;
  for(item : list) {
    if (fnExist(item)) {
      ir.addExist(item.id);
      continue;
    }
    ActionResult ar = fnAction(item.id);
    if (!ar.result) {
      ir.addFail(item.id, ar.msg);
    } else {
      ir.addSuccess(item.id);
    }
  }
  return ir;
}
```
