## 有序消费



### 设置

@RedisListener(queue = "你的队列名", virtual = 1, concurrency = 1, maxConcurrency = 1)



### 原理

virtual = 1代表队列数，服务器和 virtual 一一对应，服务器>virtual的话。那就只有1台服务器消费1个队列。

要保证有序，就只能有一台服务器在消费，同时只能有一个线程。



 concurrency = 1, maxConcurrency = 1代表最小线程和最大线程。如果小的是1  大的是64.      任务少的话会1个线程执行。超过1的8倍的话。也就是8个任务会陆续开启新线程执行。直到满64个线程。 