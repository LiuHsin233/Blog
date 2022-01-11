---
title: MySQL学习笔记03
date: 2022-01-10 17:08:31
tags:[MySQL]
---

<!-- toc -->

# SQL语句

数据库执行的所有工作都由SQL语句完成,可以分成DML和DDL两种

## DML 数据操作语言(Data Manipulation Language)

主要是对数据的增删查改(最常用的操作是查询)

| 指令        | 作用               |
| :---------- | :----------------- |
| select | 从数据库中查询数据 |
| update      | 更新数据表         |
| delete      | 从数据表中删除数据 |
| insert into | 插入数据           |

## DDL 数据定义语言 (Data Definition Language)

主要是创造和删除表格,也可以定义索引,构建表和表之间的联系,添加表之间的约束(一般是数据库管理员做的操作)

| 语句            | 作用           |
| :-------------- | :------------- |
| create database | 创建新的数据库 |
| alter database  | 修改数据库     |
| create table    | 创建新的表     |
| alter table     | 修改数据库表   |
| drop table      | 删除数据库表   |
| create index    | 创建索引       |
| drop index      | 删除索引       |

## 备注

### 注释方式

不同数据库的注释方式可能有些区别,这里只介绍两种,不过多展开

```sql
-- 单行注释方式,注释内容放到两个横杠后面
/*
多行注释方式,注释内容放到斜杠星星中间
这种注释方式可以跨任意行也能放到任意位置
*/
```

### 关于大小写

sql对大小写并不敏感,也就是说,英文字符的大小写并不影响语句内容

```sql
-- 以下两句并没有什么区别
select * from Persons
SELECT * FROM Persons
```

