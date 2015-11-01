---
layout: post
title:  SQL server / MySQL 创建使用临时表
date:   2015-08-04 08:24:00
category: [SQL]
---

## 方法一

###建表并插入数据：

    select [字段1,字段2,...,] into #临时表表名 from 表

<!-- more -->

 例如：
    
    select a.yewuyuan,b.name 
        into #tmp
        from SCM_SOrder a,CP_yewuyuan b
        where a.yewuyuan = b.id
        and a.Month>201412

### 查询临时表的数据 

    select [字段1,字段2,...,] from #临时表表名
    
例如：
    
    select * from #tmp

如果把现在的查询窗口关闭了，在重新打开，然后在在查询里输入，则会进行报错，提示 #tmp 无效。因为本地临时表只是用在当前用户的当前连接中。所以如果当前的连接退出，会自动销毁。

## 方法二
### 先建立临时表 

    create table #临时表名(
    字段1 约束条件,
    字段2 约束条件,
    .....)

例如：

     create table #tmp (
        id int,
        name varchar(50)
     )


### 再插入资料

    insert into #临时表名 select ...
    insert into #临时表名 values()

例如：

    insert into #tmp 
        select a.yewuyuan,b.name
        from SCM_SOrder a,CP_yewuyuan b
        where a.yewuyuan = b.id
        and a.Month>201412
        group by b.Name
        
    insert into #tmp select 001, 'Mike'
    insert into #tmp values(002, 'Nick')

## 其他
### 删除临时表 

    drop table #临时表表名