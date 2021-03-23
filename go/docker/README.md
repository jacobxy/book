# kafka 操作
[链接](https://blog.csdn.net/qq_26375325/article/details/105251205)

## 创建topic

```
kafka-topics.sh --create --topic test \
--zookeeper zookeeper:2181 --replication-factor 1 \
--partitions 1
```

## 生产者发送消息

```
kafka-console-producer.sh --topic=test --broker-list kafka:9092
```

## 消费者接收消息

```
kafka-console-consumer.sh --bootstrap-server kafka:9092 --from-beginning --topic test
```

## docker-compose.yml

host.name advertised.host.name [链接](https://blog.csdn.net/chenfeng_sky/article/details/103124473)

可外网访问的docker kafka容器
KAFKA_ADVERTISED_HOST_NAME: kafka
KAFKA_ZOOKEEPER_CONNECT:zookeeper:2181 (zookeeper->container_name)
KAFKA_LISTENERS: INSIDE://:9092,OUTSIDE://:19092
KAFKA_ADVERTISED_LISTENERS: INSIDE://kafka:9092,OUTSIDE://192.168.23.239:19092

[参考1](https://www.jianshu.com/p/a6d1cc14ab02)
[参考2](https://blog.csdn.net/weixin_38251332/article/details/105638535)
