---
layout: post
title: 简单理解 Restful API
date:   2020-02-02 08:24:00
category: [Server]
tags: [Server,Web]
---


## 主要包含内容

<!--more-->

- 协议，一般使用HTTPS
- 域名，`https://api.example.com`
- 版本（Versioning），`https://api.example.com/v1/`
- 终点（Endpoint），表示API的具体网址。`https://api.example.com/v1/zoos`
- HTTP动词
- 过滤信息（Filtering）
- 状态码（Status Codes）
- 错误处理（Error handling）
- 返回结果，应该尽量使用JSON
- Hypermedia API

## 1. 基本要求：面向资源，使用HTTP动词

HTTP动词有下面五个（括号里是对应的SQL命令）

- GET（SELECT）：从服务器取出资源（一项或多项）。
- POST（CREATE）：在服务器新建一个资源。
- PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
- PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。
- DELETE（DELETE）：从服务器删除资源。

还有两个不常用的HTTP动词。

- HEAD：获取资源的元数据。
- OPTIONS：获取信息，关于资源的哪些属性是客户端可以改变的。

### 例子

```
GET /zoos：列出所有动物园
POST /zoos：新建一个动物园
GET /zoos/ID：获取某个指定动物园的信息
PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
DELETE /zoos/ID：删除某个动物园
GET /zoos/ID/animals：列出某个指定动物园的所有动物
DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物
```

### 过滤信息

```
?limit=10：指定返回记录的数量
?offset=10：指定返回记录的开始位置。
?page=2&per_page=100：指定第几页，以及每页的记录数。
?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
?animal_type_id=1：指定筛选条件
```


## 2.进阶：Hypermedia API
即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么。

例子
```
PUST /zoos
```

普通返回
```
{
  "zoos": "abc"
}
```

Hypermedia API 返回查找信息的接口：
```
{
  "zoos": "abc",
  "link": {
    "rel": "infomation", //rel是relationship的意思
    "url": "/zoos/info"
  }
}
```

即返回结果中提供链接，连向其他API方法

参考
[https://zhuanlan.zhihu.com/p/30396391](https://zhuanlan.zhihu.com/p/30396391)
[http://www.ruanyifeng.com/blog/2014/05/restful_api.html](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)


> Exchange blogroll： [http://laker.me/blog]( http://laker.me/blog )
> Github：[https://github.com/younglaker]( https://github.com/younglaker )

