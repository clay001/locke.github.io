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

## Preface

C++ is needed when you want to run fast and well-perfomed codes, and it can directly controll the hardware. In fact, when you write some codes, you need to pass it to the complier, and the complier can give you the machine code for your target platform, machine code is the actual instruction that your devices CPU will actual perform. C++ is widely used in almost everywhere, it can support almost all the platforms. Everyone is using it ! Here I record some of the learning notes, check whether you know them all.

## hpp和h的区别 

hpp（Header Plus Plus）是将.cpp的实现代码混入.h头文件当中，定义与实现都包含在同一文件，调用的时候只需要include该hpp文件即可 

与xx.h类似，hpp是C++程序头文件。一般来说，xx.h里面只有声明，没有实现，而*.hpp里声明实现都有，后者可以减少.cpp的数量。xx.h里面可以有using namespace std，而*.hpp里则没有

但要注意的是，hpp中不可以包含全局对象和全局函数

## 取余运算上的不同

和python不同，在C++中 -1%10 的结果并不是9，而是-1。所以在我程序中碰到过的一个轮盘锁问题的时候，需要实现0负方向转动的结果是9，这时候就得再做一层操作，我当时的选择是如果是负数就用10去减一次

## 类的定义和调用

类的成员函数是指那些把定义和原型写在类定义内部的函数，就像类定义中的其他变量一样。类成员函数是类的一个成员，它可以操作类的任意对象，可以访问对象中的所有成员。

成员函数可以定义在类定义内部，或者单独使用**范围解析运算符 ::** 来定义。

在创建一个需要初始化的类的时候，如果在定义的时候没有定义默认值，则必须在创建的时候给出初始化的参数

## 

