---
title: MySQL学习笔记05_DDL语句
date: 2022-01-14 14:09:31
tags: [MySQL]
toc: true
---

# create database

```sql
/*
create database 用于创建数据库
格式 create database 数据库名
*/

-- 创建一个名为myDB的数据库
create database myDB

-- 注意一点,MySQL不允许在同一系统下创建两个相同名字的数据库
-- 可以使用if not exists来避免创建同名数据库的时候报错的问题
create database if not exists myDB


-- 创建数据库时候指定字符集和校对规则
-- 默认字符集 utf8
-- 默认校对规则 utf8_chiness_ci 简体中文,不区分大小写
create database if not exists myDB
default character set utf8
default collate utf8_chiness_ci
```

# alter database

```sql
-- alter database 用于修改已经创建或者存在的数据库的相关参数(字符集/校对规则)
/*
格式
alter database 数据库名
default character set 新字符集 
default collate 新校对规则
*/
```

# drop database

```sql
-- drop database 用于删除数据库(会删除整个数据库中的表和全部数据)
/*
drop database 数据库名

可以搭配if exists使用,防止当数据库不存在的时候存在报错
drop database if exists 数据库名
*/

/*
MySQL安装之后会自动创建`information_schema`和`mysql`两个系统数据库,删除之后MySQL会无法正常工作
*/
```

# use

```sql
-- MySQL中,use语句用来完成一个数据库到另外一个数据库的跳转
-- 格式 use 数据库名
-- 在使用数据库之前必须确定是哪个数据库
```

