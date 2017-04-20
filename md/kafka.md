## 安装&启动 ##

Kafka依赖ZooKeeper，所以首先得安装ZooKeeper，参考[ZooKeeper安装](/md/zookeeper.md)

下载：

```wget http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/0.10.2.0/kafka_2.11-0.10.2.0.tgz```

运行：

```bin/kafka-server-start.sh config/server.properties &```

## 参考资料 ##
[官方入门参考](http://kafka.apache.org/quickstart)
