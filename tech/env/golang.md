# golang 开发环境搭建

## 下载安装

1. 在MacOS安装

```
brew install go
```

*需要科学上网*

2. 在Linux安装

直接下载安装包，中国镜像推荐 https://studygolang.com/dl

以 1.16.2 版本为例：

```
wget https://studygolang.com/dl/golang/go1.16.2.linux-amd64.tar.gz

rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.2.linux-amd64.tar.gz
```

## 设置环境变量

1. 设置可执行文件目录
```
export PATH=$PATH:/usr/local/go/bin
```

2. 设置中国镜像

```
go env -w GOPROXY=https://goproxy.cn,direct
go env -w GOSUMDB="sum.golang.google.cn"
```

3. 私有库不走代理

```
go env -w GOPRIVATE="*.gitlab.com,*.gitee.com"
```

## 查看版本和环境变量

```
go version
go env
```
