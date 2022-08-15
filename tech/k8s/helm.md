# Helm

官网 https://helm.sh/

## 一、基本概念

`Chart`: `图表`是一个 Helm 包。它包含在 Kubernetes 集群内运行应用程序、工具或服务所需的所有资源定义。类似 Homebrew 公式、Apt dpkg 或 Yum RPM 文件

`Repository`: `仓库`是收集和共享 `Chart` 的地方

`Release`: `部署`是在 Kubernetes 集群中运行的 `Chart` 的实例。一个 `Chart` 通常可以多次安装到同一个集群中，每次安装时，都会创建一个新 `Release`。举个例子，如果您希望在集群中运行两个 MySQL 数据库，则可以安装两次 MySQL `Chart`，他们会有两个对应的 `Release`，并且每个 `Release` 都有自己的名称

## 二、安装（MacOS）

方式一：

```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

方式二：

```
brew install helm
```

## 三、仓库管理

### 3.1 添加仓库

官方的例子是添加 `bitnami`

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

### 3.2 查看已添加的仓库列表

```
helm repo list
```

### 3.3 更新仓库

```
helm repo update
```

### 3.4 删除仓库

```
helm repo remove
```

## 四、图表部署管理

### 4.1 查找图表

*支持模糊搜索*

1. 从 [Artifact Hub](https://artifacthub.io/) 搜索图表：

```
helm search hub [CHART]
```

2. 从本地仓库搜索图表：

```
helm search repo [CHART]
```

### 4.2 安装图表

```
helm install [NAME] [CHART] [flags]
```

查看用法详细描述可以跑

```
helm install -h
```

下面的例子是安装 mysql

```
helm repo update   # Make sure we get the latest list of charts
helm install bitnami/mysql --generate-name
```

#### 4.2.1 安装的可选方式

1. 从仓库安装，例如 `helm install happy-panda bitnami/wordpress`
2. 从本地图表压缩包，例如 `helm install foo foo-0.1.1.tg`
3. 从本地目录，例如 `helm install foo path/to/foo`
4. 从URL，例如 `helm install foo https://example.com/charts/foo-1.2.3.tgz`

#### 4.2.2 配置图表

**1. 查看图表支持的配置项**

```
helm show values CHART
```

例如 `helm show values bitnami/wordpress`

**2. 覆盖默认配置**

把要修改的配置写入一个 yaml 文件，安装的时候通过 `-f` 指定该文件即可，示例：

```
echo '{mariadb.auth.database: user0db, mariadb.auth.username: user0}' > values.yaml
helm install -f values.yaml bitnami/wordpress --generate-name
```

也可以通过 `--set` 参数来修改配置的值，例如 `--set a=b,c=d`

**Tips:**
- `-f` 可以多次使用指向多个文件，这种情况最右边的文件优先级最高
- `--set` 的优先级比 `-f` 高

### 4.3 查看部署情况

查看部署列表

```
helm list [flags]
```

查看某个部署的状态

```
helm status RELEASE_NAME [flags]
```

### 4.4 版本升级和失败回滚

```
helm upgrade [RELEASE] [CHART] [flags]
```

`helm upgrade` 可以用来升级版本或者修改部署的配置，例如

```
helm upgrade -f panda.yaml happy-panda bitnami/wordpress
```

我们可以用 `helm get values RELEASE_NAME` 来检查新配置有没有生效，比如针对上面的例子可以用 `helm get values happy-panda`

如果升级失败，可以使用 `helm rollback [RELEASE] [REVISION]` 进行回滚，例如 `helm rollback happy-panda 1`

*Tips: 部署的版本每次都会加1递增，可以用`helm history [RELEASE]`查看历史版本*

### 4.5 卸载部署

```
helm uninstall RELEASE_NAME [...] [flags]
```

*uninstall 也可以是别名 del, delete, un*

## 五、定制图表

### 5.1 创建一个图表

```
helm create NAME [flags]
```

上面的命令会创建一个叫`NAME`的目录，里面会包含一系列定义图表的yaml文件：

```
foo/
├── .helmignore   # Contains patterns to ignore when packaging Helm charts.
├── Chart.yaml    # Information about your chart
├── values.yaml   # The default values for your templates
├── charts/       # Charts that this chart depends on
└── templates/    # The template files
    └── tests/    # The test files
```

如何通过修改yaml文件定制图表可以参考 https://helm.sh/docs/topics/charts/

### 5.2 验证格式是否正确

```
helm lint
```

### 5.3 打包

```
helm package [CHART_PATH] [...] [flags]
```
