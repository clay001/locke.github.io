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

Ps.近期又了解到一个NOSQL图形数据库Neo4j, 它具有高性能，轻量级，嵌入式，基于磁盘等特点。

## 基本的概念

excel和数据库就像移动硬盘和网盘，一张表有列名和记录数据的行，唯一的列属性称为主键，表之间通过列建立联结，数据库管理系统是来管理的软件，SQL是操纵数据库的工具

navicat是mysql的客户端

字符串：char，text，blob（二进制形式的文本数据）

（varchar是可变长度的字符串，其他两个字符串还有tiny,medium和long的版本）

数字：整型，浮点型，decimal（更高精度）

（int也有tiny，small，medium，big版，浮点型分为float和double）

日期：date，datetime（日期加时间），timestamp（时间戳），time，year

## 基本操作指令

插入数据：insert into <表名>(<列名1>,<列名2>,.....) vaules(<值1>,<值2>,.....) ;

DDL（数据库定义语言）：create（创建）, drop（删除）, alter（修改）

DML（数据操纵语言）: insert（插入）, delete（删除）, select（查询）, update（修改）

DCL（数据控制语言）: commit（确认变更）, rollback（取消变更）, crant（赋予用户权限）

英文分号结尾，不区分大小写，输入法要是英文的

## 查询

Select <列名1>, <列名2>, ...... （\*号表示查询全部列）

from <表名>;

as用于为列设置别名

distinct用于删除重复的值

列名不能加单引号

查询条件：where 姓名 = "xxx";   （where里面不能带汇总函数）

注释：-- 单行注释， /*  xxxx    */多行注释

运算符：算术运算符（所有与空值进行运算的结果仍为空值）， 比较运算符， 逻辑运算符（not, and, between, or, in）

eg. is not null

模糊查询：like   

```sql
select *
from student 
where 姓名 like '李%'   /*以李开头       
%李    以李结尾
%李%   带李
```

王_, _表示任意1个字符

## 汇总分析

函数：count求某列的行数，sum求列和，avg求列平均，max列最大值，min列最小值

一般放在select语句里，表示查询对象是函数处理后的新表

分组用goup by（如果有多个列的话，只有全部都相同才能分为一组）分组后筛选用having子句

对查询结果排序用order by, asc表示升序，desc表示降序，如果有Null会被排到最前面

limit返回一部分数据

## 视图

视图中存放的是sql查询语句，使用的时候会创建一张临时表

语句是create view 视图名称（<列名1>, <列名2> ..... ） as

后面跟上查询语句

使用视图的时候直接把视图名字当成表名来使用即可

视图里不能插入数据

## 子查询

是指在from里写定义视图的sql查询语句，子查询是最先运行的

也可以结合in，all, any（some）放在where里面

所以如果偶尔使用的话，就写成子查询的形式，如果是频繁地使用，就可以保存成视图来方便查询

## 标量子查询

子查询中使用汇总函数调用，使得返回值是一行一列的情况，这种时候还可以和between，and连用。而且甚至还可以写到selct语句里面

## 关联子查询

功能是在每个组里进行比较，在子查询中用where语句限定两个表之间的关联条件。比如where s1.xxx = s2.xxx.

## 其他支持的一些函数

round(数值，保留的位数)四舍五入

abs绝对值

mod求余数

length求字符串长度

lower,upper大小写转化

replace(string, 原来的，想要替换成的)

substring(string，开始位置，截取长度) 下标从1开始

current_date当前日期，current_time, current_timestamp

year对日期求年, month月, day日, daytime求星期

## 表的加法

Union连接查询语句，会删除重复数据

union all保留重复的行

## 联结

关系数据表之间的连接

交叉联结（笛卡尔积）：表中的每一行都与另外一个表中的每一行连接在一起，比如扑克牌中点数与花色的组合

内联结： 查找出同时存在与两张表中的数据，先取出两张表中共同的key的数据，然后再进行交叉联结。写在from 子句中 inner join，on  a.xx = b.xx 这是用来选取主键的

左联结： 取出左表中的全部key数据都取出来，再交叉联结，如果在右边的表里没有对应的数据的话，就会自动填null。left join（如果想要取出左边独有的部分的话，在左联结的基础上，在where中写b.xx = null就可以实现过滤了）

右联结：right join同理

全联结：full join，直接交叉联结，空值填null。mysql是不支持全联结的

在应用的时候在selct语句中要指定列是来源于哪张表

## case表达式

实现分段人数统计，用括号括起来，后面还可以给列起别名

case when <判断表达式> then <表达式>

​         when ......

​		else <表达式>

end

有一种用法很聪明，配合sum可以实现分条件计数

```sql
sum(case when xxx then 1 else 0) as "aaa"
```

## 实战经验

select相当于一个建表选择显示列的操作

if函数接受三个参数，如果第一个参数为True，返回第二个参数，否则返回第三个参数

ifnull函数接收两个参数，当第一个参数不是null的时候返回第一个参数，否则返回第二个，第一个参数也可以是一个括号括起来的select语句

nullif函数，如果expr1 = expr2，返回null，否则返回expr1

isnull函数，如果为null返回1，不是则返回0

函数的格式是Create function name（参数名字 参数类型）returns 参数类型。里面有begin和end，值设定语句要写在return外面，SQL语句写在return里面，语句结束都要有分号

自连接（自身连接）的本质是把一张表复制出多张一模一样的表来使用

DELETE FROM 表名称 WHERE 列名称 = 值, 自更新是不允许的，所以如果有子查询应该把自查询先封装成一个新表。自联结一般要给表取别名，如果用了表别名，delete后要加别名。

DATEDIFF()用来比较两个日期之间的差, 返回的是第一个减去第二个日期的差值。还有一个函数timestampdiff，里面可以用参数指明“day”,"hour", "second"，但是不同的是返回第二个减去第一个日期的差值

## Top N SQL查询问题

where 子句里的条件会对每一条语句进行类似于循环筛选的感觉，所以复杂查询很多时候会在这里面嵌套子查询，子查询里还可以自联结地进行比较，比如count函数可以统计Top的个数。很容易让人想用group语句，但是group语句只能返回一条结果，所以这时候想实现分组的比较操作应该考虑自联结在where子句中限定组别相同

## 交换相邻的记录

这题让我体会到select虽然是最后运行的，但也可以逐条选取，配合case使用，case里面可以用别名访问列来逐条判别。count这种函数如果在select里用了的话只会返回一行，所以应该把它做成一个子查询和原表的每一行交联。

order是在select之后运行的，会把整行数据进行排序。

逗号联结等价于inner join，也就是join。左表和右表都不是空值的行进行全联结

异或运算：一个偶数^1,那么答案是偶数+1.如果是一个奇数^1,那么答案是奇数-1。（i+1）^ 1 -1可以实现两两交换。

coalesce是一个函数，依次参考各参数表达式，遇到非null值即停止并返回该值。如果所有的表达式都是空值，最终将返回一个空值。

很神奇的一点是，left join的时候，竟然会以右边的标号为顺序排列

## 交换工资

没有临时表的更新用update 表名 set xxx语句

