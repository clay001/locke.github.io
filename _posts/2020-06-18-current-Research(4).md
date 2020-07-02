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

sklearn中的所有方法在使用前都要进行fit，它是一个适配安装的过程，然后tranform进行标准化，降维，归一化的操作。fit_transform就是结合了这两部的操作的一个简化函数

## pd中的一些函数

在归一化的需要把训练数据和测试数据合在一起做，但之后又要分开，这里可以用ID来进行区分，取出的时候可以用merge函数，实质是表连接，这里用左连接就可以

mean函数求平均，sub做减法，div做除法，gt表示大于，abs求绝对值，mask函数把满足条件的筛除掉，where函数保留满足条件的（或者是用第二个参数替换掉），fillna函数替换掉NA值（method为ffill的时候用最后一个有效值去替换），to_csv保存为csv文件，drop函数扔掉特定的columns

dummies函数可以把类别变量变成indicator的变量，align函数用指定的连接方法（inner或者outer）在他们的轴上对齐

## sklearn的proprecess包

Imputer函数可以设置缺失值类型，填充规则等。然后再用设置好的参数去fit和transform。

PolynomialFeatures函数设置多项式构造特征的方法参数。然后同样需要fit和transform

## KFold交叉验证

平时我们会分成训练集和测试集（hold out留出法）来比避免在训练中出现过拟合的问题，但是小数据集上会浪费掉测试集的数据，所以用K折的方法来综合评判模型的性能

通常我们在进行划分的时候会记录下较为优异的超参数，然后再以最优参数进行重新训练

ShuffleSplit分隔函数是随机分隔。KFold().split(data) 会把数据分成train和valid两部分，里面有两部分数据的id。RepeatedKFold是多次K折。所谓留一法是满折时候的情况，有专门的函数LeaveOneOut，留P法的函数是leavePout，建议的K值是5或10。如果target的不均匀现象比较严重，可以在方法前面加上Stratified来修正。时间关联的数据有TimeSeriesSplit

model上用到了XGBRegressor，fit部分verbose指示多少轮打印，early_stopping_rounds指示早停轮数，eval_set以元组列表的格式给出评判数据集和它的标签

validation_curve可以画出曲线图

## Evaluate模型

```python
# MSE均方误差
from sklearn.metrics import mean_squared_error 
# MAE平方绝对误差
from sklearn.metrics import mean_absolute_error 
# R方
from sklearn.metrics import r2_score
# 准确率
from sklearn.metrics import accuracy_score
# 格式都是test，pred
accuracy = accuracy_score(y_test,y_pred)
print("accuarcy: %.2f%%" % (accuracy*100.0))
```

交叉验证模型的评估可以用 scores = cross_val_score( clf, iris.data, iris.target, cv=5, scoring='f1_macro')

Cross_validate方法在scroing部分可以传入列表或者字典，返回的字典格式为dict_keys(['fit_time', 'score_time', 'test_score', 'train_score'])

Cross_val_predict方法返回的是交叉验证之后的输出值

## bootstrapping自助法

基本思想是对于含有m个样本的数据集D，有放回地采样m次，得到一个会有重复数据的集合作为训练集，没有采样到的样本作为测试集

## XGboost和GBDT的区别

GBDT中预测值是由所有弱分类器上的预测结果的加权求和，其中每个样本上的预测结果就是样本所在的叶子节点的均值。而XGB中的预测值是所有弱分类器上的叶子权重直接求和得到，计算叶子权重是一个复杂的过程

xgboost的好处：

> 正则化： 代价函数里包含正则项，控制叶子结点个数和叶子结点输出的score的L2模的平方和
>
> 并行处理：在特征粒度上进行并行
>
> 灵活性：支持自定义目标函数和评估函数
>
> 剪枝：从顶到底建立子树，再反向剪枝，不容易陷入局部最优
>
> 内置交叉验证：允许在每一轮boosting中用交叉验证

## GridSearchCV

将需要遍历的参数定义为字典传入，n\_jobs是并行数，可以设置为-1与CPU和核数自动匹配。grid\_scores\_用于查看不同参数情况下的评价结果，best\_params_用于查看最佳结果的参数组合，best\_score\_提供最好评分。其他参数在命名和使用上都比较清晰

## 调参日记

```python
params = {
    'booster': 'gbtree',
    'objective': 'multi:softmax',  # 多分类的问题
    'num_class': 10,               # 类别数，与 multisoftmax 并用
    'gamma': 0.1,                  # 用于控制是否后剪枝的参数,越大越保守，一般0.1、0.2这样子。
    'max_depth': 12,               # 构建树的深度，越大越容易过拟合
    'lambda': 2,                   # 控制模型复杂度的权重值的L2正则化项参数，参数越大，模型越不容易过拟合。
    'subsample': 0.7,              # 随机采样训练样本
    'colsample_bytree': 0.7,       # 生成树时进行的列采样
    'min_child_weight': 3,
    'silent': 1,                   # 设置成1则没有运行信息输出，最好是设置为0.
    'eta': 0.007,                  # 如同学习率
    'seed': 1000,
    'nthread': 4,                  # cpu 线程数
}

训练完之后可以保存模型
dump model可以导出模型和特征映射
```

- General parameters
  该参数参数控制在提升（boosting）过程中使用哪种booster，常用的booster有树模型（tree）和线性模型（linear model）
- Booster parameters
  这取决于使用哪种booster
- Task parameters
  控制学习的场景，例如在回归问题中会使用不同的参数控制排序

算法的调优是一个从欠拟合到过拟合的过程，学习速率决定每一轮迭代训练集误差的下降速率，迭代轮数决定我们什么时候停止我们曲线的学习过程，所以有人建议这两个最后调。其他的参数重要性越高的越前调

在xgboost中，最重要的是max-depth，默认值为6，这个参数是每棵决策树的最大深度，一般这个参数越大，每一次迭代训练集误差下降的越快，因为树深度越大，每一轮对训练集的拟合程度也就越高。因此首先看这个参数在什么时候交叉验证集误差的最小值低且稳定。之后调整subsample和colsample_bytree，这两个参数分别代表构建决策树时的行抽样和列抽样，一般取值范围为[0.5,1]。最后调学习速率和迭代轮数

调参对于模型准确率的提高有一定的帮助，但这是有限的。最重要的还是要通过数据清洗，特征选择，特征融合，模型融合等手段来进行改进

## Hyperopt调参

之前知道Grid Search和Random Search，前者是全空间扫描，有些慢，后者容易错失一些重要的点，并且在调整第一个模型参数的时候也是用的Grid Search。

后来了解到一种通过贝叶斯优化（序贯模型优化，Sequential model-based optimization）的方法，Hyperopt。它结合MongoDB还可以进行分布式调参

传统调参的方法不是启发式的，但贝叶斯调参可以根据之前结果的验证情况来挑选下一次的迭代超参数。贝叶斯优化分为四个部分：目标函数，搜索空间，优化算法，结果。

实际操作下来发现对于小数据集并不是很稳定，而且有一些配合sklearn上的bug尚未解决，而且Hyperopt 设计伊始,是包括基于高斯过程与回归树的贝叶斯优化算法的,但是好像现在这些都还没有被实现

## 模型

ARIMA模型是传统统计学的，比较简单

RNN和LSTM Networks，还有Prophet模型

Xgboost参数介绍https://www.cnblogs.com/TimVerion/p/11436001.html

https://www.jianshu.com/p/1100e333fcab

LSTM代码https://blog.csdn.net/Muzi_Water/article/details/103921115

## 增量训练

如果数据量很大，通常做法是抽样训练多模型然后加权

但如果数据是偏态的，我们需要在之前就针对整个数据集做变换和异常处理。我们做特征变换，用到的主要是特征的最小值最大值，均值，方差，变异系数，k阶原点矩，k阶中心距，偏度，峰度等几个基本统计量，因此，我们需要算出每一个特征的这些统计量，在新的数据到来的时候，更新这个统计量，在训练模型之前，用全局统计量更新局部数据（抽样数据），以保证数据整体分布信息能够充分利用。

计算全量数据的统计量的时候内存容易不够用，这时候可以上spark+大数据集群。但如果只有有限的内存，训练的时候可以用SGD或者mini_batch SGD，方法上可以选择sklearn，原生lightGBM或者keras

## 特征选择

过滤法，包裹法和嵌入法。

过滤法：统计方法对特征进行评分和排序

包裹法：使用学习器的性能指标作为特征子集的评价准则

嵌入法：在训练的过程中自动完成特征选择

学生党建议造轮子，老油条可以使用的sklearn的feature\_selection模块




















