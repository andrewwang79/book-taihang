# 开始

* [代码仓库](https://gitee.com/qiya365/taihang)
* [演示地址]()

## 核心功能
| 功能 | 类 | 说明 |
| :----: | ---- | ---- |
| [系统启动](http://www.huangyunkun.com/2015/01/01/run-code-after-spring-boot-started/) | ApplicationStartup |  |
| API异常处理 | CustomExceptionHandler |  |
| [页面异常处理](https://www.sporcic.org/2014/05/custom-error-pages-with-spring-boot/) | CustomExceptionResolver |  |
| http异常处理 | resources/static/404.html |  |
| 跨域配置 | WebConfig的addCorsMappings |  |
| 缓存配置 | RedisConfig |  |

## 操作
### 新增业务API
| 项 | 参考 | 说明 |
| :----: | ---- | ---- |
| 对象(Model) | cn.taihang.middletier.model.Party |  |
| 数据库操作(Dao) | cn.taihang.middletier.dao.PartyRepository | 表名是class名称。如用native则是表名 |
| 逻辑服务(Service) | cn.taihang.middletier.service.PartyService | 复杂的自定义sql查询和业务逻辑 |
| API(Api) | cn.taihang.api.party.PartyController | [Restful](http://liuyanwei.jumppo.com/2015/05/28/spring-2.html) |
