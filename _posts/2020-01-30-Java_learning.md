---
layout: post
title: "Java learning"
date: 2020-01-30 11:01:14
image: '/assets/img/'
description: 'learning java and its relevant structure'
tags:
- java
categories:
- Language 
twitter_text: 'Follow me to study java' 
---

## Some words

xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx follow runoob and microsoft book.

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




