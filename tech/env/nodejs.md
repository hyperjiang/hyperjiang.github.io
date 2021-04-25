# nodejs 开发环境搭建


1. 安装 [nvm](https://github.com/nvm-sh/nvm)


下载安装脚本（*需要科学上网*）：

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

编辑 `~/.zshrc` 加入下面语句：

```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

2. 安装 node

查看长期支持的版本（LTS = long-term support）

```
nvm list-remote --lts
```

安装最新的长期支持版本

```
nvm install --lts
```

查看安装完成的node和npm版本

```
node -v
npm -v
```

3. 安装 [cnpm](https://github.com/cnpm/cnpm)

这个是使用中国镜像的npm，可以极大提高在国内下载的速度

```
npm install cnpm -g --registry=https://registry.nlark.com
```

升级npm（可选）

```
cnpm install -g npm
```

4. 安装 [yarn](https://github.com/yarnpkg/yarn)

```
cnpm install --global yarn
```
