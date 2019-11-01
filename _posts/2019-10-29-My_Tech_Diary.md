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

刚看到这种说法的原句是top 3000 high variable genes were selected on the basis of a non-parametric fit of the coefficient of variation using the mean as predictor(using support vector regression)，刚看完有点懵逼，去了解一下统计学上的非参数的含义，一是说不需要假定数据属于任何特定的分布，二是不对模型的结构做固定的假设。通常包括两种：一种是非参数的回归，对变量之间的关系结构做非参数化的建模，但模型的残差分布可能存在参数化的假设。一种是非参化的层次贝叶斯模型，基于狄利克雷过程，允许隐变量的个数随着data而改变，但个体变量或控制隐变量变化的过程依然遵循参数分布。

还是一脸懵逼，但大概的意思就是说非参模型的结构是由数据决定的，并不是说模型完全没有参数，而是说参数的维度是灵活可变的。说实话，看到这里我仍然一头雾水。但以高斯过程回归为例，这是一个非参数统计模型，也就是说即使我们通过学习得到了均值和高斯核的参数，模型仍然不能被唯一确定，所以我们可以通过参数代入估计的方法去做预测，但是也可以用蒙特卡洛方法进行纯数值的预测（后面分两条介绍）。参数模型的话就做不到后面这一点。

## 高斯过程

高斯分布的随机过程，任意一个点x，对应一个高斯随机变量f(x)，联合概率也可以简写成高斯分布，均值假设为0，还有一个核函数K。联合概率看作先验，观测y作为后验，然后在新的点上做预测

## 贝叶斯最优化

还是针对上面的高斯过程，可以加入贝叶斯的思想，通过从先验中抽取样本更新后验来近似真实后验。

## Kaggle

成立于2010年，是一个进行数据发掘和预测竞赛的在线平台，可以独立做一下101和playground的训练赛来熟悉入门：[这里](https://blog.csdn.net/bbbeoy/article/details/73274931)有一个非常好的资源集成博客，如果大家有兴趣可以深入了解一下。

## 蒙特卡洛方法

在积分问题无法找到原函数的情况下，可以通过用一个随机变量对被积函数进行采样的方法来求解，采样可以是均匀的也可以是不均匀的。数学上可以证明随着采样点的增多，求解是收敛的。

大致的思路是通过生成大量的随机数，给出一个参数的近似值。

看起来很像随机投点，但实际上是不同的，随机投点在一维上还可以做，但当维度升高的时候会有维度灾难，点在空间的分布会变得非常稀疏。但蒙特卡洛方法并不会受到影响，这是由它的一些特殊的处理方法决定的。比如采样点的选择（逆变换采样，拒绝采样，Metropolis method），方差缩减（解析积分-均匀样本放置，自适应样本放置）等等。

## 蒙特卡洛树搜索

在强化学习中好像比较重要，棋类游戏的模拟中也会用到，大致分成四步：选择(Selection)，拓展(Expansion)，模拟(Simulation)，反向传播(Backpropagation)

搜索树中的每一个节点包含了三个基本信息：代表的局面，被访问的次数，累计评分。UCT (UCB for Tree)是最经典的代表算法。

## 马尔可夫链

马尔可夫链由概率相互关联的序列组成，每一事件来自一组结果，每个结果根据一组固定的概率确定下一个结果。马尔可夫链的命名者安德烈·马尔科夫（Andrey Markov）最著名的案例之一就是要从一部俄罗斯诗歌作品中输出数千个“两字母对”（two-character pairs）。利用这些对，他计算了每一字母的条件概率。也就是说，给定前面的字母或空格，就能预测下一个字母是A还是T，或是一个空格。利用这些概率，马尔可夫可以模拟任意长的字符序列，这就是马尔可夫链。尽管前几个字母很大程度上取决于起始字母的选择，但是马尔可夫表明，从长远看来，字母的分布也遵循一种模式。因此，即使是相互依赖的事件，如果它们受到固定概率的影响，也将遵循平均水平的模式。

## 马尔可夫链蒙特卡洛方法（MCMC）

MCMC方法是用来在概率空间，通过随机采样估算兴趣参数的后验分布。

在贝叶斯统计中，代表参数信念的分布被称为先验分布。可能性分布通过表示参数值的范围和每个参数所体现的正观察数据的可能性，总结了已观测数据的意义。然后我们要做的是结合上述两个分布，去估计后验分布，在前两个分布非常标准的情况下可以直接求解，在遇到困难的时候，就可以用MCMC方法。

MCMC方法是蒙特卡洛方法的一种更通用的形式。其中有一个很关键步骤叫做细致平稳条件，为了解决采样的问题，有MCMC采样，M-H采样，Gibbs采样，现在Gibbs采样用的是最多的，有了Gibbs采样来获取概率分布的样本集，有了蒙特卡罗方法来用样本集模拟求和，他们一起就奠定了MCMC算法在大数据时代高维数据模拟求和时的作用。

## Kinetic Monte Carlo

又称Gillespie算法。

> 虽然Gibbs算法使得提议的接受率为1，让算法的效率更高并且在高维应用更稳定，但其对提议分布和目标分布的要求太过苛刻，大部分时候还是需要用Metropolis-Hasting算法。而接受率的出现使得部分提议无法接受，让算法的计算量增加，并且在高维时又因为各维度接受率的存在而使得提议效率急剧降低。如何提出不需要接受率的方法就成了一件比较重要的工作。

依然延袭MCMC的大框架，但对Metropolis-Hasting算法中每步都考虑是否接受进行改进，提议一定接受，并计算接受该提议所需要的时间。有很大一部分系统的概率演化都可以表示成ODE的形式，被称为主方程或者Fokker-Planck方程（Kolmogorov方程的直接推论 ）。Fokker-Planck方程称为化学中的质量守恒方程，浓度具有概率意义，里面的Q也具有概率意义，更深地牵扯到一些物理，化学，数学的东西，就实在有些复杂了。用该算法可以解这种方程里的Q矩阵。

## 朗之万方程

这个牵扯到的东西就非常理论物理了，从统计力学的哈密顿系统开始建立一个完全确定的动力系统，刚开始是用于研究溶液/大分子胶体/悬浮液系统的。从中可以积分得到溶剂分子的轨迹，经过一系列变换可以转变为一个非确定的，带高斯白噪声的随机微分方程，这就是朗之万方程。然后通过布朗运动满足的一些性质来进行修正，给朗之万方程一个更加严谨的定义，它有两种形式，一种是伊藤-朗之万积分，一种是Stratonovich-朗之万积分。通常选用保持“因果律”的伊藤公式，为了计算，后续要需要对其进行链式法则的修正。

换个思路，还是从随机微分方程出发，它描述的是某个流体中悬浮着的粒子的轨迹，限定在马尔可夫过程中，经过推导可以得到Chapman-Komogorov方程。马尔可夫过程的概率密度随时间的增量等于这段时间内流入这一区域的概率，减去流出这一区域的概率，由此我们可以写出主方程，由朗之万方程对应的马尔可夫过程的主方程又叫做Fokker-Plank equation，这个方程也有对应的两种诠释（Stratonovich积分和伊藤积分），FP方程实际上就是概率密度的扩散-漂移方程。ps. 类似地，与反向主方程类似，我们也可以得到反向FP方程。

FP方程所描述的系统，可以对稳态的细致平衡条件作出讨论，也就是说稳态的一定时间t'-t内，观察到从相空间中的一个点到另一个点的概率， 等于其逆过程的概率。

路径积分的构造：根据CK方程，写出维那过程（因为布朗运动更为严谨的数学定义又维那给出，所以又称为维那过程）的概率密度函数，化出泛函形式，把一般的朗之万方程代入，就得到了概率幅的路径积分构造，此时再考虑粒子走某条路径的概率，就有了大偏差定理的形式。

求解的时候需要用到平均场近似，等等一系列条件分析，不再深究。









