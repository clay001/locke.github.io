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

## SOCKET（套接字）

两个跨计算机的进程要进行通讯的话需要通过网络对接起来，比如服务器程序需要绑定在本机的某个端口号上，套接字就是指代承载着走通讯的系统资源的标识。处于应用层和传输层之间

## 数据库查找

学生成绩离两门成绩大于80的学生名字

```mysql
Select S.name 
From Student S
GROUP BY S.name
Having MIN(S.score)>= 80 and count(*)>=2
```

## 关系型数据库

- Oracle、DB2、Microsoft SQL Server、Microsoft Access、MySQL

## 非关系型数据库 NOSQL(Not Only SQL)

- NOSQL特点：

- - 易扩展，数据之间没有关系的。
  - 大数据量，高性能。高性能读写非常灵活的。
  - 灵活的数据模型。不需要事先对存储数据建立字段。
  - 高可用。

- NOSQL主要主流产品

- - Redis、CouchDB、mongoDB、Cassandra。NOSQL中比较火的三个数据库Redis、Memchache、MongoDb。

