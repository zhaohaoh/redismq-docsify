## 消息持久化(消息日志)

### 服务端持久化简介

目前框架最新版0.3.8提供了支持服务端(控制台)，进行消息持久化的功能。为保证发消息稳定性，默认异步进行持久化。

此功能暂不保证消息100%可靠性的持久化。但是可以保证非异常场景下生成消息日志。服务端的可靠性可以通过集群，暂时也不提供可靠性方案。但可以用来回溯消息和消息再消费。

### 以下是开启持久化的关键点

1.开启持久化通信后，消息持久化通信失败暂不影响消息发送到redis

2.底层通信通过tcp

3.持久化目前只提供DB单表存储的方式



###  创建表结构

```sql
CREATE TABLE `redismq_message` (
                                   `id` varchar(50) NOT NULL DEFAULT '' COMMENT '消息id',
                                   `queue` varchar(255) NOT NULL DEFAULT '' COMMENT '队列',
                                   `tag` varchar(255) NOT NULL DEFAULT '' COMMENT '标签',
                                   `key` varchar(255) NOT NULL DEFAULT '' COMMENT '消息唯一id用来hash均衡',
                                   `body` varchar(2500) NOT NULL DEFAULT '' COMMENT '消息体',
                                   `virtual_queue_name` varchar(255) NOT NULL DEFAULT '' COMMENT '虚拟队列',
                                   `offset` bigint(0) NOT NULL DEFAULT 0 COMMENT '偏移量',
                                   `header` varchar(255) NOT NULL DEFAULT '' COMMENT '头',
                                   `status` tinyint(0) NOT NULL DEFAULT 0 COMMENT '消息状态',
                                   `create_time` datetime(0) NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
                                   `update_time` datetime(0) NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP(0) COMMENT '更新时间',
                                   PRIMARY KEY (`id`),
                                   INDEX `idx_queue`(`queue`) USING BTREE,
                                   INDEX `idx_offset`(`offset`) USING BTREE,
                                   INDEX `idx_create_time`(`create_time`) USING BTREE
) COMMENT = 'redismq消息表';
```



### 持久化相关配置

增加如下配置

#### 客户端（发送消息端）

```
# 通信的端口 默认端口
spring.redismq.netty-config.server.port=10520
# 是否开启通信 默认false
spring.redismq.netty-config.client.enable=true
# 是否异步持久化
spring.redismq.producer-config.product-ack=async
# 通信失败不影响消息发送到redis
spring.redismq.producer-config.ignoreRpcError=true

# 客户端通信健康检查，开启则会检查服务端通信是否正常，默认关闭
# 如果需要启动时检查服务端通信是否正常，则可以设置为true
spring.redismq.netty-config.client.health=false
```

#### 服务端

```
# 通信的端口 默认端口
spring.redismq.netty-config.server.port=10520
# 是否开启通信 默认true
spring.redismq.nettyConfig.server.enable=true

spring.datasource.url=jdbc:mysql://你的持久化mysql地址
spring.datasource.username=你的账号
spring.datasource.password=你的密码
```

