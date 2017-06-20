## 官网&源码 ##

官网：[http://dubbo.io/](http://dubbo.io/)
源码：[https://github.com/alibaba/dubbo](https://github.com/alibaba/dubbo)

## 注册中心 ##

官方推荐使用zookeeper作为注册中心，所以先自行安装zookeeper

## dubbo admin 启动失败 ##

官方最新源码的版本是2.5.4-SNAPSHOT，通过源码编译的dubbo admin是无法在jdk1.8以上的版本运行的，

所以需要修改依赖库的版本，具体修改如下：

1、webx的依赖改为3.1.6版

```
    <dependency>
        <groupId>com.alibaba.citrus</groupId>
        <artifactId>citrus-webx-all</artifactId>
        <version>3.1.6</version>
    </dependency>
```

2、添加velocity的依赖

```
    <dependency>
        <groupId>org.apache.velocity</groupId>
        <artifactId>velocity</artifactId>
        <version>1.7</version>
    </dependency>
```

3、对依赖项dubbo添加exclusion，避免引入旧spring

```
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>dubbo</artifactId>
        <version>${project.parent.version}</version>
        <exclusions>
            <exclusion>
                <groupId>org.springframework</groupId>
                <artifactId>spring</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
```

确定war包解压后lib目录没有spring 3 以下的依赖就能运行正常了。

## 参考文档 ##

[2.5.4-SNAPSHOT dubbo admin error](https://github.com/alibaba/dubbo/issues/50)
