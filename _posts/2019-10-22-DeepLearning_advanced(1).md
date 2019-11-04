---
layout: post
title: "Deep Learning SOTA(1)"
date: 2019-10-22 19:25:37
image: '/assets/img/'
description: 'Advanced DeepLearning'
tags:
- Deep Learning
- Machine Learning
categories:
- Graph Neural Network
- Deep Learning
- Machine Learning 
twitter_text: 'Follow me to study DL'
---

## Recap

The field of deep learning is developing very fast, and there are a lot of exciting technical details which I am really interested in. I have tooken both DL and ML lessons, but since my recent research topic is far from the frontier, I find that I have forgotten a lot of theoretical foundations and operation skill which I learned before. Therefore I think the best way is to keep learning.

The purpose of this blog post is to record some important core foundations while keeping close to the cutting edge, and learn some latest technical breakthroughs.

## 图神经网络

其实我早在19年年初就已经关注到了GNN，很多大牛都预言它将是未来的潮流，我也加入了一些图神经网络的讨论小组，原本想要蹭蹭风口，但由于条件限制，在没有研究环境也没有时间的情况下，就没有过多了解。

原本我觉得GNN应该是做一些社交网络之类的推理课题，因为在医疗健康领域数据是非常昂贵的，想要做到大数据上DL几乎是不太可能的，但近期无监督学习，数据增强，迁移学习之类的兴起让我似乎看见了些许希望。图本身实在是太强大了，保罗万象，几乎所有的科学问题都能被抽象到图上。而且都说ICML是未来研究热点的标杆，如今GNN在科研舞台上风生水起，抱着对未知本能的好奇，我决定好好了解一下。

图灵奖得主、贝叶斯网络之父Judea Pearl曾经发文指出，当前的机器学习系统几乎完全以统计学或盲模型的方式运行，不能作为强AI的基础。这点我非常认同，现在的媒体吹的太厉害了，我之前也是信以为真，但自从接触深度学习的理论之后，我也是认为这种小打小闹虽然可以现象级地解决一些大数据的问题，但想要达到科幻片里的未来世界是不可能的。他老人家认为突破口在于“因果革命”。

GNN号称完成了1.DL应用过渡到非欧几里得空间，2.赋予DL以因果推理的能力这两大壮举。

## DeepGCNs: Can GCNs Go as Deep as CNNs? 

这一篇ICCV2019的文章，深度学习之所以效果好，很大程度上是因为深，那么GCN如果也可以变深，那么效果自然也会变好，文章通篇就是围绕这个思路展开的。类比CNN，借鉴CNN中克服困难的技术，最后在点云中的语义分割任务上进行测试，并进行稳定性和性能影响分析。GCN是点云任务的一个很好的候选，他有一套动态边卷积（dynamic edge conv）的方法可以去做这个事情。

首先如果变深很自然地就会出现梯度消失/爆炸问题，因为我们在反向传播的时候是依赖梯度去更新参数的，为了解决这个问题，可以用residual connection的方法加上一条恒等映射。也可以用dense connection，把层和前面所有的层都连接起来，增加每层的复用率。

还会出现节点特征过度平滑的问题，主要是因为pooling过多导致空间信息丢失，可以用dilated convolution（空洞卷积，膨胀卷积）的方法来扩大感受野，感受野中的采样点还是不变，只是在中间加上一些不采样的点，使其不止考虑一阶邻居的节点信息。

整个的分割的框架就是在GCN之后接上fusion block（1*1的global maxpool），然后再接MLP prediction block（多层感知机预测）

[详细资料](https://blog.csdn.net/yyl424525/article/details/99464457)

## to be continued



