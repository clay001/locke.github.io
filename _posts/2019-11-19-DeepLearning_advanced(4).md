---
layout: post
title: "Deep Learning SOTA(4)"
date: 2019-11-19 13:13:24
image: '/assets/img/'
description: 'Advanced DeepLearning'
tags:
- Deep Learning
- Machine Learning
categories:
- CS280 Notes
- Deep Learning
- Machine Learning 
twitter_text: 'Follow me to study DL'
---

## Recap

The field of deep learning is developing very fast, and there are a lot of exciting technical details which I am really interested in. I have tooken both DL and ML lessons, but since my recent research topic is far from the frontier, I find that I have forgotten a lot of theoretical foundations and operation skill which I learned before. Therefore I think the best way is to keep learning.

The purpose of this blog post is to record some important core foundations while keeping close to the cutting edge, and learn some latest technical breakthroughs.

## Lecture 1

应用：语音识别，语言翻译，图像分类，自动驾驶

人为地设计算法很难，而深度学习可以从数据中学习出相关的规律

所谓的数据驱动的方法就是去找一个映射函数，其中的参数最好在训练确定之后仍然可以适用于新的训练集，也就是鲁棒性要好

回顾一点数学基础知识：

海森矩阵是对于一个函数$f(x)$，x是一个向量，函数对于x的每一个维度的二阶偏导集合，第一行的一阶偏导是关于$x_1$的，第一列的二阶偏导是关于$x_1$的

雅可比矩阵是对于一个向量形式的函数值，每个维度的函数对每个维度的x的一阶导数集合，第一行是函数$f(x)_1$对x的每一维求导，第一列函数的每一维对$x_1$求导

高维度的高斯，此时的方差就是协方差矩阵

从概率论的角度来说这个过程可以用最大似然估计MLE去理解

Ridge regression的后面一项是权重的二范数（高斯分布），lasso regression的后面一项是权重的一范数（拉普拉斯分布）

## Lecture 2:

简单理解神经网络的节点，就是权重和数据的加权求和，再加上一个bias，最常用的激活函数有sigmoid，tanh和Relu（这个相当于非线形变换的过程）

神经元的激活在空间内可以理解为学得的w和真实的pattern之间的cos夹角，close enough的时候就激活

单个神经元可以完成线性分类器的任务（所谓的线形，指的是假设集中的模型是线形的）

感知机算法：







