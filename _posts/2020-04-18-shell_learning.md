---
layout: post
title: "Shell learning"
date: 2020-04-18 00:23:33
image: '/assets/img/'
description: 'Shell learning note'
tags:
- shell
categories:
- Dev-ops 
twitter_text: 'Do you know these?'

---

## Everyday sentence

11-29: I don't like rasins. They used to be fat and jucy, and now they are twisted. They had their lives stolen. They taste sweet, but really they are humiliated grapes.

12-1: We all fear death and question our place in the universe. The artist's job is not to succumb to despair, but to find an antidote for the emptiness of existence.

12-2: You know the only thing that has made the whole thing worthwhile...has been those... few times that I've been able to really, truly connect with another human being.

12-3: We are made of dreams, and dreams are made of us.

12-5: Funny, how just when you think life can't possibly get any worse it suddenly does.

12-6: 美丽的梭罗河/ 我为你歌唱 / 你的光荣历史 / 我永远记在心上 / 旱季来临 / 你轻轻流淌 / 雨季时波涛滚滚 / 你流向远方

## SHELL

机器只懂得01，能够把我们的代码翻译成机器语言，我们需要编译器（解释器）。代码语言可以分为编译型语言和解释型语言。编译型快，但跨平台性不好，所以底层开发或大型应用程序开发用编译型的比较多，服务器脚本和辅助接口用解释型。

shell 是操作系统的最外层。shell 合并编程语言以控制进程和文件，以及启动和控制其它程序，相当于一个命令行解释器，提供了一个面向Linux内核发送请求的系统级程序，也可以作为一种编程语言。Linux有很多种类的shell，用的最多就是Bourne Again Shell（Bash）

Posix(表示可移植操作系统接口(Portable Operating System Interface of UNIX), 是IEEE为要在各种UNIX操作系统上运行软件，而定义API的一系列互相关联的标准的总称，其正式称呼为IEEE Std 1003。在正则语句中会用到grep -P , 或者用awk，gawk代替( 用这个的话正则里的东西前后要加/)

## 定义变量

定义用等号(不能有空格)，调用用$号，unset用于取消变量

read 变量名   可以让用户来命名变量

declare -x 加在赋值语句前面可以给变量做限制，比如只读或者整型

env查看环境变量，set查看所有变量（包括临时变量），export把变量变为环境变量。变量文件夹的访问顺序如下。

/etc/profile                    全局环境变量

$HOME/.bash_profile  保存当前用户的环境变量

$HOME/.bashrc           保存当前用户的bash信息

/etc/bashrc                   全局bash信息

$HOME/.bash_logout  定义用户退出时执行的程序

$HOME/.bash_history  用户的历史命令

source命令相当于让其退出重新登录

## 变量运算

内置bash中的一些变量被成为系统变量

运算的时候可以用\$[ ]，​\$( ( ) )，也可以用expr，用expr的时候运算符左右要有空格

如果用+=会直接在右边加上数字，在前面加上let才能实现运算

++ i 和 i++的区别是先赋值还是先运算

## 数组

普通数组只能用整数作为数组索引，array4=(1 2 3 4 "xx" [10]=mac) 实现一次赋多个值，[ \* ] 提取数组内所有元素，\${#array[ \* ]} 获取元素个数，\${array[@]:1:2} 来用从索引1开始取两个值

关联数组可以用字符串做索引，declare -A xxx定义，有点像字典

dirname 路径 可以取出目录，basename 路径 可以取出变量

## 条件判断

有三种表达方式，第一种是test，第二种是[ ]，第三种是[[ ]]。其中第二种和第三种在括号内左右都要留一个空格，第三种支持正则表达

可以判断文件类型，判断文件权限，判断文件新旧，判断整数，判断字符串，多重条件判断

符号;和&&和\|\|都可以用来分割命令或者表达式

分号（;）完全不考虑前面的语句是否正确执行，都会执行;号后面的内容

## 控制语句

```shell
if [ condition ];then    
	command1 
elif [ condition2 ];then
  command2    
else    
	command3
fi
```

## 循环语句

```shell
for variable in {list}  # or in a b c								do 										# for(( expr1;expr2;expr3 ))
	command           
	command        
done
# 一样有continue，break，return用exit替代

while [ $i -le 100 ]
do
   let sum=$sum+$i
   let i+=2
done

until [ $i -gt 10 ]
do
  echo $i
  let i++
done
```

## case语句

```bash
case var in          #定义变量;var代表是变量名
	pattern 1)         #情况1;用 | 分割多个模式，相当于or
    command1 
    ;;               #两个分号代表命令结束
pattern 2)
    command2
    ;;
*)                  # 不满足以上情况，相当于else
    command3
    ;;
esac                # 表示case语句结束
```

## 函数的定义与调用

```shell
function 函数名()
{
   函数体
}
# return默认返回函数中最后一个命令状态值，也可以给定参数值，范围是0-256之间。如果没有return命令，函数将返回最后一个指令的退出状态值。

# 调用的时候可以当前命令行用名字直接调用
# 也可以加到bashrc里
# 也可以在脚本前面加上source ./filename.sh
```

## 应用

ping -c次数 来判断当前主机和ip地址是否能ping通

&>file 意思是把 标准输出 和 标准错误输出 都重定向到文件file中

$?是根据命令行执行状态来判断真假

ps可以查看进程的运行状态，pgrep以名称为依据从运行进程队列中查找进程，并显示查找到的进程id

wget用来从指定的URL下载大文件。wget非常稳定，它在带宽很窄的情况下和不稳定网络中有很强的适应性，如果是由于网络的原因下载失败，wget会不断的尝试，直到整个文件下载完毕

 curl利用URL规则在命令行下工作的文件传输工具。它支持文件的上传和下载

 elinks -dump 能实现一个纯文本界面的WWW浏览器，dump是参数，将HTML文档以纯文本的方式打印到标准输出设备

id 用于判断一个用户是否存在

uname -r 查看内核版本号

rpm判断某软件是否安装

echo $RANDOM  生成随机数

## 行首单独的（-参数）

-d 判断是否是一个目录
-f 判断是否是一个文件
-L 判断是否是一个软连接文件
-e 判断文件是否存在

## Linux三剑客之首：awk

是一种编程语言，在linux/unix下对文本和数据进行细切分处理，最强大也最复杂

## 三剑客：sed

sed是Stream Editor（流编辑器）的缩写，简称流编辑器，用来处理文件的

## 三剑客：Grep

首先很感谢JY大佬

grep是行过滤工具；用于根据关键字进行行过滤，命令用于查找文件里符合条件的字符串

```shell
OPTIONS:
    -i: 不区分大小写
    -v: 查找不包含指定内容的行,反向选择
    -w: 按单词搜索
    -o: 打印匹配关键字
    -c: 统计匹配到的行数
    -n: 显示行号
    -r: 逐层遍历目录查找
    -A: 显示匹配行及后面多少行  
    -B: 显示匹配行及前面多少行
    -C: 显示匹配行前后多少行
    -l：只列出匹配的文件名
    -L：列出不匹配的文件名
    -e: 使用正则匹配     # 相当于egrep
    -E:使用扩展正则匹配
    ^key:以关键字开头
    key$:以关键字结尾
    ^$:匹配空行
    --color=auto ：可以将找到的关键词部分加上颜色的显示
```

这里将常用的一些知识做个引子，不做过多详细的介绍，可读性可能比较差。alias 可以给命令起别名，可以临时起也可以放在etc/bashrc里然后source对全局所有用户生效，还可以放在~/.bashrc里source对局部某个用户生效

## 正则回顾

字符列表用[ ]括起来表示匹配任一单个或一组单个字符，^放在括号外表示匹配开头，放在里面表示非

\d表示数字0-9，\w字母数组下划线，\s表示空格、制表符、换页符

grep用拓展类正则要加-E

## cut

用于对列的截取，cut 选项 文件名

```shell
-c: 以字符为单位进行分割,截取
-d: 自定义分隔符，默认为制表符\t
-f: 与 -d 一起使用，指定截取哪个区域
```

runlevel可以对etc/inittab文件进行操作获取系统运行级别

## sort

将文件的每一行作为一个单位，从首字符向后，依次按ASCII码值进行比较，最后将他们按升序输出

```shell
 -u ：去除重复行
 -r ：降序排列，默认是升序
 -o : 将排序结果输出到文件中,类似重定向符号 >
 -n：以数字排序，默认是按字符排序
 -t ：分隔符
 -k ：第N列
 -b ：忽略前导空格。
 -R ：随机排序，每次运行的结果均不同
```

## uniq

uniq用于去除连续的重复行

```shell
-i: 忽略大小写
-c: 统计重复行次数
-d: 只显示重复行
```

## tee

tee工具是从标准输入读取并写入到标准输出和文件，即：双向覆盖重定向（屏幕输出|文本输入）-a追加模式

## echo

用于字符串的输出，-e开启转义，\c就可以表示不换行。如果要执行字符串的内容，用 \` \`反印号括起来

## diff

diff工具用于逐行比较文件的不同

注意：diff描述两个文件不同的方式是告诉我们怎样改变第一个文件之后与第二个文件匹配

输出的内容可以写到一个 > file.patch文件里，然后patch file1 file.patch就可以打补丁让它变成file2

## paste

paste工具用于合并文件行，后面可以跟两个文件的名字。用-d定义分隔符，用-s设置串行合并

## join

把两个文件中相同内容的那一行合并

## tr

tr用于字符转换，替换和删除；主要用于删除文件中控制字符或进行字符转换。-d删除所有xx，-s删除连续并重复的字符xx。可以右边接< filename来接收文件的内容

## ipconfig

用于查看网络设置IP，MAC地址，linux和mac用ifconfig

## bash特性

```bash
tab可以自动补全
^c   终止前台运行的程序
^z 将前台运行的程序挂起到后台
^d   退出 等价exit
^l   清屏 
^a   光标移到命令行的最前端
^e   光标移到命令行的后端
^u   删除光标前所有字符
^k   删除光标后所有字符
^r 搜索历史命令

*:匹配0或多个任意字符
?:匹配任意单个字符
[list]:  匹配[list]中的任意单个字符,或者一组单个字符 
[!list]: 匹配除list中的任意单个字符
{string1,string2,...}：匹配string1,string2或更多字符串

rm -f 删除文件，-rf递归删除文件夹
ls -l 查看时间属性
touch 创建空白文件或者更新文件时间属性
cp –r 复制底下的所有文件和目录 从地址1 到 地址2
      -i 提示是否覆盖
cd /  切换目录
cat   查看
mkdir 创建文件夹
pwd   显示当前工作目录
mv 2.log 1.txt 将2.log重命名为1.txt
mv * ../ 移动当前目录所有文件到上级目录
mv 1.txt test3 移动1.txt到test3目录

双引号"" :会把引号的内容当成整体来看待，允许通过$()来引用其他变量值

单引号'':会把引号的内容当成整体来看待，禁止引用其他变量值，shell中特殊符号都被视为普通字符

反撇号``:反撇号和$()一样，引号或括号里的命令会优先执行，如果存在嵌套，就无效了
```

## 脚本搭建

touch一个txt或者sh文件,用chmod +x添加权限，sh运行脚本，如果想要把它加进环境变量，就在 ~/.bashrc最后加上export PATH="绝对路径:$PATH" 之后source

```shell
#!/bin/bash
脚本第一行用于指定解释器

# 以下内容是对脚本的基本信息的描述
# Name: 名字
# Desc:描述describe
# Path:存放路径
# Usage:用法
# Update:更新时间

#下面就是脚本的具体内容
commands
...
echo "The project has been finished at $(date +%F)"

```

## 补充一点运维的知识

SaaS、PaaS、IaaS是美国国家标准和技术研究院)定义的云服务分类

IaaS是基础设施即服务，用户有权限访问操作系统之上的一切功能

PaaS是平台即服务，给开发环境

SaaS是软件即服务，给软件的使用权

主流的部署也分为私有云，公有云和混合云

## docker和k8s：占个坑



