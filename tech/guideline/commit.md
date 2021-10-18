# 代码提交约定

## 概述

代码提交约定（Conventional Commits）官网：https://www.conventionalcommits.org/en/v1.0.0/

## 格式约定

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

示例：

```
feat(lang): add polish language
```

## 关键词

参考：https://github.com/commitizen/conventional-commit-types/blob/master/index.json

- feat: 增加新功能/特性

- fix: bug修复

- docs: 编写文档

- perf: 优化性能的代码改动

- refactor: 非功能或者bug修复的代码改动

- style: 代码格式改动，不涉及逻辑修改

- test: 编写单元测试

- build: 针对编译或者外部依赖的改动

- ci: CI配置或者脚本变更

- chore: 非代码和单元测试的其他变更

- revert: 回滚提交
