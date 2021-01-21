# REST 规范

## 概述

REST 是 `REpresentational State Transfer` 的缩写，它是一种用于分布式超媒体系统的软件架构，它的核心在于资源的规划。
一个URI(endpoint)就是一个资源。

## Endpoint规范

- 使用复数名词，不用动词
- 结尾不加斜杠“/”
- 正斜杠分隔符“/”用来指示层级关系
- 使用连字符“-”，不用下划线“_”
- 使用小写字母
- 使用复数

## 动作规范

使用下列 http method 来实现rest的动作：

- GET（SELECT）：从服务器取出资源（一项或多项）
- POST（CREATE）：在服务器新建一个资源
- PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）
- PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）
- DELETE（DELETE）：从服务器删除资源

## 常用状态码

- 200 OK 服务器返回用户请求的数据
- 201 CREATED 新建数据成功
- 204 NOT CONTENT 删除数据成功
- 400 BAD REQUEST 用户发出的请求有问题，参数错误
- 401 Unauthoried 表示用户没有认证，无法进行操作（用户未登录）
- 403 Forbidden 用户访问是被禁止的（用户已登录，但没有权限访问）
- 500 INTERNAL SERVER ERROR 服务器内部错误
- 503 Service Unavailable 服务不可用状态，多半是因为服务器资源不足

## 扩展阅读

[理解RESTful架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)

[HTTP状态码](https://restfulapi.net/http-status-codes/)
