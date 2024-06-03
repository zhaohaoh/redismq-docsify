# 服务端部署(控制台监控)

jar包部署

```
nohup java -jar redismq-admin-XXX.jar --server.port=8088 
--spring.redismq.client.host=你的redis地址 
--spring.redismq.namespace=你的分组

随后访问http://localhost:8088
```

docker部署

```java
docker run --name redismq-server -p 8088:8088 -e JAVA_OPTS="-Dspring.datasource.url=数据库地址 -Dspring.redismq.client.host=redis地址 -Dspring.redismq.client.username=XX -Dspring.redismq.client.username=password" registry.cn-hangzhou.aliyuncs.com/zhaohaoh/redis-mq:0.3.8
```



docker-compose部署

