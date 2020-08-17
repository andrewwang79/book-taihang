# 事件处理
## 概要
* 通过消息队列完成
* 采用订阅模式：生产者发布消息，消费者订阅并处理
* 消息必须设置成持久化

## MQ方案
### 架构
* 业务-生产者：{Biz}Service，如TradeService。
* 业务-消费者：{Biz}Handler，如IncomeHandler。
* 框架-业务：EventDispatchService（事件分发，可不用消息队列），MsgDeliveryHandler（信息投递消费者）
* 框架-基础：MQService（消息队列服务）

### 调用方(生产者)工作
* {Biz}Service通过EventDispatchService发布消息
* {Biz}Service提供指定日期范围内的业务消息

### 业务方(消费者)工作
* {Biz}Handler注册事件处理到EventDispatchService，通过EventDispatchService接收消息，处理消息
* {Biz}Handler定期查询负责的业务的消息是否都已消费，没有消费则加入到MQ等待处理

### 消息结构
* 事件：如trade.finish
* data（json格式）：数据。
* 原则：如果db有值（如订单），则使用id或者code。无值（如日志）则保存完整数据。
* 实例：id和code二选一
```javascript
{
    event: 'trade.finish',
    ver: '1',
    time: 'yyyy-MM-dd HH:mm:ss'
    data: {
        id: 123456,
        code: '123456'
    }
}
```

## 使用案例
### 信息发送：如短信，微信通知等
* 事件：msg.delivery
* data结构：
```javascript
{
    [{
        type: 'SMS',
        receivers: ['13912345678'],
        tpl: {
            code: 'tpl_23423423',
            text: '',
            params: {userName: '旺旺', expireSecond:'60'}
        }
    },
    {
        type: 'WX',
        receivers: ['453rsfstslf3rwfsfs'],
        tpl: {
            code: 'tpl_wx322345364',
            text: 'hello {userName}',
            params: {userName: '旺旺', expireSecond:'60'}
        }
    }]
}
```
* params支持扩展参数，比如阿里短信的默认前缀编码是ali_sms_prefix_code


* 如使用阿里短信，还需要配置默认签名。如th.sms.alibaba.prefix.default=阿里默认签名
* 模板实例：${product} 验证码${code}，有效期为${expiration}分钟，请尽快验证。${slogan}

## 参考
* [RabbitMQ](http://www.rabbitmq.com/getstarted.html)
* [MQ资料](https://www.zybuluo.com/zhou333666/note/564338)
* [RabbitMQ三种Exchange模式](http://www.gaort.com/index.php/archives/366)
