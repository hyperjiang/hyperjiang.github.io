## 安装 ##

从官网 http://maven.apache.org/ 下载解压，然后把安装路径加入系统PATH，即可使用。

## 配置中国镜像 ##

编辑maven安装目录下的conf文件夹下面的setting.xml，找到mirrors那一栏，加入如下配置：
```
    <mirror>
        <id>alimaven</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
    <mirror>
        <id>central</id>
        <name>Maven Repository Switchboard</name>
        <url>http://repo1.maven.org/maven2/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
    <mirror>
        <id>repo2</id>
        <mirrorOf>central</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://repo2.maven.org/maven2/</url>
    </mirror>
    <mirror>
        <id>ibiblio</id>
        <mirrorOf>central</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://mirrors.ibiblio.org/pub/mirrors/maven2/</url>
    </mirror>
    <mirror>
        <id>jboss-public-repository-group</id>
        <mirrorOf>central</mirrorOf>
        <name>JBoss Public Repository Group</name>
        <url>http://repository.jboss.org/nexus/content/groups/public</url>
    </mirror>
    <!-- 中央仓库在中国的镜像 -->
    <mirror>
        <id>maven.net.cn</id>
        <name>oneof the central mirrors in china</name>
        <url>http://maven.net.cn/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
```

## 命令行创建一个空项目  ##
```
mvn archetype:generate -DgroupId=com.example.helloword -DartifactId=helloword -Dpackage=com.example.helloword -Dversion=1.0 -DarchetypeCatalog=internal
```

## 参考资料 ##

[Apache Maven 入门篇](http://www.oracle.com/technetwork/cn/community/java/apache-maven-getting-started-1-406235-zhs.html)
[Maven生成可以直接运行的jar包的多种方式](http://xxgblog.com/2015/08/07/maven-create-executable-jar/)
