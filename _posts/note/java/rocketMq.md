## 实现过程

### 1.配置主题

```
@RocketMQMessageListener(nameServer = "${rocketmq.name-server}",
        topic = "${rocketmq.base.normal.stock.order.merge}",// 主题
        consumerGroup = "BaseNormalStockOrderMergeConsumer",
        consumeThreadMax = 5)// 允许的最大线程数
```

### 2.定义类

实现 implements RocketMQListener `<Object>的接口`

```
implements RocketMQListener<Object>
```


### 2.接收消息

```
 onMessage(Long batchId) 
```

将消息解析成需要的对象

## 注意事项

1. 在recketMq中定义的成员变量，是所有线程共享的。
