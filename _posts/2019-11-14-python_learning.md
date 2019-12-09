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

还可以用%占位，print( "out:%s"%a ), 这时候即使a不是一个字符串，而是数字，列表也一样可以进行转换，但元组不行

这时候可以用一个更强的格式化输出，print( "out:{}".format( ) ), 更进一步，还可以控制输出的顺序，print( "out:{0}  b={1}".format(a,b) ) 或是print( "out:{0}  b={1}".format(*c) ) ， c可以是元组和列表和字符串，\*是解包的操作。如果是字典，则单星号解包的元素是key值，双星号解包的元素才是value值。在py3中，可以直接写成print( f"out:{a}  b={b}")来进行填充

其他格式的输出，比如整型，浮点数，%.2f两位小数，%5.2f 占位宽度，%-5.2f占位左对齐等等

## try/except/else/finally异常捕获

如果一个语句有可能发生错误，但又不想后面的程序因为它不能执行，可以把它放到try里，再在except里输出程序在这里发生了错误即可。还可以用except KeyError等更细致地捕获异常，最后因为你不太可能捕获所有的异常，所以一般会加上except Exception来做补充。

后面还可以跟一个else，用来提示语句没有错误，异常没有捕获。

finally则是不论如何都会进入执行的语句

## del关键字

在C++中用于释放动态分配的内存，内存释放后，该区域内存储的值也被删除

但在python中，del关键字并不会去操纵内存，而只是删除了变量的引用，python中内存的释放是由garbabe center（GC）处理的，当某块内存的引用变为0的时候才会被当成垃圾被回收

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
Arthur.flash()    
print(Arthur.__dict__)  # 用于查看它所有的实例变量值
```

## self参数



## 前置单下划线

一般是在类内定义变量的名字，由于python中没有对public和private进行严格的定义，所以默认在看到前置单下划线的变量或者方法时，领会代码编写者的意图：最好只在内部使用，起到约定俗成的private的功能

## 后置单下划线

有一些名词，比如class，在python中属于保留关键字，那么如果我们想要定义一个class仅仅作为名字的变量，就可以在它后面加上一个后置单下划线来区分，仅仅是因为懒得想新名字而已哈哈

## 前置双下划线

类内如果用前置双下划线定义一个变量或者方法，那么这时候python内部会默认为其改变属性名称，如果想自己亲自看一下可以用dir(class_name)查看所有变量

改变名称的作用有二，一是可以使属性变量或者方法私有，不会被派生类继承，仅能自己使用，二是可以避免派生类和父类属性名称的冲突

## 前后置双下划线

比如我们经常看见的类内初始化函数\_\_init\_\_，python中通常把这种被前后双下划线包裹的方法称为魔法方法，他们会在类或对象的某些事件触发后执行。比如我们在实例化一个新类的时候，python会执行一个\_\_new\_\_（）的魔法方法生成一个实例对象，然后执行init魔法方法对对象进行初始化。

除此之外，python中的许多面向对象的操作都是靠魔法方法实现的，比如len求字符长度的时候，会调用类中内置的魔法方法等等

## repr函数和\_\_repr\_\_魔法方法

repr函数和str函数类似，都是python内置的函数，都是转换为字符串，但str面向的是用户，repr则更容易被解释器接受

我们使用一个类的时候，假设为a object，使用print（a）的时候其实就是调用了\_\_repr\_\_的方法，如果没有特别进行编写的话会输出这个object的信息，如果进行编写了，可以输出你指定的字符串。（ps：在py3.6之后出现了f-string的格式化字符串方法，用{ }来提示需要被替换的内容）

## 函数参数前的单* 和双**

在函数申明中出现*，起到打包的作用，变量会被重新打包成元组，**会打包成字典

语句中*代表解包的操作，如果后面跟一个列表，集合，元组，会将之为拆分为单个元素，如果字典用单\*号只会取出键。如果后面跟的是字符串，那么会把它拆成一个个字母。  **对应字典，解包后就变成a = 0， b= 1的格式

## python中的队列

import queue，有full，empty，put和get函数。 （qsize，clear...)

- d = Queue.Queue()遵循FIFO
- LifoQueue.LifoQueue() 遵循LIFO
- PriorityQueue.PriorityQueue()

定义的时候括弧里可以定义队列的大小,不指定就是动态的

上面涉及到了优先队列，它按照优先级出队，优先级的选择过程是用堆实现的，所以这里补充一下堆的知识，堆是用数组实现的二叉树，分为最大堆和最小堆 import heapq, heapq.heapify( listname )可以用O（N）的复杂度把列表转化为堆，一般heap[0]是最小的元素（最小堆）, heapq.heappop(heapname)可以弹出元素, heapq.heappush( L, xxx )用于插入元素。

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

## numpy库学习

https://www.jianshu.com/p/92486844124a

## tensorflow 2.0

咕果，哈哈这个中国名字真的可爱，它更新啦！

之前我做深度学习的时候用的pytorch，tensorflow了解的不算多，但是最近感觉工业界用TF还是大势，而且信仰之厂的产品说什么也得学一下，刚好它出了2.0的大改版本，就去玩一下吧，感觉和以前的版本还真的有很多不同的，API做了很大的改动，这意味着很多原来的功能如果想要在TF2里实现，用TF1的代码是跑不通的（貌似有做兼容的工作，但都有2了干嘛还抱着1呢，反正我也没包袱哈哈）。（[这里有一份对照表](https://docs.google.com/spreadsheets/d/1FLFJLzg7WNP6JHODX5q8BDgptKafq_slHpnHVbJIteQ/edit#gid=0)）

TF2.0的核心功能是Eager execution（动态图机制），移除`tf.get_variable`, `tf.variable_scope`, `tf.layers`，强制转型到基于Keras的方法，也就是用`tf.keras`（好像是被TF收购了，keras被封装地更好，应该会更好用）。

## Pytorch

我觉得torch在使用上要更简单，而且基本上科研所有的需求torch现在已经都能满足够用了。在这里稍微记录一下pytorch学习中的一些过程

https://www.manning.com/books/deep-learning-with-pytorch#toc

https://livebook.manning.com/book/deep-learning-with-pytorch/chapter-1/v-10/