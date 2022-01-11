---
title: MySQL学习笔记03
date: 2022-01-11 17:08:31
tags:[MySQL]
---

<!-- toc -->

# DQL语句

**Persons**

| id   | name | age  | city |
| ---- | ---- | ---- | ---- |
| 1    | 张三 | 19   | 武汉 |
| 2    | 李四 | 18   | 北京 |
| 3    | 王五 | 20   | 广州 |
| 4    | 赵六 | 22   | 北京 |
| 5    | 孙七 | 20   | 武汉 |

## select

作用: 从表格中选取数据,结果放入结果表(也称作结果集)

```sql
-- 使用格式 select 列名 from 表名

-- 如果需要查询多列的话,那么需要用逗号隔开
select id,name from Persons

-- 如果需要查询所有列的话,可以直接使用*
select * from Persons
```

`select id,name from Persons`这个查询得到的结果集如下
| id   | name |
| ---- | ---- |
| 1    | 张三 |
| 2    | 李四 |
| 3    | 王五 |
| 4    | 赵六 |
| 5    | 孙七 |

### distinct

查询过程中如果想要去除重复值,使用distinct

```sql
-- 使用格式 select distinct 列名 from 表名

-- 查询所有人员的城市
select distinct city from Persons
```

### where

用于有条件在表中选取数据

```sql
-- 使用格式 select 列名 from 表名 where 条件

-- 查询表中年龄为20的人员数据
select * from Persons where age = 20

-- 如果有多个条件使用and和or连接
-- 查询所有年龄大于18小于23的人员数据
select * from Persons where age >18 and age <23

-- 如果比较的依据不是数值类型(比如说城市是不是在武汉),字符串类型的话需要用单引号括起来(大部分用双引号也是可以的)
select * from Persons where city = '武汉'
```
下面这些是可以在where子句中使用的操作符

| 操作符  | 作用                       |
| :-----: | :------------------------- |
|    =    | 等于                       |
|   <>    | 不等于,有些SQL中可以写成!= |
|    >    | 大于                       |
|    <    | 小于                       |
|   >=    | 大于等于                   |
|   <=    | 小于等于                   |
| between | 在某个范围内               |
|  like   | 搜索某种模式               |

#### between

指定范围

```sql
-- 查询所有年龄在18到23之间的人员数据
select * from Persons where age between 18 and 23 -- 其实就相当于 age >=18 and age <=23

-- 如果想要查询年龄不在18到23这个区间的人员数据,可以使用not
select * from Persons where age not between 18 and 23
```

#### like

用来查找指定条件的语句(匹配字符串)

```sql
-- 查询所有名字为N开头的人员数据
select * from Persons where name like 'N%'

/*
上面的'N%'中,单引号是因为字符串要用单引号括起来,N%中的%是通配符,表示任意个字符
意思是N后面加上任意个字符都是可以匹配上的,比如'Nick' 'Ni',但是'LNi'这种就不会匹配
*/
```

|         通配符         | 作用                       |         示例         |
| :--------------------: | :------------------------- | :------------------: |
|           %            | 替换一个或者多个字符       |       `%lon%`        |
|           _            | 替换一个字符               |        `_uck`        |
|        [字符表]        | 表示表中的任意一个字符     |      `[lf]uck`       |
| [^字符表]或者[!字符表] | 表示不在表中的任意一个字符 | `[!123]`或者`[^123]` |

#### in

允许查找的时候指定多个值

```sql
-- 使用格式  select 列名 from 表名 where 列名 in (value1,value2)
-- 多个匹配值用逗号隔开,支持字符串和数值类型

-- 查询所有在长沙和武汉的人员数据
select * from Persons where city in ('长沙','武汉')
```

### top

规定需要返回的语句条目数,不同数据库系统不一定支持top

```sql
-- SQL Server
-- 格式 select top number|percent 列名 from 表名
-- 选取最前面的50条数据
select top 50 * from Persons
-- 选取前50%数据
select top 50 percent * from Persons

-- MySQL
-- 格式 select 列名 from 表名 limit number
-- 选取前50条数据
select * from Persons limit 50

-- Oracle
-- 格式 select 列名 from 表名 where rownum <= number
-- 选取前50条数据
select * from Persons where rownum <= 50
```



## insert into

用于在指定表格中插入一条数据

```sql
-- 格式 insert into 表名(列1,列2,列3) value(值1,值2,值3)

-- 如果是一条完整的数据,那么注意value后面的几个值要和表中的字段一一对应,表名后面可以省略列名
insert into Persons value(20,'赵六',17,'长沙')
-- 如果不是一条完整的数据,那么在表名后面加上你要插入的列名,value后面的几个值和列名一一对应
insert into Persons(id,name) value(21,'孙七')
```

## update

用于更新表中的数据

```sql
-- 格式 update 表名 set 列名 = 新值 where 条件

-- 可以同时修改多个数据,只需要用逗号隔开就行
update Persons set age = 17,city = '武汉' where name ='孙七'

-- 这里语句开始变长了,为了好看其实可以考虑多写几行,比如说
update Persons
set age = 17,city = '武汉'
where name = '孙七'

-- 特别注意下后面的where子句,update会更新所有满足条件的行
-- 上面例子是修改所有叫做孙七的年龄和城市,如果表中有多个孙七,那么所有孙七的数据都会被修改
-- 如果不写where子句,比如下面这种,会修改整个表的所有行
update Persons
set age = 17
```

## delete

用于删除表中的记录

```sql
-- 格式 delete from 表名 where 条件

-- 删除表中所有名为孙七的人员数据
delete from Persons where name = '孙七'

-- 删除表中所有数据
delete * from Persons
delete from Persons
```

