---
layout: post
title: "C++ learning"
date: 2019-10-19 15:22:44
image: '/assets/img/'
description: 'Some knowledge about C++'
tags:
- C++  
categories:
- Language 
twitter_text: 'Do you know these?'
---

## hpp和h的区别 

hpp（Header Plus Plus）是将.cpp的实现代码混入.h头文件当中，定义与实现都包含在同一文件，调用的时候只需要include该hpp文件即可

与xx.h类似，hpp是C++程序头文件。一般来说，xx.h里面只有声明，没有实现，而*.hpp里声明实现都有，后者可以减少.cpp的数量。xx.h里面可以有using namespace std，而*.hpp里则没有。

但要注意的是，hpp中不可以包含全局对象和全局函数

## 取余运算上的不同

和python不同，在C++中 -1%10 的结果并不是9，而是-1。所以在我程序中碰到过的一个轮盘锁问题的时候，需要实现0负方向转动的结果是9，这时候就得再做一层操作，我当时的选择是如果是负数就用10去减一次

