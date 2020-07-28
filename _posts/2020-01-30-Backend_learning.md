---
layout: post
title: "Backend learning"
date: 2020-01-30 11:01:14
image: '/assets/img/'
description: 'learning backend and its relevant structure'
tags:
- career
categories:
- Backend
twitter_text: 'Follow me to study backend' 
---

## Some words

Remember the day I borrowed your brand
new car and dented it?
I thought you'd kill me, but you didn't.
And remember the time I dragged you to the beach,
and you said it would rain, and it did?
I thought you'd say, "I told you so." But you didn't.
Do you remember the time I flirted with all
the guys to make you jealous, and you were?
I thought you'd leave, but you didn't.
Do you remember the time I spilled strawberry pie
all over your car rug?
I thought you'd hit me, but you didn't.
And remember the time I forgot to tell you the dance
was formal and you showed up in jeans?
I thought you'd drop me, but you didn't.
Yes, there were lots of things you didn't do.
But you put up with me, and loved me, and protected me.
There were lots of things I wanted to make up to you
when you returned from Vietnam.
But you didn't.

follow runoob and microsoft book.

## 后端开发做什么

一个web会分为前端和后端，前端主要是静态用户界面加上一些动态效果，不涉及数据逻辑。后台一般做的是连接数据库后的逻辑处理，也有可能会参与系统架构的设计。另外，一个好的后端开发人员得知道如何使用各种框架和库，如何将它们集成到应用程序中，以及如何构建代码和业务逻辑，用一种使系统更易于维护的方式。

## 设计模式

设计模式（Design pattern）代表了最佳的实践，通常被有经验的面向对象的软件开发人员所采用。设计模式是软件开发人员在软件开发过程中面临的一般问题的解决方案。这些解决方案是众多软件开发人员经过相当长的一段时间的试验和错误总结出来的。

## 测试用例的设计

一个程序需要有测试用例来测试，强调测试场景，测试步骤化，用例流程化，将分支梳理为测试场景，通过覆盖测试场景来覆盖业务逻辑。

首先明确原始需求，梳理业务逻辑。分为页面测试和业务逻辑类测试。

页面测试包括整体界面测试，界面元素测试，控件操作验证。

业务逻辑测试可以用边界分析法，等价类划分法，错误推测法，检查测试用例的逻辑覆盖程度等等。

## 架构设计

实际上是如何合理的对现实的人力架构进行系统映射，以便最大限度的压榨整个公司的运行效率。

前后端不分离架构，用户在浏览器上发送请求，服务器端接收到请求，根据 Header 中的 token 进行用户鉴权，从数据库取出数据，处理后将结果数据填入 HTML 模板，返回给浏览器，浏览器将 HTML 展现给用户。这时候需要的是全栈开发人员，既要会数据库开发（SQL），又要会服务器端开发（java，C#），又要会前端开发（HTML、CSS、JS）。

前后端分离架构，分离的是人员职责，人员职责分离，所以架构也发生变化了。现在 Web 服务器不再处理任何业务，它接收到请求后，经过转换，发送给各个相关后端服务器，将各个后端服务器返回的，处理过的业务数据填入 HTML 模板，最后发送给浏览器。Web 服务器和后端服务器间，可以选用任何你觉得合适的通信手段，可以是 REST，可以是 RPC。这样，前端人员和后端人员约定好接口后，前端人员彻底不用再关心业务处理是怎么回事，他只需要把界面做好就可以了，后端人员也不用再关系前端界面是什么样的，他只需要做好业务逻辑处理即可。服务的切离，代码管理，服务部署也都独立出来分别管理，系统的灵活性也获得了极大的提升。

## SOA

Service Oriented Architecture，面向服务架构，精髓是严格的松散耦合，不允许直接访问其它服务的数据，大家按照一个契约或标准（service interface）来进行交流。三层架构：服务器，应用层，前端。

## Jdk1.8之后的HashMap底层原理：红黑树

红黑树是一种自平衡的二叉树，根结点始终是黑色，叶子NIL结点都是黑色，红色结点的两个直接孩子结点都是黑色，从任一结点到每个叶子结点的所有简单路径都包含相同数目的黑色结点

## 分布式系统

分布式指的是多台PC在地理上分布在不同的地方，分布式计算是基于多台PC，被分解的小任务之间有独立性，节点之间的结果几乎不相互影响，实时性要求不高。而并行计算是基于同一台PC，利用CPU的多核共同完成一个任务。

分布式操作系统负责管理分布式处理系统资源和控制分布式程序执行。分布式文件系统具有执行远程文件存取的能力。分布式程序设计分布于多台PC上被同时执行，一般被按照层数进行划分。分布式数据库管理系统对各个不同的站点进行统一管理。

Hadoop就是一个分布式系统基础框架，基于这个框架开发的程序，可以利用集群的高速运算和存储的威力。类似于基于NVDIA的CUDA并行框架开发并行程序。HDFS是hadoop的文件系统，Hbase是基于hadoop的数据库系统。Hive是基于hbase的高层语言（类似于SQL）

## 网格计算

是分布式计算的一种，利用大量异构计算机的未用资源，组成一个虚拟的超级计算机，整个计算就像是由成千上万个“PC节点”组成的一张网格

另外，我所理解的云计算就是集群的计算机能力交付。雾计算就是云计算在物联网环境下的改进，将部分计算下压到终端设备上来。

## 集群的特点

高可用集群：集群中有某个节点失效的情况下，可以将任务自动转移到其他正常的节点上。

负载均衡集群：分摊压力

## app测试和web测试

## web框架

浏览器上网的过程是客户端与服务器的交互过程，客户端就是浏览器Chrome，Firefox等。服务器程序包含了web服务器和web应用两部分，web服务器用于接收客户端的请求，由web应用对浏览器的请求进行处理，将生成的响应传给web服务器，再由web服务器返回给客户端。

web框架产生于web应用之上，它可以使开发者专注于编写业务逻辑代码而无需关心应用内各模块连接之类的重复性工作。常见的web框架有Django，tornado，flask，webpy。

WSGI协议可以将web框架和web服务器分开，是一种简单而通用的接口协议，uwsgi是基于二进制的线路协议，uWSGI是一个web服务器，实现了WSGI协议，uwsgi协议，http协议等。

一个web app就是一个WSGI的处理函数，针对每个HTTP请求进行响应，比如处理100个不同的url。Django大而全，Flask小而精，Tornado非阻塞式服务器性能高。虽然像Django，Flask框架都有自己实现的简单的WSGI服务器，但生产环境下还是建议用其他的WSGI服务器，在Java中用的比较多的就是Tomcat

在实际应用中，由于Tornado的插件没有Flask（使用Jinjia2模版引擎）多，所以会结合两者的优点进行开发

## 正向代理和反向代理

正向代理：客户端明确需要访问的网址，然后通过代理服务器来转发请求和响应

反向代理：用户的请求通过Nginx服务器进行反向代理分发给分布式部署的服务器

## 部署相关

Nginx可以实现反向代理，负载均衡等功能，可以起到一个网关的作用

Gunicorn是一个 UNIX下的 WSGI HTTP 服务器，Gunicorn默认使用同步阻塞的网络模型(-k sync)，对于大并发的访问可能表现不够好，为此可以套一个gevent来增加并发量

Docker是一个容器。仅仅只用维护一个配置文件告诉计算机每次部署要把什么东西装进“容器”，甚至借用一些工具把这个过程自动化，部署就会变得很方便

## Dubbo

一般来说Nginx是用于分发请求给分布式存储的服务器的，服务器又需要把请求发送给需要调用的应用层，这时候需要Dubbo来进行不同服务器间的数据交互来决定调用哪个service层去数据库读取数据（这时候涉及到MQ，ZooKeeper，Redis，Mysql等技术）

## 大数据相关知识

多线程同时操作一组数据的时候，为了保证准确性，可以加锁，放在同步代码块中。

线程交替读取数据，因为同步的时间不同，会产生最终全局变量的值有一个范围。

Bernstein条件是指两个过程如果有数据冲突，那么就没法并行执行。

并发是同时处理很多事情，并行是同时执行很多事情，并发的关键是处理多个任务的能力而不一定要同时。在单cpu中，系统调度在某一时刻只能让一个线程运行，一般用时间片轮巡机制，切换的过程就是并发的过程。多cpu才可以实现并行。

一个容器类数据结构，读写平均，使用锁机制保证线程安全。如果要综合提高该数据结构的访问性能，最好的办法是分段加读写锁。如果只对写操作加锁不对读操作加锁的话，有可能会读到脏数据。

CopyOnWrite的核心思想是利用高并发往往是读多写少的特性，对读操作不加锁，对写操作，先复制一份新的集合，在新的集合上面修改，然后将新集合赋值给旧的引用。如果读写平均，不适用。

```
lock(m1) lock(m2) unlock(m1) lock(m1) unlock(m2) unlock(m1) 会造成死锁，要用两个线程去思考这个问题，因为当线程1持有m2想解锁m1的时候，m1正被运行到第一步的线程2持有，相互握着别人要的锁
```

VLAN是Virtual Local Area Network，虚拟局域网。是一种将局域网设备从逻辑上划分成一个个网段从而实现虚拟工作单元的数据交换技术。最大的好处是可以隔离冲突域和广播域，在同一个Vlan中，所有设备都是同一个广播域的成员，并接收所有的广播。而不是同一个Vlan成员的交换机上，所有的端口都会对广播数据进行过滤。因此，通过VLAN的划分可以有效地缩小广播风暴产生的范围，也能够在产生广播风暴时得到更准确的定位，减少排故时间。

原子操作是汇编级别支持的指令lock xadd，简单变量的线程同步用这种方式效率最高。

RCU（Read-Copy-Update），新旧副本切换机制，这个和CopyOnWrite差不多。

CAS（Compare-and-Swap），可以做到无锁栈，无锁队列，是汇编层面的东西。

银行家算法：该算法需要检查申请者对各类资源的最大需求量，如果现存的各类资源可以满足当前它对各类资源的最大需求量时，就满足当前的申请。换言之，仅当申请者可以在一定时间内无条件归还它所申请的全部资源时，才能把资源分配给它。这种算法的主要问题是，要求每个进程必须先知道资源的最大需求量，而且在系统的运行过程中，考察每个进程对各类资源的申请需花费较多的时间。另外，这一算法本身也有些保守，因为它总是考虑最坏可能的情况。

## 运营模型

线下营销模型AIDMA（Attention, Interest, Desire, Memory, Action）

互联网行为模型AISAS（Attention, Interest, Search, Action, Share）

流量转化模型AARRR（Acquisition, Activation, Retention, Revenue, Referal）

分别是获取用户，激活，留存，收入和推荐，一层一层转化率会越来越低，但用户的价值会越来越高。AARRR并不是严格按照顺序来执行的，每一个环节也不是绝对必要的，环节与环节之间也不是严格区分的。通过锻炼这种框架思维，可以更好地了解互联网产品，去分析一些现有产品的优劣等等

