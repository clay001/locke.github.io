---
layout: post
title: "Python learning"
date: 2019-11-14 17:17:32
image: '/assets/img/'
description: 'Some knowledge about python'
tags:
- python  
categories:
- Language 
twitter_text: 'Do you know these?'
---

## Preface

Python is a very popular language, it is easy to learn and can make you get rid of  many annoying things. It is specifically suitable for data analysis, so it is widely used in research. However, lots of unscrupulous businessmen take advantage of this and offer many courses to teach python, and tell you that if you pay and take the lessons, which can give you a guarantee of high salary. I think is a waste of your money and mess up the supply-demand relationship in the market. Why? First you need to know about it, and then you will find the answer.

## some complaints :p

I think the current path of artificial intelligence can never lead to the ideal strong artificial intelligence which is like in the movie. The academia is drawing a giant pie, publish loads of "garbage paper" every year. 

In china like my school, even need every graduate student to publish a top class English paper, and you are just a graduate student, if you are not lucky encough, you will get no instruction from mentor professor or phd or even senior graduates. Even for a garbage paper, it is very painful.

I think the reason is some of the Chinese professors do not deserve to be a professor, and the academic education orientation is wired, make the students wasting their time to struggle, but do not focus on student ability development.

## if \_\_name\_\_ = \_\_name\_\_是什么意思

可以保证脚本在以模块导入的时候，不会自动执行最外层（函数定义以外）的代码

## Arg, *args, **kwargs是什么

arg是函数定义时候的形参

*arg表示传入多个但不确定个数的形参，实参传入后python会自动将其组织称元组的形式

**kwargs可以实现传入多个，但又不确定几个的键值对定义，实参传入后被组织成字典的形式

## map和reduce函数

map（function,iterable），需要注意的是，在python3.x中，这个函数返回的是一个迭代器，需要用list（）转换为列表的形式。它比循环写起来更简洁，而且它映射的过程是并行的，所以速度更快

reduce函数可以使各元素按顺序进行计算，每次计算结果也会参与到下次计算中，简单的例子比如实现累乘的功能，用reduce函数需要先import functools，然后用functools.reduce(function,iterable)

## 相对import和绝对import

\_\_main\_\_是入口文件中变量\_\_name\_\_的值，也是python中使用相对路径导入模块（from .a import *）中的 . 所代表的根路径，这样很容易找不到报错。所以在入口文件中应尽量使用绝对路径进行import。

## 前置单下划线

一般是在类内定义变量的名字，由于python中没有对public和private进行严格的定义，所以默认在看到前置单下划线的变量或者方法时，领会代码编写者的意图：最好只在内部使用，起到约定俗成的private的功能

## 后置单下划线

有一些名词，比如class，在python中属于保留关键字，那么如果我们想要定义一个class仅仅作为名字的变量，就可以在它后面加上一个后置单下划线来区分，仅仅是因为懒得想新名字而已哈哈

## 前置双下划线

类内如果用前置双下划线定义一个变量或者方法，那么这时候python内部会默认为其改变属性名称，如果想自己亲自看一下可以用dir(class_name)查看所有变量

改变名称的作用有二，一是可以使属性变量或者方法私有，不会被派生类继承，仅能自己使用，而是可以避免派生类和父类属性名称的冲突

## 前后置双下划线

比如我们经常看见的类内初始化函数\_\_init\_\_，python中通常把这种被前后双下划线包裹的方法称为魔法方法，他们会在类或对象的某些事件触发后执行。比如我们在实例化一个新类的时候，python会执行一个\_\_new\_\_（）的魔法方法生成一个实例对象，然后执行init魔法方法对对象进行初始化。

除此之外，python中的许多面向对象的操作都是靠魔法方法实现的，比如len求字符长度的时候，会调用类中内置的魔法方法等等

## 保持list顺序不变条件下的去重

转化为set可以去重，但是set是一个无序列表，如果想做到顺序不变，可以使用list_name.sort(key = list_name.index)，sort是在原位排序，依据是在原有序列表中各元素的index值

## 匿名函数lambda

基本结构是lambda argument_list: expression

这个函数在定义的时候只需要一行，而且调用也很方便，关键是逼格高，就喜欢写这种屌屌的代码嘻嘻，接下来写几个例子大家感受一下

```python
a = lambda x:x**2
print(a(2))           # 4

b = lambda x,y:x if x>y else y
print(b(1,2))         # 2

a_list = [lambda x:x.strip(), lambda x:x**2]
print(a_list)         # 返回函数指针列表
print(a_list[0]("xixi     "))   #xixi
print(a_list[1](4))   # 16

def main():
  return lambda x:x**2
print(main())        # 返回一个函数指针
print(main()(4))     # 16

```

## 全局变量和局部变量

区别就在于变量是定义在函数内还是函数外，即使重名，在函数内对变量的操作也不会对函数外的变量造成影响，如果想要在函数内操作并造成影响，那么需要在函数内事先声明global xxx，表明它是一个全局变量

还有一种比较奇怪的情况，就是一个函数里有一个局部变量，但是在这个函数里又包含了另外一个函数的定义，在后面这个定义中想要使用上一层函数中的变量，但它又不能算是全局变量，这时候声明就要用到nonlocal xxx，来清楚地界限它的地位

## 函数参数前的单* 和双**

*代表解包的操作，

## tensorflow 2.0

咕果，哈哈这个中国名字真的可爱，它更新啦！

之前我做深度学习的时候用的pytorch，tensorflow了解的不算多，但是最近感觉工业界用TF还是大势，而且信仰之厂的产品说什么也得学一下，刚好它出了2.0的大改版本，就去玩一下吧，感觉和以前的版本还真的有很多不同的，API做了很大的改动，这意味着很多原来的功能如果想要在TF2里实现，用TF1的代码是跑不通的（貌似有做兼容的工作，但都有2了干嘛还抱着1呢，反正我也没包袱哈哈）。（[这里有一份对照表](https://docs.google.com/spreadsheets/d/1FLFJLzg7WNP6JHODX5q8BDgptKafq_slHpnHVbJIteQ/edit#gid=0)）

TF2.0的核心功能是Eager execution（动态图机制），移除`tf.get_variable`, `tf.variable_scope`, `tf.layers`，强制转型到基于Keras的方法，也就是用`tf.keras`（好像是被TF收购了，keras被封装地更好，应该会更好用）。

