## 安装 ##

因为ES是java编写的，可以直接下载编译好的可执行文件运行即可。同时官方也有提供通过包安装的方式。比如Ubuntu下面可以执行下列语句安装：

``` wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - ```

``` echo "deb https://packages.elastic.co/elasticsearch/2.x/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-2.x.list ```

``` sudo apt-get update && sudo apt-get install elasticsearch ```

如果要加入开机启动，可以执行：

``` sudo update-rc.d elasticsearch defaults 95 10 ```

*默认的安装目录是 /usr/share/elasticsearch ，默认的配置目录是 /etc/elasticsearch ，默认的日志目录是 /var/log/elasticsearch  *

使用包安装的方式启动ES得用 ``` sudo service elasticsearch start ```

关闭服务 ``` sudo service elasticsearch stop ```

直接运行安装目录下的ES会报找不到配置文件的错误

官方包安装文档：[https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-repositories.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-repositories.html)

ES有很多插件，本人认为最有用的一个是 elasticsearch-head ，这个是一个纯 html5 + js 编写的图形界面，github地址：[https://github.com/mobz/elasticsearch-head](https://github.com/mobz/elasticsearch-head)

安装很简单，运行 ``` sudo elasticsearch/bin/plugin install mobz/elasticsearch-head ``` 就会在ES的插件目录安装好，然后通过浏览器访问 http://localhost:9200/_plugin/head/ 即可看到效果

## 配置 ##

ES的配置很简单，elasticsearch.yml 就是它的主要配置文件，这里说明几个关键点。

network.host 默认的设置是 \_local_ ，即监听本地网络（127.0.0.1），如果想对外开发，可以设置为 [\_site_, \_local_]

cluster.name 建议设置，默认设置是elasticsearch，这个是集群名字，几个不同的ES实例使用同一个集群的名字就能成为一个集群，当然为了让集群里面的机器能知道彼此的存在，还需要设置 discovery.zen.ping.unicast.hosts

比如说我们有两台机器，A机器的IP是192.168.1.1，B机器的IP是192.168.1.2，我们想让他们成为一个集群，那么A机器的设置是 ```discovery.zen.ping.unicast.hosts: ["192.168.1.2", "[::1]"]``` B机器的设置是 ```discovery.zen.ping.unicast.hosts: ["192.168.1.1", "[::1]"]``` 反正就是让他们相互能够发现对方，这样集群的健康状况就会是正常（绿色），如果一台机器挂掉了，那么健康状态就会变成警告（黄色）

如果不想搞集群，又不想看到健康状况是黄色，可以执行 ``` curl -XPUT http://localhost:9200/_settings -d '{ "number_of_replicas" :0 }' ``` ，表示索引的分片（shard）不做拷贝，不拷贝自然就不需要多一台机器来做热备，健康状况就会是绿色而不是黄色，这个可以参考：[http://stackoverflow.com/questions/23656458/elasticsearch-what-to-do-with-unassigned-shards](http://stackoverflow.com/questions/23656458/elasticsearch-what-to-do-with-unassigned-shards)

ES的集群做得很牛逼，基本可以认为互为主从，只要不是全部机器都挂掉都能保证业务正常进行，挂掉的机器重新开启就会自动修复，省心省力省时