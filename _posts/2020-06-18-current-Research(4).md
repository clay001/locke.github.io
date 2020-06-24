---
layout: post
title: "Current research(4)"
date: 2020-06-18 11:55:21
image: '/assets/img/'
description: 'My current research topic record'
tags:
- research 
- PDE 
- RNA velocity 
categories:
- research 
twitter_text: 'New research progress of Locke!'
---

## previous goals

This project will provide/develop two numerical methods to make use of RNA velocity 

1. Quasi potential from Freidline-Wentzell theory using ordered line method -- to estimate attractor cell states and compute transition pathways 

2. Fokker Planck equation in reduced space -- to model the dynamics and do virtual gene down- / up-regulation

## Current situation

为了防止大家看不懂，我用简短的语言介绍一下背景，再在此基础之上谈一谈目前的挑战。其实这个领域的东西不难，但传统学科缺乏像计算机一样普及的社区氛围，再加上这个领域的老头儿喜欢为自己建立技术壁垒，我的导师也基本不会给予我指导，所以我刚开始接触的时候很长时间内都很痛苦，最痛苦的是这个领域的论文篇幅又臭又长，方法论上缺乏系统性，名词不做解释地层出不穷。你在理解这些东西的路上一不留神就会走偏，但其实搞明白以后一两句话就能说完。目前大部分的单细胞转录技术拿一个barcode来标识细胞，再用一小段UMI（你不用管它是什么）来标识mRNA。

基于这个单细胞测序技术的数据，细胞作为对象，不同的基因就是对象的属性，数据一般是稀疏的，会存在很多零值，怎么利用基因的调控来填补这个零值是一个挑战

传统做差异分析，我们可以用方差分析假设检验的方法，但在单细胞数据上应该如何去有效稳健地刻画这个异质性？现在的方法大多是基于基因表达谱进行无监督聚类（t-SNE，UMAP），这又是一个挑战

进一步地我们想要了解细胞所属的精确细胞类型，就像查字典一样我们需要和reference进行mapping。我们需要用各种算法来学习reference的特征来把它映射到新的数据集上，reference可以用基因表达谱，特征基因，特征基因谱，数学模型等方法来构建。从前我们需要对集群特异性基因进行文献调查，在改动参数或者数据集之后我们还需要对其进行手动的重评估，即使在相关组织的数据集中也不能进行知识的共享。为了把人工标注类型从劳动密集型向自动化进行转变，出现了一些基于marker基因的分类方法。现在有一种新的想法是把分化的过程加到构建的过程中去，如果构建又是一个挑战

轨迹推断，这也是我之前关注过的一个方向，给大家一个数据，光在2019年据不完全统计就出现了超过60中TI的方法。大部分的方法都是基于概率图模型的，最近还出了一种新的用RNA丰度的方法进行排序。以我个人的经验来说，不同的TI算法结果真的大相径庭，有一位学者曾经说过生物学需要一个包含层级结构的/稳定的inference数据库，真的很重要，这相当于这个方向的基石，不然所有人用自己藏起来的数据，都在单打独斗，公说公有理婆说婆有理

结合癌细胞肿瘤细胞在患者体内的空间位置信息，可以用来估计细胞转移的来源和方式等。或者通过测量每个亚克隆的有丝分裂和凋亡细胞的数量来估计增殖率、突变率和死亡率，这样将极大地有利于癌症中阳性和阴性选择的检测，并提高对亚克隆耐药性的预测精度。

对于不同时间点，组织，个体，测量值的数据，需要一个有生物意义的计算框架去集成。

如何对分析工具进行系统的基准评估，是否能产生高质量的预期结果，是否能够稳健地应对高水平的测序噪音和技术误差，动态可拓展性等等

## sklearn中的fit

sklearn中的所有方法在使用前都要进行fit，它是一个适配安装的过程，然后tranform进行标准化，降维，归一化的操作。fit_transform就是结合了这两部的操作的一个简化函数。