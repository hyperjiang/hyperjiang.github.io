## 安装&启动 ##

[官方下载页](https://zookeeper.apache.org/releases.html)

可自行找个国内的镜像站下载，例如：

```wget https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz```

解压后可自行挪到一个想存放的位置，例如：

```tar xzvf zookeeper-3.4.10.tar.gz; mv zookeeper-3.4.10 /usr/local/zookeeper-3.4.10```

配置文件在conf目录下，主配置文件名是zoo.cfg，可把zoo_sample.cfg改名然后编辑一下配置：

```mv zoo_sample.cfg zoo.cfg```

在配置里面指定存放数据的目录和监听的端口等，然后就可以运行

```bin/zkServer.sh start``` 启动服务了

## PHP扩展安装 ##

[pecl下载页](http://pecl.php.net/package/zookeeper)

```wget http://pecl.php.net/get/zookeeper-0.2.3.tgz```

这个扩展需要依赖zookeeper的c库，所以要先编译一下，源码在刚才解压的zookeeper目录下面的 src/c 子目录，执行

```./configure; make; make install;```

然后解压PHP扩展源码编译安装：

```
tar xvf zookeeper-0.2.3.tgz
phpize
./configure --enable-zookeeper
make
make install
```

编辑 php.ini 加入 extension=zookeeper.so
