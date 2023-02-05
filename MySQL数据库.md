# MySQL数据库

## 基本概念

- 数据库的英文单词:**DataBase** 简称**DB**
- 什么是数据库?
  - 用于存储和管理数据的仓库
- 数据库的特点
  - 持久化存储数据的.其实数据库就是一个文件系统
  - 方便存储和管理数据
  - 使用了同一的方式操作数据库--SQL

## MySQL的启动与关闭

启动

```mysql
net start mysql
```

关闭

```mysql
net stop mysql
```

登录

```mysql
mysql -u 用户名 -p 密码
```

退出

```mysql
quit
```

```mysql
exit
```

远程连接mysql数据库

```mysql
mysql -h 主机地址 -u 用户名 -p 密码
```

## 注释

- 单行注释

  - ```mysql
    --     #
    ```

- 多行注释:

  ```mysql
  /*  */
  ```

## 数据类型

- 整形
  - tinyint smallint medium int int bigint

# SQL

什么是SQL

Structured Query Language:结构话查询语言

## SQL分类

- DDL(Data Definittion Language)数据定义语言

  用来定义数据库对象:数据库,表,列等.关键字 : create drop alter 等

- DML(Data Manipulation Language)数据操作语言

  用来对数据中表的数据进行增删改.关键字: insert delete update等

- DQL(Data Quert Language)数据查询语言

  用来查询数据库中表的记录(数据).关键字: select where等

- DCL(Data Control Language)数据控制语言(了解)

## DDl:操作数据库表

- 操作数据库:CRUD

  - C(Create):创建

    - 创建数据库

    - ```mysql
      create database 数据库名称
      ```

  - R(Retrieve):查询

    - 查询数据库的名称

    - ```mysql
      show databases;
      ```

    - 查看某个数据库的字符集

    - ```mysql
      show carete database 数据库名称;
      ```

    - 创建并判断数据库是否存在

    - ```mysql
      create database if not  exists 数据库名称;
      ```

    - 创建并且指定字符格式

    - ```mysql
      create database 数据库库名称 character set gbk;
      ```

  - U(Update):修改

    - 修改数据库的字符集

    - ```mysql
      alert database 数据库名称 character set 字符集
      ```

  - D(Delete):删除

    - 删除数据库

      - ```mysql
        drop database 数据库名称;
        ```

    - 判断如果有这个数据库就删除

    - ```mysql
      drop database if exists 数据库名称;
      ```

  - 使用数据库

    - 查询正在使用的数据库名称

    - ```mysql
      select dataase();
      ```

    - 使用数据库

    - ```mysql
      use 数据库名称;
      ```


## 操作表

- C(Create):创建

  - 创建表

  - ```mysql
    create table 表名(
    	列名1 数据类型1,......
    );
    ```

- R(Retrieve):查询

  - 查询某个数据库中所有表的名称

  - ```mysql
    show tables;
    ```

  - 查询表结构

  - ```mysql
    desc 表名称;
    ```

- U(Update):修改

  - 修改表的名字

    - ```mysql
      alter table 表名 rename to 新的表名
      ```

  - 修改表的字符集

    - ```mysql
      alter table 表名 charcater set 字符集名称;
      ```

  - 修改列的名称 类型

  - ```mysql
    alter table 表名 change 列名 新列名 新数据类型;
    ```

  - ```mysql
    alter table 表名 modify 列名 新数据类型;
    ```

  - 添加一列

    - ```mysql
      alter table 表名 add 列名 数据类型;
      ```

  - 删除列

  - ```mysql
    alter table 表名 drop 列名;
    ```

- D(Delete):删除

  - ```mysql
    drop table 表名;
    ```

  - 判断在删除

  - ```mysql
    DROP PROCEDURE IF EXISTS xxxxxx;
    ```
    

复制表

create table 名字 like 原来的表名称

客户端图形化工具:SQLYog

##  DML:增删改表中数据

### 添加数据

- ```mysql
  insert into 表名(列名1,.列名2....) values (值1,值2...);
  ```

  - 注意事项:
  - 列名和值要一一对应
    - 如果表名后,不定义列名,则默认给所有列添加值
    - 除了数字类型,其他类型需要使用引号 单双引号都可以

### 删除数据

- ```mysql
  delete from 表名 [where 条件] 
  ```

  - 注意
    - 如果不加条件,则删除表中所有记录

- ```mysql
  truncate table 表名
  ```

  注意:

  如果不加任何条件,则会将表中所有记录全部修改

### 修改数据

```mysql
update 表名 set 列名1  = 值1,...[where 条件];
```

## DQL

### 查询表中的记录

- ```mysql
  select * from 表名;
  ```

  语法:

  `select`

  ​		字段列表

  `from`

  ​		表名列表

  `where`

  ​		条件列表

  `group by`

  ​		分组字段

  `having`

  ​		分组之后的条件

  `order`

  ​		排序

  `limit `

  ​		分页限定

  ##### 基础查询

  多个字段的查询

  - ```mysql
    select 字段1,字段2...from 表名
    ```

  去除重复

  ```mysql
  distinct
  ```

  计算列

  ```mysql
  ifnull(表达式1,表达式2)
  ```

  起别名

  ```mysql
  as
  ```

  in关键字
  
  ```mysql
  select * from 表名 where in(条件);
  ```
  
  条件查询
  
  - where子句后跟条件
  
  - 运算符
  
    - ```
      > < <= >= = <>
      between ... and
      in(集合)
      like : 模糊查询
      	占位符
      	*_:单个任意字符
      	*%:多个任意字符
      is null
      and 或 &&
      or  或 ||
      not 或 !
      
      ```
  
      

### 查询语句的使用

- 排序查询
  - 语法 order by 子句
    - order by 排序字段 排序方式....;
    - 排序方式:
      - 升序
        - ASC:升序,默认的
        - DESC:降低顺序
  - 注意:如果优多个排序条件,则当前的条件值一样时,才会判断第二条件
- 聚合函数 将一列数据作为一个整体 ,进行纵向的计算
  - count:计算个数
  - max:计算最大值
  - min:计算最小值
  - sum:求和
  - avg:计算平均值
- 分组查询
  -  语法 group by 分组字段; 
  -  having的区别
     -  where在分组之前进行限定
     -  where后不能跟聚合函数,having后可以跟
- 分页查询
  - 语法:limit 开始的索引 每页查询的条数
  - 公式:开始的索引 = (当前的页码 - 1 ) * 每页显示的条数

约束

概念:对表中的数据进行限定,保证数据的正确性,有时效性和完整性

分类:

1. 主键约束：primary key

   注意：含义 非空且唯一

   一张表只能有一个子段为主键

   主键就是表中记录的唯一标识

   1. 添加主键约束

      ```mysql
      CREATE TABLE stu
      (
      id INT PRIMARY KEY,
      num VARCHAR(11) 
      );
      ```

      ```mysql
      alter table 表名 add primary key(列名 ....);
      ```

   2. 删除主键

      ```mysql
      alter table 表名 drop primary key;
      ```

   3. 修改主键

      ```mysql
      alter table 表名 modify 列名 数据类型 primary key
      ```

      自动增长 auto_increment

      ```mysql
      CREATE TABLE stu
      (
      id INT PRIMARY KEY AUTO_INCREMENT,
      num VARCHAR(11) 
      );
      ```

      删除自动增长

      ```mysql
      alter table stu modify 列名 类型;
      ```

      添加自动增长

      ```mysql
      alter table stu modify 列名 类型 AUTO_INCREMENT；
      ```

      

2. 非空约束：not null

   1. 创建时添加非空约束

      ```mysql
      create table stu(
      id int,
      name varchar (20) not null
      );
      ```

   2. 创建表后，添加非空约束

      ```mysql
      alter table 表名 modify 名字 数据类型 not null
      ```

   3. 删除非空约束

      ```mysql
      alter table 表名 modify 名字 数据类型；
      ```

3. 唯一约束：unique

   1. 创建时添加唯一约束

      ```mysql
      CREATE TABLE stu
      (
      id INT, 
      num VARCHAR(11) UNIQUE
      );
      ```

      ```mysql
      alter table 表名 add unique [索引名](列名 ....);
      ```

   2. 删除唯一约束

      ```mysql
      alter table 表名 drop index 列的唯一约束的名字
      ```

   3. 在创建表后添加唯一约束

      ```mysql
      alter table 表名 modify 添加列的名字 类型 unique；
      ```

      

4. 外键约束： foreign key

   ​	在创建表示，可以添加外键

   语法 create table 表名（....

   外键列

   constraint 外键名称 foreign key 外键列的名称 references 主表名称（主表列的名称）

   ）;

   1. 删除外键

      ```mysql
      alter table 表名 drop foreign key 外键名字；
      ```

   2. 添加外键

      ```mysql
      alter table 表名 add constraint 外键名 （关联的外键） references 主表名称（主表列名称）
      ```

级联更新

```mysql
on ipdate cascade
```

级联删除

```mysql
ondelete cascade
```

多表之间的关系

范式

数据库库的备份还原

### 去除重复

```sql
SELECT DISTINCT 字段名 FROM 表名
```

### 查询系统版本

```sql
SELECT VERSION()
```

## 数据库的设计

多表之间的关系

​	一对一

​	一对多

​	多对多

数据库设计的范式

概念：设计数据库时，需要遵循数据库的观念

分类：

第一范式1nf

第二范式2nf

第三范式3nf

## 数据库的备份和还原

命令行

语法：mysqldump -u用户名 -p密码 >保存的路径

**还原数据库**

- 登录数据库
- 创建数据库
- 使用数据库
- 执行 

图形化工具

备份 执行

## 多表查询

查询语法：

```mysql
select 
	列表名称
from
	列表名称
where....
```

**笛卡尔积：**

有两个集合A，B取这两个集合的所有组合情况

多表查询的分类：

- 内连接查询
  - 隐式内连接
    
    - 语法
    
      ```
      使用where条件
      ```
    
  - 显式内连接
  
    - 语法：
  
    ```
    select 字段列表 from 表名1 inner join 表名2 on 条件
    ```
- 外连接查询
  - 左外连接
    - 语法：
    
      ```
      select 字段列表 from 表1 left outer ioin 表2 on 条件
      ```
    
    - 查询的是左表所有的数据以及交际部分
  - 右外连接
    - 语法：
    
      ```
      select 字段列表 from 表1 right outer ioin 表2 on 条件
      ```
    
    - 查询的是右表所有的数据以及交际部分
- 子查询
  - 概述：查询中嵌套查询
  - 子查询的结果是单行单列的、
    - 子查询可以作为条件，使用运算符取判断
  - 子查询的结果是多行单列的
    - 子查询可以作为条件，使用运算符in来判断
  - 子查询的结果是多行多列的

## 事务

事务基本介绍

​	概念：如果包含多个步骤的业务操作，被事务管理，要么同时成功，要么同时失败

​	操作：

​		开启事务：start transaction

​		回滚：rollback

​		提交：commit

mysql数据库中事务默认自动提交

​	一条 DML语句会自动提交一次事务

  查看事务的默认提交方式：select @@autocommit 1代表自动提交 0代表手动提交

修改默认提交方式：set @@autocommit = 0

事务的四大特征：

- 原子性：是不可分割的最小操作单位，要么同时成功，要么同时失败
- 持久性：当事务提交或回滚后，数据库会出持久的保存的数据
- 隔离性：多个事务之间，相互独立 
- 一致性：事务操作前后，数据总量不变

事务的隔离级别

​	read uncommitted 读未提交

​	read committed 读已经提交

​	repeatable read 可重复读

​	serializable 串行化

数据库查询隔离级别

```mysql
select @@t_isolation
```

 数据库设置隔离级别

```mysql
set global transaction isolation level 级别字符串
```

## DCL

管理用户，授权

DBA：数据库管理员

- 管理用户

  - 添加用户：CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
  - 删除：drop ‘用户名’ @ ‘主机名’；
  - 修改用户的密码：updata user set password = password （‘新密码’）where user = ‘用户名’；
  - set password for ‘用户名’@ ‘主机名’  = password（‘新密码’）；

  - 查询用户：select * from user；

- 授权

  - 查询权限 show grants for ‘ 用户名’ @‘ 主机名’；

  - 授予权限 grant 权限列表 on数据库.表名 to‘用户名’@ ‘主机名’

  - 撤销权限：revoke 权限列表 on数据库名.表名 from ‘用户名’@ ‘ 主机名’


## 视图

- 创建视图

  ```mysql
  create view 视图名;
  ```

- 查看视图

  ```mysql
  select * from 视图名;
  ```

- 删除视图

  ```mysql
  drop view 视图名;
  ```

- 更新视图

  ```mysql
  alter view 
  ```

## 索引

**作用:提高查询速率**

**索引是帮助Mysql高效查询数据结构**

### 分类

- 普通索引

  ```mysql
  index
  ```

- 唯一索引

  ```mysql
  unique
  ```

- 主键 :也是一种唯一索引

- 全文索引

  ```mysql
  fulltext
  ```

### 创建索引

```mysql
create {index,unique,fulltext} index 索引名字 on 表格名字(字段)
```

### 添加索引

```mysql
alter table 表格名字 add 索引类型 索引名字(字段)
```

### 删除索引

```mysql
drop 索引类型 [索引名字] ON 表格
```

```mysql
alter table 表 drop 索引类型 索引名字
```

## 触发器

格式:

```mysql
create trigger 触发器名 触发时间 触发事件 on 表名 for each row 触发动作
```

触发时间: before after

触发事件: insert  updata delete

更改结束符:delimiter $$;

## 函数

- 数学函数

  - 绝对值

    ```
    abs()
    ```

  - 圆周率

    ```
    pi()
    ```

  - 平方根

    ```
    sqrt()
    ```

  - 求余数

    ```
    mod(x,y)
    ```

  - 获取整数

    ```
    ceil()
    ```

  - 获取随机数

    ```
    rand()
    ```

  - 四舍五入

    ```
    round()
    ```

  - 幂函数

    ```
    pow(x,y)
    ```

  - 平均值
  
    ```
    AVG()
    ```
  
  - 计数
  
    ```
    COUNT()
    ```
  
  - 求和
  
    ```
    SUM()
    ```
  
  - 最大值
  
    ```
    MAX()
    ```
  
  - 最小值
  
    ```
    MIN()
    ```
  
    