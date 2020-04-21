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

## Bagging和boosting的区别

bagging全称是boostrapping aggregation，是以采样为核心的，通重抽样来产生多个数据集，训练多个弱分类器来进行集成，针对预测任务就进行投票，回归任务就进行平均。比如随机森林，就是对行进行有放回的随机采样，列进行无放回的随机采样来有效降低过拟合现象。

Boosting是通过迭代来更改每个样本的权重，典型的算法有adaboost,GBDT

还有一种stacking的方法

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

## Kadane算法

解决最大连续子列和问题，从前往后扫描数组，每次加上当前值，如果有增益效果则更新cur_sum，如果没有就把cur_sum更新为当前值，同时每次都再维护一个ans对以前的ans和cur_sum去max

## 基于动态词表的对话生成

Neural Response Generation with Dynamic Vocabularies，北航和亚研院在2018年的AAAI上的文章。

## 分布式训练

在一些招聘的要求上面看到这一项技能，主要是一个使用并行计算的能力。在pytorch中有提供的DataParallel。分一机多卡和多机多卡。

## 降维

现在大数据越来越随处可见，降维是必须的，它可以减少数据的存储空间，节省模型的计算时间，提升某些算法的表现，去除冗余信息，可视化数据。

降维一般有两种思路，一种是剔除（特征选择），一种是组合（也就是我们常说的降维）

1. 缺失值比率，计算公式为train.isnull().sum()/len(train)*100，把缺失值较高的一些特征直接用阈值筛掉
2. 低方差过滤，计算特征的方差，把较小的特征筛掉
3. 高相关过滤器，如果两个变量高度相关，那么会降低某些模型的性能（比如线性回归和逻辑回归）。所以需要计算变量之间的相关性，如果相关性大于0.5-0.6，我们可以随机丢弃其中的一个
4. 随机森林，scikit-learn中有写好的实现，可以得到特征的重要性排序
5. 反向特征消除，如果说一共有n个变量，先用所有变量计算出模型的性能。然后重复顺序消除一个其中变量去训练模型，丢弃使得性能损失最小的变量。直到不能删去任何变量为止，sk-learn中也有相关实现（使用“ rfe.ranking”命令检查变量的排名）
6. 正向特征选择，反过来，刚开始用一个效果最好的特征去训练，然后每次增加一个使得性能提升最大的特征。f_regression能返回一个包含特征的F值和p值的数组，一般选取F大于10的
7. 因子分析，变量按相关性进行分组，组内特征具有较高的相关性，组间相关性较低，一个组成为一个因子。FactorAnalysis可以指定分组的数目
8. PCA主成分分析，主成分依次解释数据集中的最大方差，explain_variance_ratio来表示主成分的重要性，还可以把它可视化出来。还可以用SVD分解，用特征值和特征向量来把它分解为三个组成矩阵，truncatedSVD
9. 独立成分分析（ICA），寻找独立因素。该算法假设给定变量是一些未知潜在变量的线性混合。它还假设这些潜在变量是相互独立。
10. 基于投影的方法，有两种，一种是投影寻找最大化投影值的峰度的方向，作为非高斯性的度量。一种是流形嵌入（isomap），它假设两点之间的测底线距离等于欧式距离，先计算点对之间的距离构造一个邻接矩阵，确定流形的相邻数据点，用最邻近算法形成邻接图G。我们在G上可以计算两点之间的最短路径，用来当作流形中的测底线距离。对内积矩阵进行特征值分解。
11. t-SNE, 能够以非线性的方式保留数据本地和全局结构，最小化高维空间和低维空间的相似性条件概率。
12. umap，运行时间更短，用k邻近的概念，用随机梯度下降来优化差距

## Linux命令

｜是管道符，grep -v 不显示匹配上的内容，-n 显示匹配上的内容

du（disk use）显示每个文件和目录的磁盘使用空间，df（disk free）显示磁盘空间上可使用的磁盘空间

统计文件中字符串次数：

grep NullPointerException(或者字符串)  文件名字｜wc -l（按行统计）

find /xxx/xx -name \*.log | wc -l   或者 ls /xxx/xx/\*.log | wc -l 

## Clean Code

统一的插件，模版，遵循比较主流的开发者规范（google和阿里）。主要的原则有去除重复代码，去掉过长的方法，去掉不必要的注释和main方法，合理设置变量和方法的属性，清除IDE提示的代码问题，使用稳定的第三方包进行简化等等

## 单例模式

假如很多地方都需要使用配置文件的内容，会导致系统中存在多个AppConfig的实例对象，单例就是只有一个对象。

## DIoU损失函数（2020AAAI）

交并比损失函数，在目标检测任务的边界框回归上有显著的效果

## CI,CD&CD

CI是持续集成的意思，开发人员会频繁地提交代码到主干，这些新提交在最终合并到主线之前，都需要通过编译和自动化测试进行验证

CD&CD的第一个CD是持续交付的意思，多了一步自动化的发布流，每天每周或者每两周发布；第二个CD是持续部署，只要在工作流中能够构建成功，就会自动被部署到产品线上和用户见面

CI/CD工具可自动完成构建，测试和部署新代码的过程

## 中间件

将具体业务和底层逻辑解耦的组件

## 产品方面的前期准备

用户研究经历，公众号运营经历，设计的产品demo

制作一个产品作品，对公司的产品写一些竞品分析，产品体检报告

花时间设计产品，前期用户调研，市场分析，产品定位，写MRD市场需求报告，需求分析，需求排队，产品架构设计，产品原型设计，写出PRD产品需求文档，画出完整的产品原型交互稿

快速抽象出产品的核心设计框架逻辑，学习优缺点，对公司写报告，发表在社区上

运营公众号，运营公众号可以反映映产品定位、用户分析、数据分析、产品策划、产品推广等能力，运营了一个用户量几千以上的公众号是加分项

## FCN的实现和注意事项

计算softmax loss时要用数值的方式

softmax与 loss可能要分开计算. 得到前者的计算方式可以是常规方法. 但计算后者时要注意无穷大和NaN的出现.

NAN一定是因为出现了无穷大. 无穷大的出现则是因为变量存储的数值超出了变量数据类型能表示的最大值.使用GPU计算常用float32, 它的最大表示值在10的38.51038.5次附近.

learning_rate太大可能导致NAN的出现: weight值会变得很大(超过10应该就算大了). 在forward的过程中会不断乘以weight值, 这样就会导致神经元的激活值达到无穷大。然后, 只要碰到值为0的weight(小概率)或与其他的无穷大, 就会出现NaN.

像素级别的loss的取均值决定learning_rate的数量级. 我使用224×224的图片, 如果loss是对单个像素的均值, 则数量级在10的−5. 如果是对单张图片的loss, 要再小4个数量级.

loss不降的时候，先尝试用更小的lr，再尝试用大的，因为大的lr也可能会使wight set落入一个更好的basin

## PCA的劣势

1. 在对数据完全无知的情况下效果不太好，因为PCA需要对数据进行预处理，进行中心化和标准化，如果有噪声的话会有比较大的误差
2. 对于隐变量的数目不能很好地估计
3. 非线性的数据关系有可能被丢失
4. 如果数据不服从高斯分布的话，会发生尺缩和旋转

## Zero shot learning

是指基于样本，训练网络对物体属性的感知，从而对没有见过的物体进行分类，比如学习了马和老虎，希望它能正确分类出斑马



## VAE做预测











 