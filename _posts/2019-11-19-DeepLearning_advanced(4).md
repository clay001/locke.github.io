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

单个神经元可以完成线性分类器的任务（所谓的线性，指的是假设集中的模型是线性的）

感知机算法：

![perceptron](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/SOTA(4)/perceptron.png?raw=true)

数学上可以证明感知机错误的最大次数和数据个数无关，与到决策边界最近距离的平方成反比

output的决策有赢者通吃，softmax function等计算方法

线性多分类器的实现：

- 感知机
- Hinge Loss（SVM）
- log loss and logistic regression

## 强化学习在药物分子设计上的应用

强化学习在基因组学上应用几乎没有，分子结构合成领域基于GAN和图网络的方法比较多。我看到[北卡罗来纳大学](https://advances.sciencemag.org/content/4/7/eaap7885)在18年中有一篇用强化学习做药物分子设计的文章。

通过学习170万种已知生物活性分子化学结构词汇背后的句法和语言规则，创造出未出现过的新型分子。机器学习可以分为有监督，无监督和强化学习。强化学习三要素，reward，state和action。mode-free是在真实的环境中进行学习策略优化，不需要对环境进行建模，比如Q-learning，Sarsa，Policy gradients。model-based是在模拟的环境中学习，比如AlphaZero。

Policy-based得到的reward是一个概率。Value-based得到的是reward的期望。

DQN是用神经网络预测Q值的方法，policy gradients是建模连续的动作的策略选择方案，最大化衰减reward的累加期望

ReLeaSE包含一个生成器和一个预测器。生成器由一个预训练的栈式GRU构成，输出新的SMILES字符传作为预测器的输入，预测器是一个单层的LSTM网络，计算出一个reward再反馈回去。

用openChem toolkit进行预训练，预训练结果作为true label









