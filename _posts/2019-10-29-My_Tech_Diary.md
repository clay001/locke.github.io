---
layout: post
title: "My Tech Diary"
date: 2019-10-28 16:00:06
image: '/assets/img/'
description: 'thoughts and daily useful tips'
tags:
- Thoughts
- Tips
categories:
- Dairy 
twitter_text: 'thoughts and daily useful tips'
---

## Git

I know the git has version rollback function, but I didn't care too much before, because I think I've already uploaded my file to github, if I just want the previous version back why not just download the file back from GitHub? And I always think that git pull can do this for me, but I was wrong, if I modified the file and ran  with git pull, it doesn't work. 

Well, it is time to pay for my lazyness, I finally met this stupid situation, I messed it up and all I wanted is to get my previous file version back. `Git reset` saves me.

You can use `git log` to view the commit history, Head indicates your current version, and use `git reset --hard commit_id` to get back to the past. Or you can use `git reflog` to view the command history and to jump to the future.

## non-parametric fit

刚看到这种说法的原句是top 3000 high variable genes were selected on the basis of a non-parametric fit of the coefficient of variation using the mean as predictor(using support vector regression)，刚看完有点懵逼，去了解一下统计学上的非参数的含义，一是说数据不需要属于任何特定的分布，二是不对模型的结构做固定的假设。通常包括两种：一种是非参数的回归，对变量之间的关系结构做非参数化的建模，但模型的残差分布可能存在参数化的假设。一种是非参化的层次贝叶斯模型，基于狄利克雷过程，允许隐变量的个数随着data而改变，但个体变量或控制隐变量变化的过程依然遵循参数分布。

还是一脸懵逼，但大概的意思就是说非参模型的结构是由数据决定的，并不是说模型完全没有参数，而是说参数的数量和性质是灵活可变的。

## Kaggle

成立于2010年，是一个进行数据发掘和预测竞赛的在线平台，可以独立做一下101和playground的训练赛来熟悉入门：[这里](https://blog.csdn.net/bbbeoy/article/details/73274931)有一个非常好的资源集成博客，如果大家有兴趣可以深入了解一下







