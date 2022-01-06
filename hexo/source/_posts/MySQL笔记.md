---
title: MySQL笔记
date: 2021-03-27 16:42:42
tags:
---

<!-- toc -->


# 基本概念简介和mySQL的安装配置
## 基本概念介绍
### 数据库的作用

DataBase(DB)用来存放和管理数据

1. 数据共享
2. 减少数据冗余(每个应用不需要单独存放数据)
3. 数据独立
4. 数据集中管理
5. 数据一致性
6. 故障处理(遇到异常处理)
### 常用的数据库
1. MySQL 开源免费 关系型数据库管理系统
2. SQL Server 微软开发 关系型数据库管理系统 一般用于web存储数据
3. Oracle 世界使用最广泛之一
4. Sybase 开放 高性能
5. DB2 IBM开发 主要用于大型应用
    > 关系型数据库 由二维表的形式存放数据(可以用SQL查询语句)
    > 非关系型数据库(NoSQL) 存储格式灵活(不支持SQL查询语句)
### 关于SQL
结构化查询语言(Structured Query Language),简称SQL 访问标准数据库的标准计算机语言
## MySQL的安装和配置
## SQL语法
[SQL语法](http://www.w3school.com.cn/sql/index.asp)对于不同的SQL数据库可能有各自的私有拓展,但是都支持SQL标准

### 数据库表
关系型数据库以二维表方式存放数据,一个数据库中通常包含一个或者多个表

**Persons**

|  ID  | 姓名 | 年龄 | 城市 |
| :--: | :--: | :--: | :--: |
|  1   | 张三 |  19  | 武汉 |
|  2   | 李四 |  18  | 北京 |
|  3   | 王五 |  20  | 广州 |

上述表格Persons中包含三条**记录**,和四**列**(id 姓名 年龄和城市)
## SQL语句分类
数据库执行的所有工作由SQL语句完成,大致可以分为DDL,DML和DQL三种(SQL对大小写不敏感)

1. DML 数据操作语言(Data Manipulation Language)
主要是添加删除更新数据

   | 指令        | 作用               |
   | :---------- | :----------------- |
   | update      | 更新数据表         |
   | delete      | 从数据表中删除数据 |
   | insert into | 插入数据           |

2. DDL 数据定义语言 (Data Definition Language)
主要是创造和删除表格,也可以定义索引,构建表和表之间的联系,添加表之间的约束

   | 语句           | 作用           |
   | :------------- | :------------- |
   | creat database | 创建新的数据库 |
   | alter database | 修改数据库     |
   | create table   | 创建新的表     |
   | alter table    | 修改数据库表   |
   | drop table     | 删除数据库表   |
   | create index   | 创建索引       |
   | drop index     | 删除索引       |

3. DQL 数据查询语言(Data Query Language)

   主要是查询数据，是通常最频繁的数据库操作

   | 指令   | 作用               |
   | ------ | ------------------ |
   | select | 从数据库中查询数据 |

   

## DQL和DML语句

### select
作用 从表格中选取数据,结果存放在结果表(也称为结果集)
**语句使用格式 `select 列名 from 表名`**

```sql
-- 如果需要选取多个列则用逗号隔开
select ID,姓名 from Persons

-- 如果需要选取所有列可以直接使用*
select * from Persons
```

#### 关键字 distinct
在选取的时候 可能存在重复的值,可以加上distinct这个关键字来避免重复
**避免重复 `select distinct 列名 from 表名`**
#### where子句
用于有条件的在表中选取数据,可以搭配select使用
**格式 `select 列名 from 表名 where 条件`**
条件可以用的一些操作符

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

`select * from Persons where ID=2`
`select * from Persons where 名字='张三'`
对于条件中如果是数值则不需要加单引号,如果是文本(字符或者字符串)则需要用单引号括起来(大部分也支持双引号)
#### and和or
用于组合where子句的条件
`select * from Persons where (ID>2 and ID<4) or 名字='李四'`
#### order by
按照某一列对结果进行升序排序
按照id升序排序`select * from Persons order by ID`
如果想要降序使用关键字**desc** ,升序关键字**asc**(默认升序)
按照ID降序,按照名字升序`select * from Persons order by ID desc,名字 asc`

### insert into
用于在指定表格中插入一条记录
插入一条完整的记录
`insert into Persons values(20,'赵六',17,'长沙')`
如果是不完整的记录(某些信息为空)
`insert into Persons(ID,名字) value(21,'孙七')`

### update
用于修改表中的数据
**格式 `update 表名 set 列名=新值 where 条件`**
修改一行的若干列`update Persons set 年龄=17,城市='武汉' where 名字='孙七'`

### delete
用于删除表中的一条记录
**格式 `delete from 表名 where 条件`**
删除表中的一行 `delete from Persons where 名字='孙七'`
如果想要删除表中的所有行 `delete from Persons`或者`delete * from Persons`

### top子句
规定需要返回的语句的条目数
对于不同的数据库系统top子句不一定支持
* SQL Server
  `select top number|percent 列名 from 表名`

  ```sql
  -- 从表中选取最前面的两条
  select top 2 * from Persons
  
  -- 从表中选取前50%
  select top 50 PERCENT * from Persons
  ```
  
* MySQL
  `select 列名 from 表名 LIMIT number`

  ```sql
  -- 从表里面选取前5条数据
  select * from Persons LIMIT 5
  ```
  
  
  
* Oracle
`select 列名 from 表名 where ROWNUM <= number`
### like子句
用来查找指定条件的语句
选取名字为N开头的人
`select * from Persons where 名字 like 'N%'`
其中的% 用于定义通配符 表示缺少的字母,如名字以y结尾可以写成'%y',名字中包含s可以写成'%s%'

|         通配符         | 作用                       | 示例             |
| :--------------------: | :------------------------- | :--------------: |
|           %            | 替换一个或者多个字符       | `%lon%`       |
|           _            | 替换一个字符               | `_uck`          |
|        [字符表]        | 表示表中的任意一个字符     | `[lf]uck`        |
| [^字符表]或者[!字符表] | 表示不在表中的任意一个字符 | `[!123]`或者`[^123]` |

### in
允许在寻找的时候指定多个值
`select * from Persons where 名字 in ('张三','李四')`

### between
指定范围
`select * from Persons where 学号 between 102 and 103`

```SQL
SELECT * from Persons
where 学号
not between 104 AND 105
```

## DDL语句   

###  数据类型
| 名称         | 类型         | 说明                                                         |
| ------------ | ------------ | ------------------------------------------------------------ |
| int          | 整型         | 4字节整数类型,约21亿                                         |
| bigint       | 长整型       | 8字节整数类型,约922亿亿                                      |
| real         | 浮点型       | 4字节浮点数,范围约10^38                                      |
| double       | 浮点型       | 8字节浮点数,范围约10^308                                     |
| decimal(m,n) | 高精度浮小数 | 由用户指定精度的小数,<br />DECIMAL(20,10)表示一共20位，其中小数10位，通常用于财务计算 |
| char(n)      | 定长字符串   | 存储指定长度的字符串,char(100)存储长度100                    |
| varchar(n)   | 变长字符串   | 存储可变长度的字符串,varchar(n)可以存储长度0-100的字符串     |
| boolean      | 布尔类型     | 存储true或者false                                            |
| date         | 日期类型     | 存储日期 2020-1-1                                            |
| time         | 时间类型     | 存储时间  12:12:00                                           |
| datetime     | 时间日期类型 | 存储日期+时间  2020-1-1 1:0:0                                |

