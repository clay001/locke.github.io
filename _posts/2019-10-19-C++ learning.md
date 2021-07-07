---
layout: post
title: "C++ learning"
date: 2019-10-19 15:22:44
image: '/assets/img/'
description: 'Some knowledge about C++'
tags:
- C++  
categories:
- Language 
twitter_text: 'Do you know these?'
---

## Preface

C++ is needed when you want to run fast and well-perfomed codes, and it can directly controll the hardware. In fact, when you write some codes, you need to pass it to the complier, and the complier can give you the machine code for your target platform, machine code is the actual instruction that your devices CPU will actual perform. C++ is widely used in almost everywhere, it can support almost all the platforms. Everyone is using it ! Here I record some of the learning notes, check whether you know them all.

## 基本步骤

代码首先传入编译器，产出机器码，机器码可以直接控制硬件。它可以支持几乎所有的平台，C#和java是运行在虚拟机里的，所以它们中间存在一个翻译的中介。当我们需要榨干硬件所有的性能的时候，C++就是一个很好的选择

在VS里有solusion和project之分，solution是一个包含多个相关projects的集合，类似一个工作台。projects是文件的集合，被编译成某目标二进制文件（库文件lib或者可执行文件exe）

在VS的视图里，filter可以看作是一个虚拟的文件夹，用于组织代码。我们可以转到真实的file目录去创建一个src文件夹，然后把源文件都放在里面。

<<是重载符，可以想象成一个函数。最后只有cpp文件会被编译，头文件不会，编译后会生成一个obj文件，然后通过linker把所有的obj缝起来成为一个exe。exe存在sln文件夹一起的Debug目录下

声明是在主函数里写的函数头，告诉编译器函数存在。

## 编译具体

编译就是对源代码进行语法检查，一个cpp文件会被当成一个translate unit被编译器编译成一个obj文件（对象文件）

预处理 --> tokenizing(标记解释) --> parsing(解析) 

预处理的语句：inlude（直接粘贴），define（替换），if和endif（条件判断）。.i文件是编译产生的替换文件，.obj文件是编译之后的二进制文件，.asm是汇编指令文件，汇编指令文件中每一个变量会被存储在一个寄存器中。在debug模式下很多额外的东西不会被优化，所以会比较冗长。

创造一个抽象语法树。在java里，类名必须和文件名相同，文件夹结构也得和package一样，C++则不需要。

命令： g++ 一个cpp文件（在linux/unix上是cc文件）， -c选项单独执行编译

## 链接具体

检查定义声明是否能被完整找到，把编译过程中生成的所有对象文件链接起来，形成一个可执行程序

遇到linking重复定义的问题，有几种解决方案：

1. static是静态标识，表示函数或变量只是为这个翻译单元声明的
2. inline标识表示只取出定义中的body来使用
3. 把相关的函数主体放在一个相关的文件里，头文件中只写声明去调用

mac OS：nm -C 查看对象文件中的内容， 有数字的是我们定义的函数，没有的是外部函数。 g++ 对象文件得到out文件。

## 变量

定义的时候可以直接赋值，也可以不赋值，后续可以重赋。int是4字节，32bits，1位用于表示符号，31位表示值。unsigned关键字可以解放符号位。

char是2个字节的字符，short是2个字节，long是4个字节，long long是8个字节。

float是4个字节（需要在数字后面加上字母f ），double是8个字节。

bool是1个字节。其实只需要一个bit，但我们最小访问的单位就是byte。

sizeof ( )可以帮助检查变量大小。

指针的形式是在类型后加上\*，引用是在类型后加\&

先写一个return type，然后参数，最后写主体

## 头文件

函数定义之后如果要在另一个文件中使用，需要声明，这是通过复制函数签名实现的，我们可以把这些签名都写在一个头文件里来简化这个过程。头文件的第一行一般有#Pragma once，是一种header guard（头文件保护符），他可以防止我们把单个头文件多次include到一个单一翻译单元里。老版本用的是ifndef。

方括号include用于编译器的include路径，引号用于所有。C标准库里的文件一般都有h扩展名，C++中的一般没有。

如果是使用第三方模块，需要在源代码中包含头文件，然后在链接阶段的时候需要有相应的静态链接库（a文件）

## hpp和h的区别 

hpp（Header Plus Plus）是将.cpp的实现代码混入.h头文件当中，定义与实现都包含在同一文件，调用的时候只需要include该hpp文件即可 

与xx.h类似，hpp是C++程序头文件。一般来说，xx.h里面只有声明，没有实现，而\*.hpp里声明实现都有，后者可以减少.cpp的数量。

但要注意的是，hpp中不可以包含全局对象和全局函数

## 调试代码

断点和查看内存

## 取余运算上的不同

和python不同，在C++中 -1%10 的结果并不是9，而是-1。所以在我程序中碰到过的一个轮盘锁问题的时候，需要实现0负方向转动的结果是9，这时候就得再做一层操作，我当时的选择是如果是负数就用10去减一次

## 类的定义和调用

类的成员函数是指那些把定义和原型写在类定义内部的函数，就像类定义中的其他变量一样。类成员函数是类的一个成员，它可以操作类的任意对象，可以访问对象中的所有成员。

成员函数可以定义在类定义内部，或者单独使用**范围解析运算符 ::** 来定义。

在创建一个需要初始化的类的时候，如果在定义的时候没有定义默认值，则必须在创建的时候给出初始化的参数

## Cin的用法

cin >> 可以从键盘读取数据，以空格 tab 或者换行符作为分隔符

不想略过空白符：cin>>noskipws>>input

a = Cin.get() 或者cin.get(a) 可以读取一个字符（不略过空白符），也可以cin.get(array,20) {char array[20]={NULL}; } 来读取一串指定的长度，设20的话经过我实验发现可以读19个字符(需要留一位给结束符)。第三个参数可以设置一个"\n"之类的参数来设定结束符，默认为回车，cout数组的话结束符是不会被输出的。后续可以继续使用get来读入，如果之前的命令在到达指定长度之前已经遇到了结束符，这个结束符不会被缓冲区自动删除，接着读的话依然可以读到。（cin.get(a).get(b) 之类的链式操作也是合法的）

cin.getline(array,20) ，读一行，规则和上面的get差不多，但是如果这一行在指定长度之后还有输入，后续再使用get是读不到任何东西的，我觉得这里要特别小心，可见不能随便设置line的长度，至少不能估小。如果这一行在长度之前读到了结束符，getline会自动删除缓冲区里的结束符。get到的是后一位的东西。

## 原码，补码，反码

正数的这三码都是它自己

负数的原码也是不变，只是符号位放的是1。反码是符号位不变，其余位取反。补码是符号位不变，其余位取反，然后加1

&是按位与，｜是按位或，^是按位异或（不同时为1），～是按位取反，<<和>>是左右移位，值得注意的是他们在计算机中都是对原数的补码进行操作的，计算得到的结果再返回其补码对应的原码，所以正数的操作不受影响，但负数的操作就要特别注意了。

## queue和pair

用了queue的数据结构，里面塞入了一个pair<>的结构，定义语句写为`queue<pair<int,int>>  xxx;`queue.push()可以往里加元素，如果是加pair，就是`xxx.push({x,x})`，取出头元素用.front()，弹出头元素用.pop()

pair结构的第一个元素值用pairname.first访问，第二个元素用pairname.second访问

## 基础语法

这些和其他语言基本是一样的，for，while，continue，break，return等等

## 指针

指针存储的是一个整数，代表内存中的地址，\&是取址符，\*是解引用，对指针使用的话就是取值。指针类型没有什么实际的用处，只是告诉编译器一个类型，这样我们在给指针赋值的时候就会是合法的。

这里还会涉及到stack和heap的知识。如果我们用new（new底层调用了malloc）和memset去新建一个变量，那么数据是被分配在heap上的，使用完之后我们会用delete[ ]（底层调用了free）去删除。

由于指针也是变量，那么还会有double和triple指针的骚操作。二级指针在一个32位的应用程序中是4个字节的，其存储的值是一级指针的地址，有时候电脑的内存是逆序的，所以需要反向拼接得到真实的地址。

## Push/emplace/insert

Unorderedset, stack, queue等容器的插入操作好像都有类似的表达，我也困惑了很久。emplace是C++11之后才有的特性，用于插入一个元素，相比于insert，它可以避免产生不必要的临时变量。

map上情况比较特殊，emplace会需要额外构建两个tuple，所以如果临时变量构建代价不是很大（基础类型），也存在insert更快的情况。

对于stack和queue只有push和emplace，和其的front和end插入功能。

## Struct和class

struct里的东西默认是公有的，class默认是私有的。

## Static和extern

类外的static表示这个变量在link的时候只对这个编译单元（obj）里的东西可见。extern的意思是从外部去寻找定义。类内的static表示是类结构本身私有的唯一变量，类内静态方法无法访问非静态成员变量，相当于是在类外的方法。

静态的局部变量的生命周期是整个程序，作用域就是这个函数内。

## \&和\*

\&是取址，\*是取值

## constructors和destructors

C是用来初始化类变量的，D是用于销毁的，D方法的前面有一个～号。D的存在是为了防止内存泄漏，比如堆的内存分配。

## ENUM

一种便于枚举的数据类型，给定第一个赋值变量的值，之后就会自动枚举。

## 继承
