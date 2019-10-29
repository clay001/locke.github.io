---
layout: post
title: "Deep Learning SOTA(3)"
date: 2019-10-26 13:28:17
image: '/assets/img/'
description: 'Advanced DeepLearning'
tags:
- Deep Learning
- Machine Learning
categories:
- Auto-Encoder
- Deep Learning
- Machine Learning 
twitter_text: 'Follow me to study DL'
---

## Recap

The field of deep learning is developing very fast, and there are a lot of exciting technical details which I am really interested in. I have tooken both DL and ML lessons, but since my recent research topic is far from the frontier, I find that I have forgotten a lot of theoretical foundations and operation skill which I learned before. Therefore I think the best way is to keep learning.

The purpose of this blog post is to record some important core foundations while keeping close to the cutting edge, and learn some latest technical breakthroughs.

## Auto-Encoder

大家应该都学过一些典型的有监督学习算法，如SVM，DNN或boosting，决策树等。但有监督学习需要大量带标签的数据，对数据标注是一个需耗费人力与时间的工作。反观不带标签的数据，那可谓取之不尽用之不竭。因此我们可利用无监督学习对其进行聚类或特征提取。利用无监督学习得到的特征结果也可应用到带标记数据较少的有监督学习任务中，提高其分类性能。

自编码器就是其中一个例子，目前这个技术主要有两方面的应用，分别是降噪和降维。网络先是一个encoder进行表征学习，用压缩过程迫使网络去学习输入中的一些结构信息，得到的中间结果称为一个bottleneck层，然后再用一个decoder去进行重构，误差函数就是重构误差，算法的训练过程就是在拟合一个恒等函数。权值更新一般结合批梯度和随机梯度，采用一种折中的最小批方法。相比于PCA这种找线性超平面的方法，auto-encoder可以学到一些非线性的流型信息。

为了使我们的自编码器能够真正地学到东西而不是简单的记忆，我们能想到可以减少bottleneck层的节点数。但其实即使只有一个隐藏层节点，只要有足够的capacity，模型依然可以记住训练数据。这时候稀疏自编码器(如下图)就十分有效

![稀疏自编码器](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/SOTA(2)/sparse.png?raw=true)

我们让模型选择性地去激活网络区域，同时对过度激活进行惩罚。可以加L1正则化，也可以用KL散度。

结合上特定的任务，以降噪为例。如果我们在输入的时候适当地对输入进行一些破坏，输出仍然以未被破坏的输入作为目标。这样我们最后的模型就具有了一定的降噪能力。

如果说降噪自编码器能够抵抗有限小扰动的输入，那么还有一种模型可以抵抗无限小的扰动，称为压缩自编码器。它通过构造一个损失项，该项会对输入的衍生进行惩罚，本质上是惩罚了输入中的微小变化导致编码空间发生巨大变化的实例。用数学语言来说就是雅可比矩阵的F范数，也就是对一阶偏导矩阵的L2范数。

对于降维任务，我个人认为可以尝试取出训练好模型的bottleneck层，但有一个挑战就是如何确保这个压缩表示是有意义并且可泛化的。

## 变分自编码器

VAE以概率的方式描述潜在空间观察。因此，我们不再是输出单个值来描述每个潜在状态属性，而是用每个潜在属性的概率分布来描述。在decoder的时候再从每个状态分布中随机采样，生成一个向量作为解码器的输入。特别地，对于VAE的编码器又称之为recognition model，解码器称为generative model。

假设我们的观测是由一个隐变量Z决定的，我们相当于是想计算$p(z|x)=\frac{p(x|z)p(z)}{p(x)}$ 其中分母通常是一个非常复杂的分布$p(x) = \int p(x|z)p(z)dz$，这时候我们用变分推断取去估计它，做法是记一个近似分布为$q(z|x)$, 我们要做的是使q尽可能地逼近真实的先验分布p(z), 也就是想让这两个分布之间的KL散度最小。变换一下也就是最大化下面的式子：
$$
E_{q(z|x)}logp(x|z)- KL(q(z|x)||p(z))
$$


然后encoder的过程我们就用q来把输入的x映射到隐藏空间z中，decoder则用likelihood$p(x|z)$再映射回$\hat{x}$。写成损失函数的形式就是：
$$
\mathcal{L}(x,\hat{x}) + \sum_{j} KL(q_j(z|x) || p(z))
$$


其中j代表维度，前一项代表重构误差，后一项代表分布的差异程度。

既然我们假设先验是符合正态分布的，那么我们可以构建如下的网络结构：

![model](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/SOTA(2)/model.png?raw=true)

 中间输出的是两个描述均值和方差的向量，解码器该分布中进行采样，然后生成一个潜在矢量进行后续的重构。

采样的过程应该是随机的，但是随机又无法进行梯度反传，所以需要用到一个技巧叫reparameterization trick（再参数化）。即先从单位高斯中随机采样ε，再通过潜在分布的均值μ和方差σ对其进行缩放 。

![repara](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/SOTA(2)/repara.png?raw=true)

![repara2](https://github.com/clay001/blog/blob/gh-pages/_posts/posts_picture/SOTA(2)/repara2.png?raw=true)

在调试的过程中，可以尝试检查潜在空间的分布情况，或是一些样本的潜在维度，以了解分布的特征，同时相应地改变重构误差和KL散度项的权重：
$$
\mathcal{L}(x,\hat{x}) + \beta\sum_{j} KL(q_j(z|x) || N(0,1))
$$



[本文参考[yuxianyu](http://www.atyun.com/17888.html)的博客]

