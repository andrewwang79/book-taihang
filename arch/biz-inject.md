# 业务注入
* 业务层服务注入框架层，这样框架层可以使用业务层服务

## 框架层使用业务层的用户

|  层级   | 类 |  说明 |
| --------   | -----  | ----  |
| 框架层   |   实体类UserAccount | 框架层使用的用户信息结构 |
| 框架层  |   服务类UserAccountService | 框架层其他类获取用户信息的入口，实例化IUserAccountService就是注入 |
| 框架层  |   接口类IUserAccountService |  |
| 业务层  |   服务类UserService，实现接口IUserAccountService | 继承接口就是定义注入类 |


## 框架层使用业务层的储值卡系统

|  层级   | 类 |  说明 |
| --------   | -----  | ----  |
| 框架层   |   实体类Card | 框架层使用的卡信息结构 |
| 框架层  |   服务类CardService | 框架层其他类使用卡系统的入口，实例化ICardService就是注入 |
| 框架层  |   接口类ICardService |  |
| 业务层  |   服务类CardService，实现接口ICardService | 继承接口就是定义注入类 |

# 用户的删除与合并

## 描述
为了方便对用户进行删除及合并

## 方案
1. 自定义一个@UserOperation注解；
1. 定义一个IUserOperation接口，并定义deleteUser（userId）和mergeUser（srcUserId，destUserId）两个方法;
1. 在XXXManager里面查询所有定义了@UserOperation的XXXService;XXXService实现IUserOperation接口,放入map；
1. 遍历map,执行相应的删除或合并操作,失败需提供日志;

## 实现
### 删除
1. 删除时提供一个userId,调用deleteUser（userId）;
1. 删除用户时提供一个口子,删除所有XXXService上注解了@UserOperation对应的信息;
1. 删除失败时需提供失败日志,方便手动删除;;

### 合并
1. 合并时需提供srcUserId( 合并方 )和destUserId( 被合并方 );
1. 合并用户时提供一个口子,在所有XXXService上面注解了@UserOperation执行对应的merge方法;
1. 删除失败时需提供失败日志,方便手动删除

## 实现
### XXXManager
```
    public void init() {
    for (Map:   this.context.getBeansWithAnnotation(UserOperation.class).entrySet()) {
            String key = entry.getKey();
            IUserOperation item = (IUserOperation) entry.getValue();
            this.map.put(key, item);
        }
    }

    public void deleteUser(Long userId) {
        for (Map.Entry<String, IUserOperation> entry : map.entrySet()) {
            try {
                IUserOperation item = (IUserOperation) entry.getValue();
                item.deleteUser(userId);
            } catch (Exception e) {
                log.error("删除失败的用户userId:" + userId + "  " + entry.getKey());
            }
        }
    }

    public void mergeUser(Long srcUserId, Long destUserId) {
        for (Map.Entry<String, IUserOperation> entry : map.entrySet()) {
        }
    }
```

### XXXService
XXXService均应实现IUserOperation接口
```
    @Service
    @UserOperation
    public class Test1Service implements IUserOperation{
    @Override
    public void deleteUser(Long userId) {
        System.out.println("test1  的  delete::::::::::::::;"+userId);
    }

    @Override
    public void mergeUser(Long srcUserId, Long destUserId) {
        System.out.println("test1  的  merge::::::::::::::;"+srcUserId+"   "+destUserId);
    }
}
```

### IUserOperation接口
```
        public interface IUserOperation {

             void deleteUser(Long userId);

                void mergeUser(Long srcUserId, Long destUserId);
        }
```
