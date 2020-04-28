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

## 先说一个技巧 

在pycharm里的时候写代码，写完以后想把它统一的变成比较漂亮的形式的时候，可以用快捷键Ctrl+alt+L 

## if \_\_name\_\_ = \_\_main\_\_是什么意思

可以保证脚本在以模块导入的时候，不会自动执行最外层（函数定义以外）的代码

## 相对import和绝对import

\_\_main\_\_是入口文件中变量\_\_name\_\_的值，也是python中使用相对路径导入模块（from .a import *）中的 . 所代表的根路径，这样很容易找不到报错。所以在入口文件中应尽量使用绝对路径进行import。

## list保序去重

转化为set可以去重(例如`a1 = list( set(list_name))` )，但是set是一个无序列表，得到的列表是不保序的，如果想做到顺序不变，可以使用`a1.sort(key = list_name.index)`，sort是在原位排序，依据是在原有序列表中各元素的index值

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

## arg, *args, **kwargs是什么

arg是函数定义时候的形参

*arg表示传入多个但不确定个数的形参，实参传入后python会自动将其组织称元组的形式

**kwargs可以实现传入多个，但又不确定几个的键值对定义(类似 student = "学生")，实参传入后被组织成字典的形式

## 全局变量和局部变量

区别就在于变量是定义在函数内还是函数外，即使重名，在函数内对变量的操作也不会对函数外的变量造成影响，如果想要在函数内操作并造成影响，那么需要在函数内事先声明global xxx，表明它是一个全局变量

还有一种比较奇怪的情况，就是一个函数里有一个局部变量，但是在这个函数里又包含了另外一个函数的定义，在后面这个定义中想要使用上一层函数中的变量，但它又不能算是全局变量，这时候声明就要用到nonlocal xxx，来清楚地界限它的地位

TIPS: \# 在实践中我发现了一个神奇的设定，在python中外部的变量可以不传入函数而进行引用。但是不能不传入修改，这样会报错。可以重定义，但此时就是新建了一个局部变量，不更改外部变量

## 变量间的引用和赋值

传递机制分为值传递和引用传递，值传递传递实际参数值的一个副本，常见于不可变对象的传递（int，str，tuple）

引用传递会传递参数值的地址，原位修改，常见于可变对象（list，dict）

对一个变量a，可以用id(a)来查看它在内存中存储的位置，比如a是一个数组，命令b = a，此时a和b都指向这个数组，如果重新给a赋值，系统会重新给a分配一块空间，但是如果用切片操作的方法改变a数组里的值，那么b也会相应地被改变，如果这不是我们想要的，就会造成变量的混乱

## 深复制和浅复制

浅复制，先import copy，然后用形如b = copy.copy(a)的语句进行复制，这时候系统会为其新开一块内存空间，普通的操作并不会同时改变两个变量的值，但是如果变量中包含子对象的时候，浅复制仅仅采用引用的方式对其处理，比如a数组中存在嵌套数组的情况，那么改变这个子对象的时候就会同时改变两个变量中的对应值

深复制就可以避免这种问题，b = copy.deepcopy(a)

## 关于变量和指针

假如不用copy函数，直接用变量的传递b = a，那么只有在直接存储数字的时候才不会受影响，比如存储列表的时候对一个的改变都会影响另外一个。

这是因为计算机列表变量存储的其实是头位置的指针，指针也拥有自己的内存空间，假如a = [1,2]，如果对a取地址，取到的是a这个指针所在的内存地址，a[0]取地址才是它指向的空间所在的头地址，这时候我们让b = a，是让b也指向了a指向的位置，b指针的地址和a指针的地址也是一样的，对a指向的空间作出改变之后，b由于也是指向同一片区域，所以也会跟着改变

## map和reduce函数

map（function,iterable），需要注意的是，在python3.x中，这个函数返回的是一个迭代器，需要用list（）转换为列表的形式。它比循环写起来更简洁，而且它映射的过程是并行的，所以速度更快

reduce函数可以使各元素按顺序进行计算，每次计算结果也会参与到下次计算中，简单的例子比如实现累乘的功能，用reduce函数需要先import functools，然后用functools.reduce(function,iterable)

## 切片操作

[起始索引值：结束索引值：步长] 默认为[0: -1 : 1]  (区间左闭右开)

## generator生成器

```python
mylist = [x*x for x in range(3)]  
print mylist

output:
[0, 1, 4]#这是列表
```

```python
mygen=(x*x for x in range(3))  
print mygen  

output:
<generator object <genexpr> at 0x052E8210>#这就是生成器generator和一个内存地址

# 可以这么用
for i in mygen:  
    print (i)  

output:
0
1
4
```

上面的用法就体现了“要用再算”的思想。

如果有一个很大的列表，只需要访问前某几个元素，或者我们要存储一个本身有无穷项的数列（斐波那契数列），不确定长度，无法进行初始化。这时候我们就可以用generator来再需要的时候再产生结果（延迟操作）

```python
def fib(max):
    n,a,b = 0,0,1
    while(n<max):
        yield b
        a,b = b, a+b
        n += 1
        
for n in fib(15):  
    print n  
```

一个带有yield命令的函数就是一个生成器，它和普通函数不同，生成一个generator看起来像函数调用，但是却不会执行任何函数代码，直到对其调用generator.next()才开始执行, 在循环中会自动调用next()。每执行到yield语句就会中断，并且返回一个迭代器，下次执行的时候从yield的下一个语句继续执行，看起来就像一个函数被中断了数次，每次中断都会通过yield返回当前的迭代值。

## 过滤器

filter可以过滤掉可迭代对象(dict，list)中不符合条件的元素

filter( lambda x:x%2 == 0, a) 它返回的是filter object，我们需要在外面再套一个list() 进行转换

## 可变对象和不可变对象

区别在与会不会在原来的内存地址中对值进行修改，不可变对象有（int, float, str, tuple）会在一块新的内存区域创建新值，老值的内存会被python当成垃圾处理掉。

可变对象有（dic, set, list），他们只会在原内存地址内进行修改

## 字典和集合的生成器

```python
# list
a = [x for x in range(10)]
# set
a = {x for x in range(10)}
# dic
# key is x ; value is after : thing
a = {x:x%2 == 0 for x in range(10)}
```

## 变量快速交换

在python中可以直接用 a,b = b, a 的语法进行元素间的快速交换，再更多的变量也是同理，我觉得可能是因为python语言底层在每一行的时候会保存之前的变量值，而同行的操作是同步的，所以在python中是合法的，a变量的值不会丢失

## zip函数实现高效遍历

当要遍历一个以上的列表的时候，可以用 for i , j in zip(a,b)的写法

zip函数会将列表按位组合成元组，如果列表长度不同的话，只会输出最短长度个的元组

## sort和sorted

sort是列表内置的函数，假如a是一个列表，可以用a.sort()来进行排序，更一般的，可以用a.sort(key = lambda x:x[1], reverse = True)这些参数来控制函数的行为，操作会直接对a进行改变

sorted是python语言内置的函数，所以不止list，所有可迭代的数据结构都能用sorted函数，返回的是一个列表副本，不会对原来的对象进行修改。如果对象是字典，那么如果参数只写dic，返回的将会只有字典的排序键值，所以正确的使用格式是sorted(d.items(), key = lambda x: x[1], reverse = True)，items把键值和value打包成一个元素为元组的列表（其实严格来说是dict_items），这样返回出来的东西也是一个元素为元组的排序后的列表

## is和==运算符的区别

对象的三个基本要素：id内存地址，type数据类型，value值

== 比较的是值，is比较的是id

## eval(expression, globals = None, locals = None)

python的内置函数，作用是将字符串当成有效的表达值来求值，并且返回计算结果

可以将包含列表，字典或者元组的字符串转换回原来的数据类型，因为读入的时候是以字符串读入（比如一些网络响应返回的数据包）

 后面两个参数是全局变量和局部变量，以字典的形式传入`rst = eval('a+1',{'a' :2},{'a':3})`，python查找变量的顺序是先局部，后全局，最后内置（优先级覆盖）

## python中的链式比较

1<2<3理解成 1<2 and 2<3

False is False is False 理解成 （False is False）and (False is False)

从中间开始扩散，中间用and连接

## 字符串拼接

join函数的效率比+高很多，因为字符串是不可变对象，每次使用+=都会生成新对象，而join会先计算结果所需的内存，然后一次性申请，最后把每个字符串复制过去，没有中间字符串的生成

## （and，or）和 （&，｜）

当运算对象为逻辑变量的时候没有区别

对象为数字的时候，前者返回比较，后者返回按位操作的结果

如果对象混合，那么（&，｜）会把True，False认为是1和0再进行逻辑与或运算

## 交集，并集，差集

集合{} 

 并集｜        交集 &        差集 -         对称差集  ^ (两个集合中不重合的部分)

如果是列表，就先转换为 set()

## 生成随机数

import random 

random.random()  随机输出 [ 0.0,1.0 ) 的浮点数

random.randint(1,10)   输出 [ 1, 10 ] 的整数

random.randrange(1,10)   输出 [1, 10) 左闭右开的整数

random.uniform(1,10)       [1.0 , 10.0 )的浮点数

random.choice(a)      a可以是一个列表，会在index里随机选一个输出    

random.choices (a, [weight1,weight2 ...], k )  可以为列表中的index指定权重，或者是累积权重cum_sum = [weight_t1, ..... ]，k是选择的个数

random.sample (a , k)     取样, 不会重复

## any函数和all函数

any函数用于判断可迭代对象中是否包含（0，“”，False）之外的元素

比如print( any( [0,"",1] ) )返回的是true

all函数用于判断是否可迭代对象是否全部都是（0，“”，False）之外的元素

## 格式化输出

如果a是一个字符串，我们经常用的就是print( "out:" + a )

还可以用%占位，print( "out:%s" %a ), 这时候即使a不是一个字符串，而是数字，列表也一样可以进行转换，但元组不行。元组得写成%（a，）才可以。

这时候可以用一个更强的格式化输出，print( "out:{}".format( xx ) ), 更进一步，还可以控制输出的顺序，print( "out:{0}  b={1}".format(a,b) ) 或是print( "out:{0}  b={1}".format(*c) ) ， c可以是元组和列表和字符串，\*是解包的操作。如果是字典，则单星号解包的元素是key值，双星号解包的元素才是value值。在py3中，可以直接写成print( f"out:{a}  b={b}")来进行填充

其他格式的输出，比如整型，浮点数，%.2f两位小数，%5.2f 占位宽度，%-5.2f占位左对齐等等

## try/except/else/finally异常捕获

如果一个语句有可能发生错误，但又不想后面的程序因为它不能执行，可以把它放到try里，再在except里输出程序在这里发生了错误即可。还可以用except KeyError等更细致地捕获异常，最后因为你不太可能捕获所有的异常，所以一般会加上except Exception来做补充。

后面还可以跟一个else，用来提示语句没有错误，异常没有捕获。

finally则是不论如何都会进入执行的语句

## del关键字

在C++中用于释放动态分配的内存，内存释放后，该区域内存储的值也被删除

但在python中，del关键字并不会去操纵内存，而只是删除了变量的引用，python中内存的释放是由garbabe center（GC）处理的，当某块内存的引用变为0的时候才会被当成垃圾被回收

标记-清除机制：平时先按需分配，等到没有空闲内存的时候，从寄存器和程序栈上的引用出发，遍历以对象为节点，以引用为边构成的图，把所有可以访问到的对象打上标记，然后清扫一遍内存空间，把所有没有标记的对象释放

分代技术：将系统中所有内存块根据其存活时间划分为不同的集合，每个集合就成为一个代，垃圾收集频率随着代的存活时间的增大而减小

## 解释性语言和编译型语言

编译型语言在执行之前需要进行编译，高级语言如c会被编译成所在平台对应的机器语言（obj），最后包装成该平台的可执行文件（exe）。这种语言效率高，执行速度快，适合开发操作系统，数据库等应用

解释性语言没有编译的过程，每次运行时才被解释器解释成机器语言，效率稍低，适合开发网页脚本，服务器脚本等

## python的解释器

运行代码时候的解释器会不断地将代码翻译成机器所能理解的机器语言，最常用的解释器是Cpython，此外还有基于Cpython之上的交互式解释器Ipython，运行在java平台上的Jython，运行在微软.net平台上的IronPython，以及使用rPython实现的Python（也就是Pypy，运用JIT技术，对代码动态编译，大大提升了代码的速度）

## sum函数

```python
a = [1,2] 
sum(a)  # 为3
sum(a,1) # 为4

a = [1,2] *3
# a = [1,2,1,2,1,2]

a = [[1,2]]*3
# a = [[1,2],[1,2],[1,2]]

# 如果我们想要展开它
print([i for k in a for i in k])
# [1,2,1,2,1,2]

# 还可以用
sum(a,[])
# 就相当于用加号进行计算，但是字符串不行，字符串得用"".join(xx)
```

## a+=b和a=a+b

对于数值计算，两个是等价的

如果对于可变对象，那么前面的操作是在a的原内存空间操作，后者则是新开辟了一块内存空间

很神奇的一点就是，如果a仍然是个列表，但b是个元组，这样前者不会报错，而后者会。因为对象的相加运算背后有两个魔法方法（\_\_iadd\_\_和\_\_add\_\_），可变对象背后两个都有，但不可变对象背后只有后者。有iadd方法优先调用iadd方法，iadd方法是用extend实现的，所以列表和元组可以合并

ps: 对于list，我们都知道+，是同为列表之间的合并。append，它是把需要加的对象不改变数据结构原模原样地加。extend则是会将其强制变为list，再执行想加操作

## for搭配else

如果我们在for循环中有一个判断，如果进入了就break，然后运行接下来的程序，我们想要知道上面的循环是否正常执行完了，那么通常我们会设一个flag来判断，其实也可以在后面接上else，如果前面所有循环都进行完了，那么就会进入这个else，如果没有，那么就不会

## ==判断

python中整型和浮点型是如果值相同，==是True，所以如果一个字典中既包含了整型又包含了浮点型的key，如dic = {1:2, 1.0:3}，dic会通过检查键值和哈希值是否相同来确定两个键是否相同（hash(1) == hash(1.0)），所以会依次覆盖

## 类和对象

类是把有相同属性和方法的对象都归在一起，对象是从类中实例化出来的

## 类的定义和调用

```python
class Hero:
    def __init__(self,chinesename,slogen):
        # 实例变量（成员变量）
        self.chinesename = chinesename
        self.slogen = slogen
 
     # 实例方法 
    def flash(self):
        print(self.chinesename + ":闪现")
    
    
Arthur = Hero("盖哥","德玛西亚")
Arthur.flash()       #在调用方法的时候会自动把对象的指针传入
print(Arthur.__dict__)  # 用于查看它所有的实例变量值
```

## 类变量，实例变量和局部变量

```python
class Hero:
    # 类变量
    game = "hahaha"
    
Arthur = Hero() 
print(Arthur.game)  
# 此时对Arthur.game进行修改，只是改变了对象新建的实例变量
# 实例变量用对象访问，类变量有被实例对象copy到实例变量一份，但想要访问最原始的类变量，还是要用类名进行访问
# 局部变量是在类内的方法里定义的
```

## 实例方法，类方法，静态方法

```python
class Hero:
    # 类变量
    game = "hahaha"
    
    # 类方法
    @classmethod
    def heal(cls):
        print(cls.game)
    # 如果想在类方法中访问实例变量，只需要把实例传入即可
    # def heal(cls,Arthur)
    
    # 静态方法，无默认的形参
    @staticmethod
    def ignit():
        print("fire!")
        # 如果需要使用类变量，直接用
        print(Hero.game)
        # 如需使用实例变量，需要传入实例变量的指针
    
Arthur = Hero() 
# 类方法实例对象和类都能调用
Authur.heal()    #Hero.heal()  
# 静态方法也是对象和类都能调用
Arthur.ignit()   #Hero.ignit()
```

总结：实例方法只能实例对象调用，其他两个方法类和对象都能调用，且三个方法都能实现对类变量和实例变量的调用

## 继承

把一个类中定义的属性和方法复用到另一个类中的过程就是继承

继承后的类称为子类，或者派生类

继承前的类称为父类，或者超类

```python
# 之前我们定义过Hero类
# 现在我们可以直接继承它
class AD(Hero):
    slogen = "xxx"
    def Q(self):
        print("biu biu biu")
ashe = AD()
```

## 继承中的构造函数

如果子类没有重写init，会直接继承，如果重写了会以子类为准。也可以在子类中用Hero.\_\_init\_\_(self,参数)来调用，然后额外再做新初始化的添加。

还可以在子类中用super( AD, self ).\_\_init\_\_(参数）来实现。super相当于向上寻找一个父类

## 多继承

如果是按照一步步划分的话可能会产生很多不必要的类，我们可以把各种限定类都事先定义好，然后在后续继承的时候，一次性多继承几个。这样很清晰，但是相应的也会多产生一些bug

## 函数指针和闭包

```python
def temp(x,y):
    def add():
        print(x+y)
    return add
temp(4,2)()
```

为什么返回内层函数的函数指针，还能访问的到x和y呢？因为当内层函数调用了外层函数作用域中的变量时，外层函数调用结束后，将会把内层函数涉及到的变量“送”给内层函数以保证其正常运行，这就是所谓的闭包

（闭包 = 函数块 + 创建它时的环境）

closure是函数式编程的重要语法结构，也是组织代码的结构，提高了代码的可重复使用性

## 装饰器

在不改变函数内部代码的情况下，为已经存在的对象增添一些新的功能。经常被用于有切面需求的场景（AOP），较为经典的场景有插入日志，性能测试，事务处理等。

```python
# 介绍一个嵌套函数的装饰器
# 它可以用来给函数运行时间计时
import time
def out(fun):
    def In():
        start = time.perf_counter() #time.clock()
        fun()
        end = time.perf_counter() #time.clock()
        print("函数运行时间为: " + str(end - start))
    
    return In

def append():
    a = []
    for i in range(100000):
        a.append("haha")

# 把append函数闭包包装一下，返回一个函数指针
append = out(append)
append()
```

相当于append函数有自己的功能，但又不想把计时功能直接写进去，就另外写了一个装饰器，要用这个功能的时候用装饰器装饰一下。或者是当一百个函数都要计时的时候，就不用一个个加代码了，直接调用装饰器即可。

为什么这里还用到了闭包嵌套In函数呢？这是为了不仅仅是实现计时的功能，而且是返回了一个新的加上计时功能的装饰后的函数指针

python中还提供了一种非常方便的写法，append = out(append)这种装饰操作还可以直接用在append函数的定义上方写上@out（装饰器名）来替代

## 装饰器的参数传递

值得注意的是如果要装饰的函数有多个参数，也需要在装饰器中进行修改相应的传入操作。这时候联想到之前学过的*args, 我们可以把装饰器和需要装饰的函数都使用args来解决这个问题。

装饰器也可以在@的时候传入参数，这时候需要考虑传入参数的接收问题，可以再在装饰器外面套一层定义一个形参来接收

## 多个装饰器的执行顺序

先@装饰器a  ，再@装饰器b，然后再是函数

和套箱子📦是一个原理，每套一层就产生一个新的函数，所以修饰的时候是从下往上修饰（先b再a），调用的时候是先a再b

## call魔法方法

类和函数都是可调用对象，实例对象是不可调用对象，可以用callable（）来验证

call魔法方法和init类似，可以让实例对象能够像函数一样加小括号可以调用

`def __call__(self,*args,**kwargs):`

## 类装饰器

类装饰器也可以实现嵌套函数装饰器的效果, 通过实例化一个类来生成一个函数，类内有call转换为可调用对象

```python
import time
class Caltime:
    def __init__(self,fun):
        self.fun_ = fun
    
    def __call__(self,*args,**kwargs):
        start = time.perf_counter()
        self.fun_(*args)
        end = time.perf_counter()
        print(f"函数的运行时间为: {str(end-start)}")

@Caltime  # append = Caltime(append)
def append():
    a = []
    for i in range(100000):
        a.append("haha")    
        
append()
```

## 装饰类的装饰器

之前说的两种方法是装饰器的实现，都是用来装饰函数的，那么类可以被装饰吗？

```python
# 当然可以
def decorator(cls):
    cls.name = "microsoft"
    cls.slogen = "I am coming"
    return cls

@decorator
class person:
    pass

person.name
```

## 前置单下划线

一般是在类内定义变量的名字，由于python中没有对public和private进行严格的定义，所以默认在看到前置单下划线的变量或者方法时，领会代码编写者的意图：最好只在内部使用，起到约定俗成的private的功能

## 后置单下划线

有一些名词，比如class，在python中属于保留关键字，那么如果我们想要定义一个class仅仅作为名字的变量，就可以在它后面加上一个后置单下划线来区分，仅仅是因为懒得想新名字而已哈哈

## 前置双下划线

类内如果用前置双下划线定义一个变量或者方法，那么这时候python内部会默认为其改变属性名称，如果想自己亲自看一下可以用dir(class_name)查看所有变量

改变名称的作用有二，一是可以使属性变量或者方法真正私有，不会被派生类继承，仅能自己使用，二是可以避免派生类和父类属性名称的冲突

## 前后置双下划线

比如我们经常看见的类内初始化函数\_\_init\_\_，python中通常把这种被前后双下划线包裹的方法称为魔法方法，他们会在类或对象的某些事件触发后执行。比如我们在实例化一个新类的时候，python会执行一个\_\_new\_\_（）的魔法方法生成一个实例对象，然后执行init魔法方法对对象进行初始化。

除此之外，python中的许多面向对象的操作都是靠魔法方法实现的，比如len求字符长度的时候，会调用类中内置的魔法方法等等

## repr函数和\_\_repr\_\_魔法方法

repr函数和str函数类似，都是python内置的函数，都是转换为字符串，但str面向的是用户，repr则更容易被解释器接受

我们使用一个类的时候，假设为a object，使用print（a）的时候其实就是调用了\_\_repr\_\_的方法，如果没有特别进行编写的话会输出这个object的信息，如果进行编写了，可以输出你指定的字符串。（ps：在py3.6之后出现了f-string的格式化字符串方法，用{ }来提示需要被替换的内容）

## abs函数

这里扩展到复数范围就是取模的操作，一个数的复数的模等于实部和虚部的平方和再开方（调和平均），虚数用j来表示，如1+2j

## 单下划线的用法

可以表示丢弃不想要实际接收的变量

## #coding=utf-8

解释器会对代码中的每一行，包括注释都进行句法分析，所以不是只要带了#开头的就是注释，这里的作用是告诉解释器你用的编码方式，python2默认使用的是ascII编码，所以如果不加这个用中文的话就会报错，py3没有关系

## 大数字中的单下划线

不影响数字本身，只是增加代码的可读性，比如10_000_000这样

如果想在输出的时候也是用下划线进行分割的话，可以用print("\{:\_\}".format(100000)), 如果是其他进制，比如16进制则用print("\{:\_x}".format(0xFFFFFFFF)), 八进制{:_b} （十进制默认隔三位，其他隔4位）

括号里的数字可以是任意进制，但必须格式规范，比如16进制用0x提示

## 类型提示

就是在定义函数的时候def flash(xxx ), 里面的参数如果不带类型提示的话，如果xxx我们计划它是一个布尔类型，但是我们传入的时候用字符型，那么即使字符的内容是False，也会被判断为真，这时候可以在参数后加上类型提示def flash(xxx:bool)，这只在编译器中会提示，并不能像C一样做到真正意义上的把控。

返回值也可以提示,如def flash(xxx:bool)->int :

## help函数

查看文档，如果想要看某个函数的源代码，就用ctrl + 鼠标左键

这个help输出的其实就是这个源代码前面的'''xxxx'''多行注释，因此如果要规范代码的话也可以这么去写（函数，类，模块都适用）

## 单* 和双**

在函数申明中出现*，起到打包的作用，变量会被重新打包成元组，**会打包成字典

语句中*代表解包的操作，如果后面跟一个列表，集合，元组，会将之为拆分为单个元素，如果字典用单\*号只会取出键。如果后面跟的是字符串，那么会把它拆成一个个字母。  **对应字典，解包后就变成a = 0， b= 1的格式

## 数组

python中的如果用[ ]定义，定义出来的是一个列表，它和数组还是有一定区别的，列表可以支持不同类型的元素在一起，而数组不行，但数组是连续存储的，更加高效，内置方法则与list基本一致。

想用数组可以用from array import array，a= array()，更强大的，可以用numpy中的ndarray（）

## python中的队列

import queue，有full，empty，put和get函数。 （qsize，clear...)

- d = queue.Queue()遵循FIFO
- LifoQueue.LifoQueue() 遵循LIFO
- PriorityQueue.PriorityQueue()

定义的时候括弧里可以定义队列的大小,不指定就是动态的

上面涉及到了优先队列，它按照优先级出队，优先级的选择过程是用堆实现的，所以这里补充一下堆的知识，堆是用数组实现的二叉树，分为最大堆和最小堆 import heapq, heapq.heapify( listname )可以用O（N）的复杂度把列表转化为堆，一般heap[0]是最小的元素（最小堆）, heapq.heappop(heapname)可以弹出元素, heapq.heappush( L, xxx )用于插入元素。

heapq.nlargest(k, nums)会返回k大的列表，如果要取出第k大，就切片[-1]即可

常用的方法：

task_done() 意味着之前入队的一个任务已经完成，由队列的消费者线程调用，通常在get等一系列处理之后调用

join() 阻塞调用线程，直到未完成的任务数降到0之后，调用接触阻塞

put(item[, block[, timeout]]) 后面的默认参数是阻塞调用和超时情况。默认为true，false等同于put_nowait()。塞入一个数据

get( [, block[, timeout]]) 从队列中返回并移除一个数据

empty() 判断是否为空

## collections

这是一个内建的集合模块，里面有一些非常好用的功能

https://www.liaoxuefeng.com/wiki/1016959663602400/1017681679479008

- deque：list的访问很快，但是插入和删除很慢，deque是双向列表，能使得插入和删除都变得高效，栈和队列的功能都可以实现，因为它除了pop和push之外，还支持appendleft和popleft

- OrderedDict: 顾名思义，key是有序的，有序指的是保持插入顺序，用OrderedDict( [ ] )定义，里面是一个列表，列表里的键值对以元组的形式插入

  在dict中，我们可以调用.items()来遍历元组对，有序字典是字典结构的一个子类，所以也继承有个功能，此外还可以用move_to_end(key)和popitem()来对键值对的位置和删除进行操作，里面有一个参数last非常重要，当last默认为True，就是LIFO的机制（栈），如果想要队列功能的话就应该把这个值设为False

- Counter：初始化在无参数的情况下就是空类，还可以直接传入可迭代对象创建，字典创建和从等号连接的键值对创建。当访问键不存在的时候，返回0，否则返回它的频数。增加用update，减少用subtract，删除用del，elements()返回一个包含重复频数的键值的迭代器。most_common()返回一个按频数排序的列表，（）里可以传需要top N的数字

## 并查集回顾

并查集是一种用来管理元素分组情况的数据结构，在查询两个元素是否属于同一组和合并两个元素所在组的操作上很方便。其实现也是用树结构实现的，查询的时候看元素的根节点是否一致。为了合并的时候树型结构尽可能地平衡，还需要记录一下每颗树的高度，在合并的时候从高度小的向高度大的连边，在查询的时候还可以把路径上的点都指向根节点来压缩路径。

树的存储用字典实现，还需要编写一个find函数和一个union函数

```python
#不断地向上找根
def find(x):
	f.setdefault(x, x)  #当键不存在的时候才设置
  if f[x] != x:
 		f[x] = find(f[x])
  return f[x]

# x的根指向y的根,所以是把x连到y上，这个顺序很重要
def union(x, y):
	f[find(x)] = find(y)
```

这里插一句，在网格上遍历的时候可以按照网格的index值作为键值，因为遍历有顺序所以只需要合并一下该位置的左边和上边就可以了。

## bisect模块

之前提到过sort是在原位排序，bisect.insort(list, number)会在原位插入number保持有序的列表。bisect.bisect(list, number)不会直接改变列表，返回的是插入的位置（其中bisect_left和bisect_right，insort_left和insort_right是针对列表中有重复值的情况，分别使用左端插入和右端插入的原则）

## remove函数

list.remove(x)是用来删除元素用的

## python是如何进行内存管理的

从三个方面来说，一是对象的引用计数机制，python内部使用引用计数来保持追踪内存中的对象。比如为对象分配一个新名字，将其放入一个容器中都会增加计数；用del语句对对象别名的销毁等会减少计数。sys.getrefcount()可以查看引用计数。对于不可变对象，解释器会在程序的不同部分共享内存，以便节约内存。

## 垃圾回收

引用计数归零的时候会被垃圾收集处理机制处理掉，当两个对象a和b相互引用的时候，引用计数不会归零，对象也不会被销毁，这样就会导致内存泄露，为了解决这个问题，解释器会定期执行一个循环检测器，搜索不可访问对象并删除它

## 内存池机制

python中的垃圾收集机制将它不用的内存放到内存池，而不是返回给操作系统。pymalloc机制是为了加速python的执行效率而引入的内存池机制，用于管理对小块内存的申请和释放。python中小于256个字节的对象都适用pymalloc实现的分配器，大对象用系统的malloc。对于python对象，都有其独立的私有内存池，如果你分配又释放了大量的整数，用于缓存的内存是不能再被分配给浮点数的

## lambda函数的好处

通常是在需要一个函数，但是又不想去费神命名一个函数的场合下使用

## 删除一个list里重复元素的方法

有一个列表a，可以用set函数，或者用b = {}, b= b.fromkeys(a)  c= list(b.keys())。或者先排序，然后从最后一个元素开始判断，如果和下一个元素相等就del掉

## except的用法

先执行try语句，如果引发异常则跳到except的语句，对每个分支语句顺序尝试执行，如果引发的异常与except中的异常组匹配，则执行相应的语句，如果except中不写条件，就是未知异常的捕获。如果正常执行就执行else语句，finally语句总是会执行。

如果希望某段代码的异常能被后面的 except 块捕获，那么就应该将这段代码放在 try 块的代码之后；如果希望某段代码的异常能向外传播（不被 except 块捕获），那么就应该将这段代码放在 else 块中

## 如何用python来进行查询和替换一个文本字符串

假设有字符串a，如果是简单的替换，可以用a.replace('xx','xxx')

如果比较复杂，可以用re模块中的sub()函数或者subn()函数

re.sub(pattern, repl, string, count=0, flags=0)，最后返回一个string里匹配到pattern后用repl替换后的字符串, count 表示模式匹配后替换的最大次数，0表示全部替换

repl也可以是一个函数，一般用分组匹配的特殊语法为匹配值起别名，

subn返回的是替换后的字符串和替换次数组成的一个元组

## 正则表达式

既然都说到这里了，就详细地整理一下正则表达式的一些用法

- 反斜杠后边跟元字符去除特殊功能；（即将特殊字符转义成普通字符）
- 反斜杠后边跟普通字符实现特殊功能；（即预定义字符）
- 引用序号对应的字组所匹配的字符串。(从1开始计数)

re.match(pattern, string, flags=0)返回一个match object，是从头开始匹配的，用span函数可以返回一个（start，end）的元组。如果不是从头开始匹配，会返回None。flag是[标志位](https://www.runoob.com/python/python-reg-expressions.html#flags)：re.I表示忽略大小写，L表示特殊字符集，M表示多行模式等等

pattern里用r'xxx'写正则匹配，如matchObj = re.match( r'(.\*) are (.\*?) .\*', line, re.M\|re.I)。括弧里是匹配的东西，group( )返回的是正则匹配到的全文，groups( )返回的是正则中被括号括出来的字符串组成的元组，group可以在括号里指定返回第几个括号的匹配

re.search( )返回的是任意位置的第一个匹配

'(?P<value>\d+)'表示匹配字母后的多个数字，并且给他们起了一个别名叫value

re.compile()函数，用于保存正则表达式

findall( string, start, end)表示匹配所有

re.finditer(pattern, string, flag = 0)和findall类似，但是返回的是一个迭代器

\w表示字母数字及下划线，\W表示非字母数字以及下划线

re.split( pattern，string, time) 表示按照什么和最大划分次数，pattern加括号会把所有的割裂集都返回在列表中，不加就会把分隔符都去掉

## 用python匹配HTMLtag的时候，<.>和<.?>的区别

前面的是贪婪匹配，后面的是非贪婪匹配

\*，+的字符默认是贪婪匹配模式，后面加？变成非贪婪模式

\*表示零次或多次，+表示1次或多次，？表示零次或一次

贪婪模式倾向于最大长度匹配，非贪婪模式是只要有结果符合就行

## 帮助查找python中的bug和进行静态分析的工具

PyChecker，Pylint

## 元类

type除了查看变量类型之外，还可以用来创建一个元类，是class关键字在python幕后做的事情。像字符串，数字等对象，都是由str，int函数创建的，这些函数就是这些对象的类。元类就是创建类这种对象的东西，type是内建的元类

在写类的时候，如果加上\_\_metaclass\_\_属性， 可以自定义类的元类，目的就是在创建类的时候自动改变类。可以通过函数来定义属性，也可以用class来做元类（改写\_\_new\_\_）

在Django中ORM的创建中会用到元类，使用元类的编写很复杂但使用者可以非常简洁地调用API

## 单例模式

属于创建类型的一种常用的软件设计模式，通过单例模式的方法创建的类在当前进程中只有一个实例。new静态方法负责创建一个实例对象，返回后会自动调用init方法进行初始化。new方法主要是当继承一些不可变的class的时候，提供一个自定义的途径。

实现的方式：

1. 用模块的方式导入

   ```python
   # mysingleton.py
   class My_Singleton(object):
       def foo(self):
           pass
   
   my_singleton = My_Singleton()
   
   # to use
   from mysingleton import my_singleton
   
   my_singleton.foo()
   ```

   

2. 用装饰器

   ```python
   def singleton(cls):
     instances = {}
     def getinstance(*args,**kwagrs):
       if cls not in instances:
       	instances[cls] = cls(*args,**kwagrs)
       return instances[cls]
     
     return getinstance
   
   @singleton
   class MyClass:
     ...
   ```

   

3. 共享属性，所有实例的dict指向同一个字典

   ```python
   class Borg(object):
     _state = {}
     def __new__(cls,*args,**kwargs):
       ob = super(Borg,cls).__new__(cls,*args,**kwargs)
       ob.__dict__ = cls._state
       return ob
    
   class Myclass(Borg):
     a = 1
   ```

   

4. new方法，同时为了保证线程的安全，在内部加锁

   ```python
   class Singleton(object):
       def __new__(cls, *args, **kw):
           if not hasattr(cls, '_instance'):
               orig = super(Singleton, cls)
               cls._instance = orig.__new__(cls, *args, **kw)
           return cls._instance
   
   class MyClass2(Singleton):
       a = 1
   ```

5. 元类实现

## 静态方法，类方法，实例方法

实例方法只能通过实例来调用，静态方法和类方法都可以通过类直接调用。静态方法在定义的时候不用在参数里写上cls。

由此引申出类变量和实例变量，类变量是可以在类的所有实例之间共享的值，实例变量是单独拥有的。如果类变量是可变对象，那么改变实例变量会影响类对象

## 自省用法

type(), dir(), getattr(), hasattr(), isinstance()

## enumerate和items

enumerate返回一对index和值，items返回字典类型的键值对。

在函数里面可以被args和kwargs预先占位

## 类重写绕过

类的访问查找是从左到右深度优先，所以在有些重写过类内函数的时候有可能会在访问的时候依然访问到旧版本的方法

## GIL线程全局锁

Global interpreter lock, 限制一个核只能在同一时间运行一个线程，对于IO密集型任务，python多线程起到作用。但对于cpu密集型任务，python多线程占不到优势。

## 协程

是进程和线程的升级版，进程和线程都面临着内核态和用户态的切换问题，协程就是用户自己控制切换的实际，不需要陷入内核态，比如yield语句思想

## read，readline和readlines

read读取整个文件，readline读取下一行（使用生成器方法），readlines读取整个文件到一个列表里供我们遍历

## range和xrange

range生成的是列表，xrange生成的是生成器，不需要开辟内存空间，所以如果返回很大的时候xrange的性能更优一些

## python中的整数位运算

机器中整数的运算和存储都是用其补码表示的，正数的右移和左移是正常可以直观理解的，但是负数，比如int是8位的，那么-5就应该是1111 1101，然后再进行位操作。右移左补符号位。左移右边正常补0。特别的是，python中的移位没有高位溢出，因为python 的整数是不限长的

类似的，与，或，异或，取反也都是对补码进行运算然后再还原。正数自然没有影响，负数的时候就要用补码思维去思考了。

对于负数，无论是右移操作，还是n&（n-1）操作，都会陷入死循环，这时候需要一个技巧，-1右移动多少都是-1

```python
一个技巧
n & 0xffffffff 可以把负数转化为它的正数补码表示
```

另外，n-1会让n最右边一个1变成0，他右边的所有0变成1，左边不变。那么如果我们再进行n &（n-1），可以做到只把n最右边一个1变成0的效果。







---------------------------------------------------------------

------

------

## numpy库学习

https://www.jianshu.com/p/92486844124a

numpy是python中提供科学计算的一个基础包。提供了ndarray这一非常重要的数据结构，还提供了比如数学计算，形状操作，各种排序，傅立叶变换，线性代数计算，统计计算等等，而且为了提升数组操作的效率，有许多操作都是c语言代码编写并在本地预先编译完成的，所以可以达到近c的速度。

## ndarray的创建

## ravel()函数和flatten()函数

扁平化操作，都是把一个矩阵拉成一条，但是flatten会为数据分配新的内存。ravel返回的是一个原数组的视图，虽然其拥有不一样的地址，但是如果改变视图上的值的时候，原数组也会跟着被改变。

------

------

------

## tensorflow 2.0

咕果，哈哈这个中国名字真的可爱，它更新啦！

之前我做深度学习的时候用的pytorch，tensorflow了解的不算多，但是最近感觉工业界用TF还是大势，而且信仰之厂的产品说什么也得学一下，刚好它出了2.0的大改版本，就去玩一下吧，感觉和以前的版本还真的有很多不同的，API做了很大的改动，这意味着很多原来的功能如果想要在TF2里实现，用TF1的代码是跑不通的（貌似有做兼容的工作，但都有2了干嘛还抱着1呢，反正我也没包袱哈哈）。（[这里有一份对照表](https://docs.google.com/spreadsheets/d/1FLFJLzg7WNP6JHODX5q8BDgptKafq_slHpnHVbJIteQ/edit#gid=0)）

TF2.0的核心功能是Eager execution（动态图机制），移除`tf.get_variable`, `tf.variable_scope`, `tf.layers`，强制转型到基于Keras的方法，也就是用`tf.keras`（好像是被TF收购了，keras被封装地更好，应该会更好用）。

------

------

------

## Pytorch

我觉得torch在使用上要更简单，而且基本上科研所有的需求torch现在已经都能满足够用了。在这里稍微记录一下pytorch学习中的一些过程

https://www.manning.com/books/deep-learning-with-pytorch#toc

https://livebook.manning.com/book/deep-learning-with-pytorch/chapter-1/v-10/

xx