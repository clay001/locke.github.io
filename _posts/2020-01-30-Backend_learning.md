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

一个web app就是一个WSGI的处理函数，针对每个HTTP请求进行响应，比如处理100个不同的url。比较流行的框架是flask，比WSGI要简单

