## 1.初识Mysql

javaEE：企业级java开发 WEB

前端(页面：展示，数据！)

后台（连接点：连接数据库jdbc，连接前端（控制试图跳转，给前端传递数据）

数据库(存数据，Txt，Excel，word)

```java
只会写代码，学好数据库，基本混饭吃；
操作系统，数据结构与算法！ 当一个不错的程序员
离散数学，数字电路，体系结构，编译原理 + 实战经验 高级程序员优秀

```

### 1.1为什么学习数据库

1、岗位需求

2、现在的世界，大数据时代

3、被迫需求：存数据

4、数据库时所有软件体系中最核心的存在 DBA



### 1.2、什么是数据库

数据库(DB,DataBase)

概念：数据仓库，软件，安装在操作系统上，可以存储大量工具的数据仓库软件

作用：存储数据，管理数据



### 1.3、数据库分类

关系型数据库：行、列 

​	Mysql,Oracle,sql Server,DB2,postgres sql

​	通过表和表之间，行和列之间的关系进行数据的存储



非关系型数据库: （no sql）not only sql

​	Redis,MongoDB

​	非关系型数据库，以对象存储，通过对象的自身属性来决定





DBMS(数据库管理系统)

​	数据库的管理软件，科学有效的管理我们的数据

​	Mysql 是关系型数据库管理系统 是最好的RDBMS



### 1.4、Mysql简介

MySQL是一个关系型数据库管理系统

现属于RDBMS

开源的数据库软件~

体积小、速度快、总体拥有低成本，招人成本较低，所有人必须会

中小型网站或者大型网站集群







## 2.操作数据库

**操作数据库**  >  **操作数据库中的表** > **操作数据库中表的数据**

### 2.1 操作数据库

1、创建数据库

```mysql
CREATE DATABASE if not EXIST westos;
```

2、删除数据库

```mysql
DROP DATABASE if not EXIST westos;
```

3、使用数据库

```mysql
USE 'school'
```

4、查看数据库

```mysql
SHOW DATABASE
```



### 2.2 数据库的列类型

>数值

​	tinyint 十分小的字节 一个字节

​	smallint 较小的字节  两个字节

​	mediumint 中间字节 三个字节

​	int  		标准的整数  四个字节

​	bigint 	较大的数据	8个字节

​	float 	浮点数		4个字节

​	double	高精度浮点数 	8个字节 精度问题

​	decimal   字符串形式的浮点数	金融计算的时候，一般是使用decimal

> 字符串

​	char	字符串	0~255

​	varchar	可变字符串	0~65535  对应String

​	tinytext	微型文本		2^8-1

​	text		文本串		2^16 -1

> 时间日期

​	Date 	YYY--MM--DD 	日期类型\

​	time 	HH:mm:ss		时间类型

​	datetime	时间日期类型	  最常用的

​	timestamp	时间戳	1970.1.1到现在的毫秒数

​	

> null

​	没有值，未知

​	==不要使用==



### 2.3、数据库的字段属性

Unsigned:

​	无符号的整数

​	声明了改列不能为负数



zerofill

 - 0填充
 - 不足的位数使用0来填补 int（3） ， 5---- 005



自增

- 通常理解为自增，自动在上一条记录的基础上+1（默认）
- 通常用来设计唯一的主键，必须是整数类型
- 可以自定义设计主键自增的起始值和步长



非控 Null not Null

- 假设设置为not null，不给值就是报错
- null 如果不填写值 ，默认就是null

默认

- 设置默认值
- 如果不填 默认就是默认值



**创建表的时候 表名字 和字段尽量用`` 飘号 扩起来**



#### 数据库的引擎



INNODB ： mysql 默认使用的

MYISAM：  早些年使用的

![1](C:\Users\Administrator\Desktop\学习图片\1.png)

常规使用操作：

- MYISAM ：节约空间速度较快
- INNODB： 安全性高，事务的处理，多表多用户操作



Mysql 引擎在物理文件上的区别

- InnoDB在数据库表中只有*fmr的文件
- MYISAM 对应文件
  - *.frm -表结构的定义文件
  - *.MYD 数据文件
  - *.MYI 索引文件



修改表

```mysql
ALTER TABLE teacher RENAME AS teacher1  #修改表的名称

ALTER TABLE teacher ADD age INT (11) #增加字段

ALTER TABLE teacher MODIFY age varchar(12) #修改字段约束

ALTER TABLE teacher CHANGE age age1 int(1) #修改字段名

ALTER TABLE teacher DROP age;
```



## Mysql数据管理

#### 3.1 、外键





#### 3.2、DML语言(全部记住)

数据库意义:数据存储，数据管理

DML语言 ： 数据库操作语言

- insert
- update
- delete
- TRUNCATE + 表名 清空表

#### auto_increment 自增







## 4.DQL 查询数据

#### 4.1、DQL 

Data Query LANGUAGE ：数据查询语言

- 所有查询操作都用它 Select
- 简单的查询，复杂的



#### 4.2、查询语句

```mysql
select @@auto_increment_increment  ---查询自增的步长
```

