---
title: MySQL学习笔记
tags: [MySQL]
categories: MySQL
top: true
---
数据的安装和远程连接，请访问如下：
[https://blog.csdn.net/qq_43630810/article/details/104287280](https://blog.csdn.net/qq_43630810/article/details/104287280)
### 一、MySQL命令
#### 1、MySQL操作
##### 1.1、启动和停止服务操作
在命令行输入：
```
service mysql start  //开始mysql服务
service mysql stop   //停止mysql服务
service mysql restart  //重新启动mysql服务
```
##### 1.2、查看MySQL服务
在命令行输入：`ps -e|grep mysql`
##### 1.3、登录mysql数据库
在命令行输入：`mysql -u root -p`
#### 2、MySQL数据库操作
mysql数据库操作与sql语句(对大小写不敏感)
##### 2.1、显示已经存在的数据库
```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.05 sec)
```
##### 2.2、创建一个新的数据库
命令格式：create database 数据库的名字（DB_dbname）
```
mysql> create database db_test;  //db_test为数据库的名字
Query OK, 1 row affected (0.00 sec)
```

##### 2.3、使用指定的数据库
命令格式:use 查看的数据名
```
mysql> use db_test;  //db_test为查看的数据库名
Database changed
```
##### 2.4、查看数据库中的表
命令格式：show tables;
```
mysql> show tables;
Empty set
```
##### 2.5、==创建数据库表==
在此说明数据记录的属性：
>关键概念：
>>字段名：表格的列名
>>>数据类型：该列数据的存储类型（主要有数据类型、时间日期类型和字符串类型）

数据类型 | 字节数(byte)
---|---
int| 4
float| 4
tinyint|1
Bigint|8
double|8
>注:int和double比较重要

时间日期类型|格式|范围
---|---|---
date|YYYY-MM-DD|1000-01-01 ~ 9999-12-31
TIME|HH:MM:SS   | -838:59:59 ~ 838:59:59
YEAR|YYYY        |1901-2155
DATETIME|YYYY-MM-DD |HH:MM:SS
>注:date和time比较重要

字符串类型|范围(byte)|名称
---|---|---
varchar|0-65535|变长字符串
text|0-65535|长文本数据
longtext|0-4294967295|极大文本数据
>注:varchar比较重要

命令格式：create table 表名 (字段名1 数据类型, 字段名2 数据类型... 字段名n 数据类型);
```
mysql> create table student(id int,name varchar(20)); //创建表名为student
Query OK, 0 rows affected (0.03 sec)
```
创建表格时实现唯一性约束:
create table 表名 (字段名1 数据类型 not NULL, 字段名2 数据类型... 字段名n 数据类型,UNIQUE (字段名1)); //not NULL非空约束，UNIQUE设置唯一
例如：
`create table student_1(id int not NULL,name varchar(50),UNIQUE (id));`

##### 2.6、向表中插入数据
查看表结构：desccribe 表名;或者desc 表名;
插入数据的语法格式： insert into 表名 values(value1, value2,..valuen);
```
mysql> desc student;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.04 sec)
mysql> insert into student values(1,'xiaoming');
Query OK, 1 row affected (0.01 sec)
```
##### 2.7、查询表中的记录
语法格式：select 字段1，字段2 ..字段n from 表名 [where Clause] [Limit N];
```
mysql> select * from student;   
mysql> select id from student;
mysql> select * from student where id = 1;
mysql> select id 学号 from student;  //别名
mysql> select id '学号' from student;
```
##### 2.8、删除操作
- 删除记录:`delete from 表名 where 条件;`

- 删除表:`drop table 表名;`

- 删除数据库:`drop database 数据库名`

```
mysql> delete from student where id=2; //删除id为2
Query OK, 1 row affected (0.01 sec)
```
##### 2.9、更新表中的记录
命令格式： update 表名 set 字段=值，字段=值 where 条件;
```
mysql> update student set id =2 where id=1; //修改id为1的修改为2
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
##### 2.9、==中文乱码问题==
首先查看数据库编码：`show variables like 'char%';`
改成utf8格式
```
set charactor_set_database=utf8;
set character_set_server=utf8;
alter database 数据库名 default character set utf8 collate utf8_general_ci;
```
>注：想要实现中文不乱码，输入以上三行，重新建立表格，而之前的表格是无法再改为中文的。

##### 2.10、过滤重复
在查询语句中使用distinct关键字来过滤重复的行。
命令格式：select distinct * from 表名;

### 二、SQL约束
用于规定数据表中的数据使用规则。如果存在违反约束规则，数据行为就会被约束终止
#### 2.1、约束条件
##### 1.1.1、NOT NULL 非空约束 规定该数据段不能为空 
- 创建时候的非空约束
`CREATE TABLE Student(ID int not NULL, Name varchar(50) not NULL, Age int);`

1. 为表中的Age字段添加非空约束
`ALTER TABLE Student MODIFY Age int NOT NULL;`

2. 删除表中的Age字段的非空约束
`ALTER TABLE Student MODIFY Age int NULL;`

##### 1.1.2、UNIQUE 保证某列的每行必须有唯一的值
- 创建时候的唯一约束
`CREATE TABLE Student( ID int NOT NULL, Name varchar(50) NOT NULL, Age int,UNIQUE (ID));`

1. 一个字段的唯一约束：
- 删除表中ID字段的唯一约束
`ALTER TABLE Student DROP INDEX ID;`

- 添加表中ID字段的唯一约束
`ALTER TABLE Student ADD UNIQUE (ID);`

2. 多个字段的唯一约束：
- 添加表中ID和Name字段的唯一约束
`ALTER TABLE Student ADD CONSTRAINT StuID UNIQUE (ID,Name);`
- 删除表中ID和Name字段的唯一约束
`ALTER TABLE Student DROP INDEX StuID ;`

>注：如果设置了两个字段都是非空约束和唯一约束，则相当于这两个字段都是主键，则其中第二个字段的设置就失效了。

##### 1.1.3、PRIMARY KEY主键约束  
实际上可以理解为UNIQUE和NOT NULL 的结合
>1. 唯一的标准数据库中的每一条记录
>2. 主键必须包含唯一的值
>3. 主键列中不能有包含NULL的值
>4. 每个表都应该有一个主键，并且每一个表只能有一个主键

1. 创建表时添加主键：
`create table Student( ID int NOT NULL, Name varchar(50) NOT NULL, Age int, PRIMARY KEY (ID));`

2. 当表已经创建时，再设置主键约束

- 删除主键:
`ALTER TABLE Student DROP PRIMARY KEY;`

- 添加主键:
`ALTER TABLE Student ADD PRIMARY KEY (ID);`

##### 1.1.4、FOREIGN KEY 外键约束
保证一个表中的数据匹配另一个表中的值的参照完整性,
一个表中外键指向了另一个表中的主键（唯一约束）
>外键的优势:
>- 外键约束预防破坏表与表之间的行为
>- 也能防止非法数据的插入，因为外键中的内容是指向表中的值之一

1. 删除表中的外键约束:
`ALTER TABLE Orders DROP FOREIGN KEY fk_Orders;`

2. 撤销数据库中所有表的外键约束(不常用):`SET FOREIGN_KEY_CHECKS=0;`之前建立的表的外键约束都无发修改了，之后的设置都可以撤销了外键约束

3. 添加表中的外键约束: `ALTER TABLE Orders ADD CONSTRAINT fk_Orders FOREIGN KEY (S_id) REFERENCES Student(ID);`

### 三、多表联合查询
![连接方式](https://note.youdao.com/yws/api/personal/file/72495A09A9DC4A2CB6D4420033C87349?method=download&shareKey=41d7ec19f04106360487640d4705d12d)

首先建立两个表：
建立两个表:
表1 tcount_tbl(网站点击次数) :`create table tcount_tbl(id int,website varcahr(20));`

website | count
---|---
baidu |26
bilibili| 35
bilibili| 35
github |10

表2 info_tbl(网站上教授的内容) :`create table info_tbl(id int,title varcahr(20),website  varcahr(20));`

id  |  title | website 
---|---|---
1|c++ | baidu 
2|Linux| bilibili
3|C |bilibili 
4|python|github 
5|java |Google

1. 内连接：查询两个表中相交的内容

需要连接两张表进行联合查询，读取info_tbl表中所有website字段在tcount_tbl表中对应的count字段值，将info_tbl 作为a， tcount_tbl作为b
```
mysql> SELECT a.id,a.website,b.count FROM info_tbl a INNER JOIN tcount_tbl b ON a.website = b.websit;
+----+----------+-------+
| id | website  | count |
+----+----------+-------+
|  1 | baidu    |    26 |
|  2 | bilibili |    35 |
|  3 | bilibili |    35 |
|  4 | github   |    10 |
+----+----------+-------+
4 rows in set (0.05 sec)
```
2. 左连接
会读取a表中的所有内容，即使b表没有对应数据
```
mysql> SELECT a.id,a.website,b.count  FROM info_tbl a LEFT JOIN tcount_tbl b ON a.website = b.websit;
+----+----------+-------+
| id | website  | count |
+----+----------+-------+
|  1 | baidu    |    26 |
|  2 | bilibili |    35 |
|  3 | bilibili |    35 |
|  4 | github   |    10 |
|  5 | Google   | NULL  |
+----+----------+-------+
5 rows in set (0.03 sec)
```
3. 右连接
会读取b表中的所有内容，即使a表中没有对应数据
```
mysql> SELECT a.id,a.website,b.count  FROM info_tbl a RIGHT JOIN tcount_tbl b ON a.website = b.websit;
+------+----------+-------+
| id   | website  | count |
+------+----------+-------+
|    1 | baidu    |    26 |
|    2 | bilibili |    35 |
|    3 | bilibili |    35 |
| NULL | NULL     |    16 |
|    4 | github   |    10 |
+------+----------+-------+
5 rows in set (0.05 sec)
```





















