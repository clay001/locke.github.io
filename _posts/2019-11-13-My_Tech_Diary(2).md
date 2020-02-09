---
layout: post
title: "My Tech Diary(2)"
date: 2019-11-13 16:00:06
image: '/assets/img/'
description: 'thoughts and daily useful tips'
tags:
- Thoughts
- Tips
categories:
- Dairy 
twitter_text: 'thoughts and daily useful tips'

---

## Where should we go?

Nowadays, more and more people want to be programmers, their purpose is always the same: for money. Well it is not wrong, but I just feel that something is wrong. In the past, when people talk about programmer, the first impression coming to the mind is that they are not good at communicating with others, loving staying messy at home, rigid, boring and heavy workload. Yeah, you are right, they are all stereotypes. But look at now, programmers are symbols of high IQ, successful, high salaries etc. The shift is so fast, I think it is the propaganda went awry.   

The media vigorously agitate artificial intelligence, deep learning, news are all about how rich programmers are, depicts the technical bright future for you and thousands of training institutions came up saying that they can make you rich. Bullshit, by the way I always don't like social media, they are the monster who has the power to manipulate the public mind and reverse black and white. It is not good for both society and academia, not everyone is suitable for programmer, and the future is not that "bright". Will the salary always match to your effort? What you sacrificed? Health? Happiness?

Although myself is a half way programmer, but I think there is something more important than money, I feel happy when I am doing what I want to do. I saw lots of people dived into this area but don't know why they dived. They feel unhappy all the time but making the job competition way too severe. 

Well, stop thinking here, just keep going my way :)

## 第一次ak了周赛

这次的周赛比较简单，基本都是不太用脑子的暴力解法就可以搞定，但非常珍贵的是学了一些很好用的用法，首先是eval函数，它可以将字符串转为变量名进行访问，相似的还有local和vars，还没尝试过。

其次是C++和python中class里面的定义和调用。以及运用dfs编写程序的一些思路，先写好主函数框架，定好需要传入的参数，然后再去补dfs的细节。

然后学到了枚举可以用1<<n，然后在for里用n>>i进行按位访问，这时候就用到了很多大佬很喜欢用的按位与&或者一些其他的操作了。

## 双周赛+周赛+kick start的酸爽周末

做题做上瘾，同时还能追追星，舒服，所以我又去啦

## 164周赛

这次真的福利，前三题都很简单，

## 关于算法复杂度的分析

主定理分析法，专门用于分析递归问题，$T(N)=a*T(N/b)+Θ(N^d)$, a是问题的个数，每个问题大小为N/b，$Θ(N^d)$用于完成递推以外的操作。举个例子，以用先序遍历和中序遍历还原二叉树的递归代码为例，划分是常数时间完成的，d=0，二分a=2，b=2

比较d与$log_ba$的大小，若小于，则复杂度为$n^{log_ba}$；若等于，则为$n^{log_ba}logn$；若大于，则为$N^d$

## 图像处理中的mask操作

掩膜，用于对图像的局部或者全部进行遮挡，控制图像处理的区域或处理过程

用处：提取感兴趣的区域；屏蔽部分区域；结构特征提取，用相似性变量或图像匹配方法检测和提取图像中与mask相近的结构特征；特殊形状图像的制作

做法：通常是两个矩阵对应像素之间的与运算（&），或者其他运算

## 集成学习

Adaboost：重点关注被错分的样本（弱分类器的线性组合）（或者理解为一种加法模型，指数的损失函数，前向分步的二分类学习方法）

- GBDT（boosting）串行构造决策树，进行预测
- Gradient boosting：存负梯度，异常值
- Random Forest（bagging）：决策森林
- XG-boost是GBDT的改进，用到了二阶展开
- Light-GBM    leaf-wise 又分为GOSS（Gradient based one side samping）和EFB ( exclusive feature bundling)
- Cat-boosting: Category boosting

## 医学图像处理

https://zhuanlan.zhihu.com/p/68111445

https://www.zhihu.com/people/zhangzhenren/posts

## 总线

包括一组数据线，一组控制线和一组地址线

类型分为内部总线，系统总线和通信总线

北桥是主存控制器，连接处理器总线和存储总线。南桥是I/O控制器，连接PCI总线和E( ISA )总线，南北桥之间通过桥间接口相连。

## 中央处理器CPU

是计算机的运算核心和控制单元。包括运算逻辑部件，寄存器部件和控制器部件。 

## 

