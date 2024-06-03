## 基础配置

命名空间，同一个redis环境隔离

spring.redismq.namespace

应用名，后续通过控制台展示不同应用的集群

spring.redismq.applicationName=redisMQ-Client

## 全局通用配置

延时队列拉取的头部消息数量  

spring.redismq.globalConfig.delayQueuePullSize=100  

单个虚拟队列消费的锁定时间  

spring.redismq.globalConfig.virtualLockTime=10  

单个虚拟队列消费看门狗的续期时间  

spring.redismq.globalConfig.virtualLockWatchDogTime=8  

队列最大大小  

spring.redismq.globalConfig.queueMaxSize=100000  

是否全局开启事务提交后发送  

spring.redismq.globalConfig.sendAfterCommit=true  

开启seata事务  

spring.redismq.globalConfig.seataState=false  

打印核心消费日志  

spring.redismq.globalConfig.printConsumeLog=false  

任务执行超时时间 ms  

spring.redismq.globalConfig.taskTimeout=120000  

任务阻塞等待轮询时间 ms  

spring.redismq.globalConfig.taskWaitTime=1000  

最大机器数量  

spring.redismq.globalConfig.maxWorkerIdBits=8

## 队列配置

消费者数量（并发度），会被注解redis监听替换  

spring.redismq.queueConfig.concurrency=1  

最大消费者数量  

spring.redismq.queueConfig.maxConcurrency=64  

消费者重试次数  

spring.redismq.queueConfig.consumeRetryMax=1  

生产者重试次数  

spring.redismq.queueConfig.producerRetryMax=1  

发送者重试时间间隔（毫秒）  

spring.redismq.queueConfig.producerRetryInterval=200  

消费者重试时间间隔（毫秒）  

spring.redismq.queueConfig.retryInterval=500  

ack模式（字符串形式，与AckMode枚举对应）   auto和maual

spring.redismq.queueConfig.ackMode=AUTO

虚拟队列数量  

spring.redismq.queueConfig.virtual=1

## 生产者配置

生产者重试次数   spring.redismq.producerConfig.producerRetryCount=30     

生产 loadBalance 加载服务 重试   

spring.redismq.producerConfig.loadBalanceRetryCount=100  

生产 loadBalance 加载服务 重试间隔

spring.redismq.producerConfig.loadBalanceRetryMills=10    

生产者重试间隔   

spring.redismq.producerConfig.producerRetrySleep=200    

生产者批量发送消息限制最大数量   

spring.redismq.producerConfig.producerMaxBatchSize=200     

生产者消息确认机制  

spring.redismq.producerConfig.productAck=ASYNC     

打印核心生产日志  

spring.redismq.producerConfig.printProducerLog=true     

忽略rpc错误请求，只有同步的时候有效  

spring.redismq.producerConfig.ignoreRpcError=true     

发送消息超时60秒 rpc默认30秒  

spring.redismq.producerConfig.sendMaxTimeout=60000     

生产者异步发送队列大小。小了影响吞吐量，默认10000  

spring.redismq.producerConfig.producerBasketSize=10000





