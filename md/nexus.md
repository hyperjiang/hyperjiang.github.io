## 安装&启动 ##

[免费版下载页](https://www.sonatype.com/download-oss-sonatype)

选择对应系统的下载链接会重定向到实际的下载地址

```wget https://sonatype-download.global.ssl.fastly.net/nexus/3/nexus-3.2.1-01-unix.tar.gz```

解压后会有两个文件夹 nexus-3.2.1-01 和 sonatype-work，可以把这两个移到自己想存放的地址，比如

``` mv nexus-3.2.1-01 /usr/loca/nexus; mv sonatype-work /usr/local/sonatype-work ```

这两个目录必须放在同个父目录下，如果不打算这样干，必须修改nexus的配置：

``` vim /usr/local/nexus/bin/nexus.vmoptions ```

运行下列命令可以启动nexus：

``` /usr/local/nexus/bin/nexus start ```

启动需要等待几分钟，然后nexus会监听8081端口，可以用浏览器直接访问，默认用户名是admin，默认密码是admin123

登录后可以在管理后台添加其他管理用户

## 上传第三方jar包  ##

```
mvn deploy:deploy-file -DgroupId=<group-id> \
 -DartifactId=<artifact-id> \
 -Dversion=<version> \
 -Dpackaging=<type-of-packaging> \
 -Dfile=<path-to-file> \
 -DrepositoryId=<id-to-map-on-server-section-of-settings.xml> \
 -Durl=<url-of-the-repository-to-deploy>
```

注意部署的时候只能部署到Hosted类型的仓库中，示例：

```
mvn deploy:deploy-file -DgroupId=com.pingan \
 -DartifactId=pingan-open-sdk \
 -Dversion=1.1.0 \
 -Dpackagin=jar \
 -Dfile=open-sdk-1.1.0.jar \
 -DrepositoryId=nexus \
 -Durl=http://localhost:8081/repository/maven-releases/
```

## 把自己项目打的包上传到nexus  ##

首先在maven的全局配置里面的<servers>添加nexus账户密码信息
```
<server>
  <id>nexus</id>
  <username>admin</username>
  <password>admin123</password>
</server>
```

然后在项目的pom.xml的<project>下面添加子节点
```
<distributionManagement>
  <repository>
    <id>nexus</id>
    <name>Nexus Release Repository</name>
    <url>http://localhost:8081/repository/maven-releases/</url>
  </repository>
  <snapshotRepository>
    <id>nexus</id>
    <url>http://localhost:8081/repository/maven-snapshots/</url>
  </snapshotRepository>
</distributionManagement>
```

在项目更目录运行
```
mvn deploy
```
即可将jar上传到nexus私服

## 参考资料 ##

[使用nexus3搭建私有仓库](http://www.jianshu.com/p/dbeae430f29d)
[上传jar包到nexus私服](https://my.oschina.net/lujianing/blog/297128)
