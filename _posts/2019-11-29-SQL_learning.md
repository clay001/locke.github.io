---
layout: post
title: "SQL learning"
date: 2019-11-29 13:57:14
image: '/assets/img/'
description: 'SQL learning note'
tags:
- SQL
categories:
- Language
twitter_text: 'Do you know these?'
---

## Everyday sentence 

11-29: I don't like rasins. They used to be fat and jucy, and now they are twisted. They had their lives stolen. They taste sweet, but really they are humiliated grapes.

12-1: We all fear death and question our place in the universe. The artist's job is not to succumb to despair, but to find an antidote for the emptiness of existence.

12-2: You know the only thing that has made the whole thing worthwhile...has been those... few times that I've been able to really, truly connect with another human being.

12-3: We are made of dreams, and dreams are made of us.

12-5: Funny, how just when you think life can't possibly get any worse it suddenly does.

12-6: 美丽的梭罗河/ 我为你歌唱 / 你的光荣历史 / 我永远记在心上 / 旱季来临 / 你轻轻流淌 / 雨季时波涛滚滚 / 你流向远方

## SQL

SQL是用于访问和处理数据库的标准的计算机语言，常见的数据库有：MySQL, SQL server, Access, Oracle, Sybase, DB2

https://www.runoob.com/sql/sql-tutorial.html

https://www.zhihu.com/search?type=content&q=SQL

## 数据库基础知识

https://blog.csdn.net/yutianzuijin/article/details/12243751

## Oracle数据库

是目前世界上流行的关系数据库管理系统，一个基本任务是存储数据。物理存储结构是存储数据的纯文件，当CREATE DATABASE语句来创建一个新的数据库时，将创建数据文件，控制文件和联机重做日志文件。

逻辑存储结构使用逻辑存储结构对磁盘空间使用情况进行精细控制。包括数据块，范围，段（分配用于存储用户对象的一组范围），表空间

## 数据库事务的四大特性

1.原子性  2.一致性 3. 隔离性  4.持久性

脏读是指在一个事务处理的过程里读取了另一个未提交的事务中的数据，事务的修改未提交的情况下另一个并发的事务来访问的不一致情况

不可重复读是读取了前一个事务提交的数据

幻读是事务非独立执行时发生的一种现象，比如事务1对一个表中的某项数据进行修改后，事务2又对这个表进行了插入数据行（仍保留原数据修改前的列），这时候操作事务1的用户查看时就会发现有一行没有修改

MYSQL提供了四种隔离级别：

1. Serialization（串行化）：可避免脏读，不可重复读，幻读
2. *默认Repeated read（可重复读）：避免脏读，不可重复读
3. Read commited（读已提交）：避免脏读
4. Read uncommitted（读未提交）

## SOCKET（套接字）

两个跨计算机的进程要进行通讯的话需要通过网络对接起来，比如服务器程序需要绑定在本机的某个端口号上，套接字就是指代承载着走通讯的系统资源的标识。处于应用层和传输层之间

## 数据库查找

学生成绩离两门成绩大于80的学生名字

```sql
Select S.name 
From Student S
GROUP BY S.name
Having MIN(S.score)>= 80 and count(*)>=2
```

## 关系型数据库

- Oracle、DB2、Microsoft SQL Server、Microsoft Access、MySQL
- 表（Relationship），列（Attribute）被称为字段，行（Tuple）被称为记录
- 优点：事务一致性，复杂查询，容易理解，使用方便，易于维护
- 缺点：读写性能（容易死锁），表结构更新，高并发(硬盘IO问题)，海量数据

## 非关系型数据库 NOSQL(Not Only SQL)

- NOSQL特点：

- - 易扩展，数据之间没有关系的
  - 大数据量，高性能。高性能读写非常灵活的
  - 灵活的数据模型。不需要事先对存储数据建立字段
  - 存储格式多，分布式存储成本低廉

- NOSQL主要主流产品

- - Redis、CouchDB、mongoDB、Cassandra。NOSQL中比较火的三个数据库Redis、Memchache、MongoDb。

思想：以键值对存储，结构不固定，每个元组可以有不一样的字段。可以用来做缓存服务器

## 基本的概念

excel和数据库就像移动硬盘和网盘，一张表有列名和记录数据的行，唯一的列属性称为主键，表之间通过列建立联结，数据库管理系统是来管理的软件，SQL是操纵数据库的工具

navicat是mysql的客户端

字符串：char，text，blob（二进制形式的文本数据）

数字：整型，浮点型，decimal（更高精度）

日期：date，datetime（日期加时间），timestamp（时间戳），time，year

## 基本操作指令

insert into <表名>(<列名1>,<列名2>,.....) vaules(<值1>,<值2>,.....) ;

DDL（数据库定义语言）：create, drop, alter

DML（数据操纵语言）: insert, delete, select, update

DCL（数据控制语言）: commit, rollback, crant

英文分号结尾，不区分大小写，输入法要是英文的

## 查询

Select <列名1>, <列名2>, ......

from <表名>;

as用于为列设置别名

distinct用于删除重复的值

列名不能加单引号

查询条件：where 姓名 = "xxx"; 

注释：-- 单行注释， /*  xxxx    */多行注释

运算符：算术运算符（所有与空值进行运算的结果仍为空值）， 比较运算符， 逻辑运算符（not, and, between, or, in）

模糊查询：like   

```sql
select *
from student 
where 姓名 like '李%'   /*以李开头       
%李    以李结尾
%李%   带李
```

王_, _表示任意1个字符



## 实战经验

select相当于一个建表的操作，ifnull函数里的第一个参数可以是一个括号括起来的select语句。

函数的格式是Create function name（参数名字 参数类型）returns 参数类型。里面有begin和end，值设定语句要写在return外面，SQL语句写在return里面，语句结束都要有分号

select里面还可以套select来得到新列的内容

自连接（自身连接）的本质是把一张表复制出多张一模一样的表来使用





