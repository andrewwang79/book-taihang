# 唯一号生成服务

## 方案
### 种类
| 类别 | 格式 | 说明 |
| :----: | ---- | ---- |
| 自增长 | {##}，{#BIZ}{##} | 需持久化当前值(如10001) |
| 模板 | RUD{#yyyy}{#MM}{#dd}{#hh}{#mm}{#ss}{##N3} | 通过模板生成号码 |
| 号池 | 无 | 号池中随机取号码 |

### 模板占位符
| 占位符 | 适用范围 | 实例 | 说明 |
| :----: | ---- | ---- |
| {#yyyy} | 自增长，模板 | 2017 | 日期 |
| {#MM} | 自增长，模板 | 08 | 月 |
| {#dd} | 自增长，模板 | 25 | 日 |
| {#hh} | 自增长，模板 | 11 | 小时 |
| {#mmm} | 自增长，模板 | 12 | 分钟 |
| {#ss} | 自增长，模板 | 13 | 秒 |
| {#BIZ} | 自增长，模板 | 11111 | bizId |
| {##} | 自增长 | 12346 | n位(基于自增长的当前值)随机数，数字 |
| {##N3} | 模板 | 123 | n位(基于数字)随机数，数字 |
| {##A2} | 模板 | aB | n位(基于数字)随机数，字母 |
| {##a2} | 模板 | ab | n位(基于数字)随机数，小写字母 |
| {##S3} | 模板 | 1ab | n位(基于数字)随机数，小写数字/字母 |
| 自定义业务占位符 | 自增长，模板 | 888123 | 如{MerchantNo}。可无限自定义，内嵌在{}，首字符不能是"#"。业务方生成时提供值 |

## 流程
### 自增长号码生成

```
拿到NumRule数据，在start_num字段上，每次加1

```

### 号池中随机取号码

```
根据号码类型，随机取出一个。
如果没有了，拿最后一个号码，加1

```

### 号池生成

```
定时检查号码池的可用数量是偶是否小于一定的值
if（小于）
    拿到配置规则，根据号段，生成一批号码
```

### 模板号码生成
```
function(num, plData) {
  for (match : num.match("{%s}")) {
    switch (match.text) {
      case "YYYY":
        num.replace(match, time.toYYYY());
        break;
      ...
      case "SS":
        num.replace(match, time.toSS());
        break;
      case "##%d": // n位随机数
        num.replace(match, RandomUtils.genNum(%d));
        text = time.toYYYY();
        break;
      default: // 业务占位符
        num.replace(match, plData.get(match.text));
        break;
    }
  }

  return num;
}

```

## 表结构

### 唯一号生成规则:th_num_rule

|列名|字段|类型|NULL|说明|
|:--------:|:--------:|:--------:|:--------:|:--------:|
|编号|id|LONG|N||
|编码|code|VARCHAR(50)|N|规则项。如订单号，退货单号等|
|类型|type|VARCHAR(50)|N|模板、号池、自增长|
|业务id|bizId|LONG|N|通用是0，专用，写用户id|
|业务类型|bizType：USER，MERCHANT等|VARCHAR(500)|N|通用是sys,USER，MERCHANT等|
|基准数值|startNum|INT(11)|Y|当前基准数值,针对自增长使用|
|规则|content|VARCHAR(500)|N||
|创建时间|createtime|DATE|N||
|状态|status|INT|N|||

### 号池:th_num_section

|列名|字段|类型|NULL|说明|
|:--------:|:--------:|:--------:|:--------:|:--------:|
|编号|id|LONG|N||
|号段|num_section|VARCHAR(500)|N||
|类型|type|VARCHAR(50)|N|order,returnOrder等|
|创建时间|createtime|DATE|N||
|状态|status|INT|N|||

### 号池明细:th_num_detail

|列名|字段|类型|NULL|说明|
|:--------:|:--------:|:--------:|:--------:|:--------:|
|编号|id|LONG|N||
|号码|num_detail|VARCHAR(50)|N||
|号段|num_section|VARCHAR(500)|N||
|类型|type|VARCHAR(50)|N|order,returnOrder等|
|创建时间|createtime|DATE|N||
|状态|status|INT|N|||
