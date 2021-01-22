# python 开发环境搭建

1. 安装 [pyenv](https://github.com/pyenv/pyenv)

```
brew install pyenv
```

2. 查看支持的版本

```
pyenv install -l
```

3. 安装 python，必须指定版本

```
pyenv install 3.9.1
```

4. 设置为全局使用

```
pyenv global 3.9.1
```

5. 把 `pyenv init` 放进 shell 配置

    *Mac 默认的 shell 是 zsh*

```
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.zshrc
```

6. 查看使用中的 python 版本

```
python --version
python3 --version
pip --version
```
