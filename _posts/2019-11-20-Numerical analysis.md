---
layout: post
title: "Numerical analysis"
date: 2019-11-19 13:13:24
image: '/assets/img/'
description: 'Numerical analysis review'
tags:
- Numerical Analysis
categories:
- Course Review
twitter_text: 'Follow me to study NA'
---

## Some words

Previous I liked to record things in paper, or in mind :)  But recently I found my memory is so bad, I thought I will remember forever because I learned very carefully and figure out every detail when I took courses or learned from the Internet  or read books, but nothing.

Then I decide to record online for easy viewing, actually I recorded some of my notes elsewhere on other platform, I will transfer to this blog when I have time. So here start with Numerical Analysis (mainly the second half of semester)

因为是第N遍回顾了，可能比较混乱，脑子里想到什么重要的概念忘记了就先整理哪一部分，大家可以各取所需

## 线形方程

Ax = b的形式

## LU分解（方阵，不一定存在）

当矩阵A的各阶顺序主子式不为零时，A有唯一的Doolittle分解A= LU

把矩阵分解为一个下三角矩阵和一个上三角矩阵的乘积，L对角线元素都是1（这时候是Doolittle分解）。其思想就是对A自下而上地做初等行变换，直到将数据的左下部分都变为了0，这个矩阵就是U矩阵，而我们知道每一次的初等行变换就相当于左乘一系列单位下三角矩阵，这些矩阵乘在一起就是L矩阵。在编写程序的时候，角标的起止和处理顺序还是挺难的，而且挺容易出错的，这就是所谓的程序转化，有些时候很多细节不真正做过还是没有想象的那么容易的。

（考虑到计算机精度的问题，可以优化上述方法，为了使得U的对角元素不过小，加入选主元的过程，即QA = LU。具体做法是在每一次LU循环的过程中，行交换当前列最大的元素到当前位置，b也要同时进行变换）

## LR分解（对于任意矩阵）

首先矩阵A肯定不是满秩的，所以才需要进行满秩分解。因为满秩的矩阵存在逆矩阵,计算较为方便。满秩分解需要将矩阵A进行初等行变换，将其化简为Hermite型B（高斯消元的结果，阶梯形），L矩阵取非零行第一个非零元素所在的列，其对应矩阵A的列。R为B的非零行。此种变形非常利于我们求解矩阵A的四个子空间

## LUP分解

由于浮点数的固有问题，在处理数值计算问题时候，大数和小数相加减比较容易造成误差，LU分解中会产生矩阵条件数很小，但相对误差很大的情况。解决方法就是在高斯消元的过程进行一些行置换操作，使得PA=LU，来增加LU分解的稳定性。

## $LDL^T$分解（对称矩阵）

当求解方程组的系数矩阵是对称矩阵,且他的各阶顺序主子式不为零时，则A可以唯一分解为$A= LDL^T$

其思想就是LU分解更进一步，把U中的对角线元素提取出来形成一个对角矩阵D，然后利用A对称的性质和分解的唯一性，推出上式

## Cholesky分解（正定矩阵（默认对称））

如果A是一个正定矩阵（是厄尔米特矩阵的一种，在实数范围内就是对称的意思），可以把D拆成两个$\sqrt{D}$，分别分给两边的L，这样分解就成了$LL^T$的形式，如果A是半正定的，也可以进行分解，但是这时候分解就不唯一了

## QR分解（可逆矩阵存在，则分解唯一）

Q是一个正交矩阵（其实是酉矩阵，在实数矩阵中就等同于正交矩阵）， R是一个上三角矩阵。

矩阵可逆也不一定存在三角分解，但QR分解一定存在。可以推广到非方阵上，这时候要求变为列满秩。

正交矩阵可以看作坐标系的转换，R矩阵可以看作对坐标系不同维度的组合系数

## SVD分解（要求更低）

如果对于一个非方阵（m\*n），仍然可以进行奇异值分解，分解为正交矩阵（有转置等于其逆的性质）和对角矩阵，$USV^T$的形式

U为m\*m矩阵，由$AA^T$ 的m个特征值对应的特征向量组成。

V为n*n矩阵，由$A^TA$的n个特征值对应的特征向量组成。

S的对角线上为奇异值，其余为0

## 分解矩阵有什么用

其实矩阵的乘法就相当于对空间进行缩放，对角矩阵的乘法就相当于对每个坐标轴进行缩放（scale），三角矩阵的乘法相当于水平或者竖直的斜拉（shear），正交矩阵的乘法就相当于旋转（rotate）。分解中很喜欢三角阵，原因是因为像高斯消元法一样，他很容易逐层迭代进行求解。结合这三种矩阵的乘法，可以使得在求解方程的过程中绕过求逆运算，既可以保证精度，也可以简化计算。（比如LL就可以应用在相关性分析中）

## 特征值和特征向量的求法

在这种问题中的矩阵一般是方阵，方阵就不用SVD分解这么麻烦了，可以直接进行特征值分解成$WDW^T$的形式，常见的做法是先求特征值写到D里，再求特征向量（标准化一下）按列填到W里。

## 矩阵的条件数

向量范数是对向量长度的衡量，矩阵范数则用来衡量矩阵对实体变换的能力，一般定义为矩阵作用在一个向量x上得到的向量范数除以x本身的范数，x取能让这个结果最大的向量。

假设考虑一个矩阵A，则他的逆的范数可以推导出等于$1/min_{x}\frac{\left \|Ax  \right \|}{\left \|x  \right \|}$，如果A的范数代表对于实体拉伸的能力，等同于A的逆的范数对实体的压缩能力。条件数定义为上述两个范数的比值，通常记为k，可以理解为使得实体向量发生形变的能力

联想奇异值分解，他在几何上的表现就是将一组正交基转化为另一组正交基，奇异值描述了对应基向量的放缩倍数。因此在实际计算的时候k（A）就可以用A的最大奇异值除以最小奇异值来得到。

如果是正规矩阵，就是最大特征值除以最小特征值的绝对值

## 线性方程的稳定性

对形如Ax = b的线性方程，对b添加微小的扰动，观察对x的影响

数学推导可以得到一个双端不等式，![1](https://www.zhihu.com/equation?tex=%5Cbegin%7Bequation%7D+%5Cfrac%7B1%7D%7B%5Ckappa%28A%29%7D+%5Cfrac%7B%5Cleft%5ClVert+%5Cdelta+b+%5Cright%5ClVert%7D%7B%5Cleft%5ClVert+b+%5Cright%5ClVert%7D+%5Cle+%5Cfrac%7B%5Cleft%5ClVert+%5Cdelta+x+%5Cright%5ClVert%7D%7B%5Cleft%5ClVert+x+%5Cright%5ClVert%7D+%5Cle+%5Ckappa%28A%29+%5Cfrac%7B%5Cleft%5ClVert+%5Cdelta+b+%5Cright%5ClVert%7D%7B%5Cleft%5ClVert+b+%5Cright%5ClVert%7D+%5Ctag%7B6%7D+%5Cend%7Bequation%7D)

可以看出条件数越大，越不稳定

## 几个概念

奇异非奇异是对方阵而言的，奇异矩阵的行列式为0，非奇异对应满秩

奇异矩阵的条件数字为无穷大，正交矩阵的条件数为1

病态矩阵的条件数远离1

特征值分解是找一组只有缩放效果的基（特征向量），奇异值分解是找一组有旋转、缩放、投影的基。



