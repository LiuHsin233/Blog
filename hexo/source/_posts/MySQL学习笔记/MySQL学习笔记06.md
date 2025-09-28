---
title: MySQL学习笔记06_DDL语句
date: 2022-01-14 14:09:31
tags: [MySQL]
toc: true
---

# create table

```sql
-- 基础格式
/*
create table if not exists 表名(
	列1 类型1,
	列2 类型2,
	列3 类型3 约束1 约束2 约束3 ...., -- 附带约束
	...
)
*/

create table if not exists Persons(
    ID int,
    姓名 varchar(20),
    年龄 tinyint,
    城市 varchar(20)
)
```

## 约束

>约束即为表中数据的限制条件,目的是为了确保表中的记录完整有效,可以分为表级约束和列级约束(针对某一个字段)
>
>表级约束 对多个数据列建立的约束,只能在列定后声明
>
>列级约束 对单个数据列建立的约束,可以在列定义的时候声明,也可以在列定义后声明

### 非空约束 not null

>用not null 约束的字段不能为null值,必须给定具体的数据(插入数据的时候不指定值会报错)

```sql
-- 格式 字段名 数据类型 not null
create table if not exists Persons(
    ID int,
    姓名 varchar(20) not null, -- 非空约束
    年龄 tinyint,
    城市 varchar(20)
)
```

#### 唯一性约束 unique

> 用unique 约束的字段具有唯一性,不可以重复,可以为null

```sql
create table if not exists User(
    ID int,
    name varchar(20),
    age tinyint,
    city varchar(20),
    email varchar(20) unique, -- 唯一约束,邮箱不可以重复,插入重复的会报错
)

create table if not exists User(
    ID int,
    name varchar(20),
    age tinyint,
    city varchar(20),
    email varchar(20),
    phone varchar(20),
    unique(email,phone) -- 联合约束,两个或者两个以上的字段和另外一个记录相同则报错,一个手机号两个不同的邮箱可以
)

phone varchar(20) not null unique -- 非空 不能重复
```

### 主键约束 primary key

>为了便于快速查找表中的数据,一般会在表中设定一个主键
> - 每个表只能定义一个主键
> - 主键作为每一列的唯一标识,不可为null也不能重复
> - 可以设置表中的一个字段为主键,也可以设定多个字段为主键(联合主键)
> - 使用多个字段为主键的时候,需要遵循最小化原则(字段尽可能少且不重复)

```sql
-- 格式 字段名 数据类型 primary key
-- 或者在定义所有字段之后单独指定主键  constraint 约束名 primary key(字段名)

create table if not exists User(
    ID int primary key, -- 定义的时候设定主键
    name varchar(20),
    age tinyint,
    city varchar(20),
    email varchar(20),
    phone varchar(20)
)

create table if not exists User(
    ID int,
    name varchar(20),
    age tinyint,
    city varchar(20),
    email varchar(20),
    phone varchar(20),
    primary key(name),-- 定义之后设定主键,如果是联合主键的话就在这里列出来
    -- constraint pri_key primary key(ID) -- 这种是给约束起个别名后续方便操作
)

-- 创建表后设定主键(注意表里面这个字段不能有null值)
-- alter table 表名 add primary key(字段名)

-- 删除主键
-- alter table 表名 drop primary key

-- 当主键定义为自动增长之后,这个主键的值就不在需要用户输入,每增长一条记录,主键会自动进行增长
-- 给字段添加auto_increment属性来实现自动增长
-- ID int primary key auto_increment

-- auto_increment 
-- 默认初始值为1,每次加新记录,字段值自动加1
-- 插入的第一条数据如果赋了初始值,那么就从这个初始值开始
-- 约束的字段只能是整数类型,且必须具备not null属性
-- 如果超过字段数据类型的上限,auto_increment会失效
-- 一个表中只能有一个字段使用auto_increment约束,且该字段必须有唯一索引(主键或者主键的一部分)
```

###  外键约束 foreign key

> 外键约束用于建立主表和从表的关联关系,约束两个表中数据的一致性和完整性
> 主表删除某条记录的时候,从表与之对应的记录也应该有相应的变化
> 一个表可以有一个或者多个外键,外键不可以为空值

| 学号 | 姓名 | 班级 | 年龄 | 联系方式 | 班主任 | 班主任联系方式 |
| :--- | :--- | :--- | :--- | :------- | :----- | -------------- |

上面这个学生表中,不难注意到,通过班级就可以确定班主任和班主任的联系方式,如果不进行拆分,会产生很多*数据冗余*,所以从上面这个表中只留下一个班级,另外加一个新的表来存放班主任的信息

| 学号 | 姓名 | 班级 | 年龄 | 联系方式 |
| :--- | :--- | :--- | :--- | :------- |

| 班级 | 班主任 | 班主任联系方式 |
| :--- | :----- | :------------- |

拆分出学生表和班主任两个表,通过学生的班级这个字段,可以从班主任表中取到对应的班主任数据.
```sql
-- 外键格式
-- foreign key (字段名) references <主表名> (主键列名)

-- 创建学生表
create table if not exists students(
    ID int primary key,
    name varchar(20),
    class int,
    age tinyint,
    phone varchar(20)
)

-- 创建班主任表
create table if not exists class(
    classId int primary key,
	htname varchar(20), 
    phone varchar(20),
    foreign key (classId) references students(class) -- 表示class表中的classId字段依赖于student表中的class字段
)

-- 如果创建表之后在添加外键,那么可以使用alter table
alter table class add foregin key (classId) references student(class)

-- 删除外键
-- 使用constraint给外键取别名的话,后续删除会简单一点
alter table class add constraint classForStudent foregin key (classId) references student(class)
-- 上面的外键名字叫做classForStudent 那么后续删除的时候可以
alter table class drop foregin key classForStudent

-- 如果创建的时候没有取别名,那么使用show create table来查看这个表结构
-- 找到mysql随机给外键取的别名之后再操作
-- show create table class

/*
注意事项:
1. 创建数据表的时候,先创建主表,然后创建子表
2. 添加数据的时候先向主表中添加数据,然后向子表中添加记录,删除顺序相反
3. 修改数据一般通过触发器来实现
*/
```

### 检查约束 check

```sql
-- 检查约束用于限制数据
-- 字段名 类型 check <表达式>

create table if not exists student(
   ID int primary key,
   age int check(age>0 and age <150) -- 如果插入的数据不满足条件会插入失败
)

-- check约束可以放定义字段后面也可以定义之后再创建
create table if not exists student(
	ID int primary key,
    age int,
    constrain ageLimit check(age > 0 and age <150) -- 这里起了一个别名叫做ageLimit
)

-- 定义之后用alter atble 也可以
alter table student add constrain ageLimit check ( age > 0)
alter table student drop constraint ageLimit
```

### 默认约束 default

```sql
-- 如果没有规定其他的值,那么会将默认值添加到所有的新纪录
-- 字段名 类型 default 默认值
create table if not exists student(
   ID int primary key,
   age int,
   city varchar(50) default 'wuhan' -- 插入的新数据如果没有city字段那么使用默认值填充
)

-- 创建表之后添加default约束
alter table student alter city set default 'wuhan'

-- 撤销default约束
alter table student alter city drop default
```

### 自动增长 auto_increment

```sql
create table if not exists student(
	id int primary key auto_increment, -- 默认从1开始,每次插入一条数据自动+1
    name varchar(20) not null,
)
```

# 查看数据表的结构

## describe

```sql
-- describe/desc 用来查看表的字段信息
describe 表名
desc 表名
```

| Field | Type | Null | Key  | Default | Extra |
| :---- | :--- | :--- | :--- | :------ | :---- |

>Null 表示该列是否可以存储NULL值
>Key 表示该列是否有索引 PRI表示该列是主键的一部分,UNI表示该列是UNIQUE索引的一部分,MUL表示某个给定值允许出现多次
>Default 表示该列是否有默认值
>Extra 表示可以获取到给定列的附加信息,比如auto_increment

# 修改表的结构

## 修改表名
```sql
alter table 旧表名 rename 新表名
```

## 修改数据类型

```sql
alter table 表名 modify 字段名 新类型
```

## 修改字段名

```sql
alter table 表名 change 旧字段名 新字段名 新数据类型
```

## 添加字段

```sql
alter table 表名 add 新字段名 数据类型
```

## 删除字段

```sql
alter table 表名 drop 字段名
```

