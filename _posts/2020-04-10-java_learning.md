---
layout: post
title: "Java learning"
date: 2020-04-10 11:43:13
image: '/assets/img/'
description: 'Java learning note'
tags:
- java
categories:
- Language 
twitter_text: 'Do you know these?'

---

## To You

When I think of you, I'm reminded of the beautiful plains of Iowa.The distance between us is breaking my spirit. My time and experiences without you are meaningless to me. Falling in love with you was the easiest thing I have ever done. Nothing matters to me but you.And everyday I am alive, I'm aware of this. I loved you the day I met you, I love you today, and I will love you to rest of my life.

网络传输乱码

高并发

## 疫情公众地图号 - 01

任务卡1

```java
任务名称： 自动关机程序
任务描述
public static void main
```

cheat egine

任务卡2

```java
任务名称：向任意手机号发送验证码短信
```

工具类与工具对象

网址https/http（明文传输）超文本传输协议

协议：// 域名：端口号/虚拟路径？参数列表#锚点

ip地址，是计算机在互联网中的唯一标识 （公网ip）

192.168.1.1  /  192.168.0.1

家里要拉网线，主网线是有共网ip的，你不小心的时候签了协议，因为ipv4不够用了，会被分流，可以打给运营商改公网ip

ip地址为了好记会被dns服务商转化成域名

端口号就像确定发送计算机上的哪个进程/门牌号（0-65535）

锚点相当于导航栏定位页面位置

URL （网址）统一资源定位符：

```java
URL url = new URL("网址");
# 1. 通过对象的打开网络连接的功能来打开网络连接,并得到一个连接对象
URL Connection conn = url.openConnection();
# 2. 通过连接对象，得到用于读取网页内容的字节输入流
InputStream is = conn.getInputStream();
# 4个数字一个位，8个数字一个字节
  
# 3. 将上述字节流 装饰 为字符输入流 
# 4. 再装饰为带有缓冲功能，能一次读取一行的字符输入流
BufferedReader br = new BufferReader(new InputStreamReader(is,"UTF-8"));

# 5. 通过字符输入流，读取一行内容
String text = br.readLine();

# 6. 将读取到的内容，展示到控制台
System.oy.println(text);

```

爬到的内容会出现乱码：因为编码表的不同（ASIC，GBK，GB2312，GB18030，unicode，UTF-8）

疫情数据的分析与读取：

网易是用前后端分离的架构，百度用的是动态网页嵌入源代码的方式

F12-network-刷新网页-找request-xhr

编程规约 华山论剑版

在做机器人对话的时候，需要把我们的沟通文字进行乱码处理

```java
# 0
String para = URLEncoder.encode("讲个笑话","UTF-8")
URL url = new URL("https://api.jisuapi.com/iqa/query?appkey=62958a3a6ef3c56d&question");
URL Connection conn = url.openConnection();
InputStream is = conn.getInputStream();
BufferedReader br = new BufferReader(new InputStreamReader(is,"UTF-8"));
String text = br.readLine();
System.oy.println(text);
```

短信API：三网合一，出现了很多云中间商（阿里云，华为云）来为你开放小量购买的条件

附加任务卡：

申请自己的微信公众号

Day03:

静态网页：网页里的内容不发生改变

动态网页：会根据程序的规则动态变化。根据数据动态生成新的网页，供用户访问。填入前端程序猿编写的模版

JSP（java server pages）与html不同，可以编写java代码

执行区域：<%   cccc 用户每次访问都执行一次 %>

成员区域：<%!   cccc只能用于定义成员，不能编写能执行的功能语句，只会在第一个用户访问时执行，每一个用户访问时执行区域的代码都可以使用这里定义的变量 %> 

tomcat开发和调试JSP的首选

```
任务名称：
疫情地图的开发与部署
任务实施：
部署在阿里云，放开微信公众号的入口，对高并发情况就行优化处理
```

优化：加上变量缓存

## 在浏览器中输入URL到显示出来的过程

浏览器查找域名IP的网址（DNS查找过程：浏览器缓存，路由器缓存，DNS缓存）

浏览器向web服务器发送一个HTTP请求（cookies会随着请求发送给服务器）

## URI和URL的区别是什么

URI(Uniform Resource Identifier)是统一资源标识符，可以唯一标识一个资源 
URL(Uniform Resource Location) 是统一资源定位符，可以提供该资源的路径。它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何定位这个资源

## Java 中 IO 流分为几种

按照流的流向分，可以分为输入流和输出流
按照操作单元划分，可以划分为字节流和字符流
按照流的角色分，可以划分为节点流和处理流

## 使用Java实现两数交换

方法一：使用第三个变量进行交换
int x = 3, y = 9;
System.out.println(“交换前：” + x + “，“ + y)；
int temp = x;
x = y;
y = temp;
System.out.println(“交换后 ：” + x + “，“ + y)；

方法二：不使用第三个变量，通过数学方式（两数相加保存和）交换
int x = 3, y = 9;
System.out.println(“交换前：” + x + “，“ + y)；
x = x + y;
y = x – y;
x = x – y;
System.out.println(“交换后 ：” + x + “，“ + y)；

方法三：使用异或，通过两数异或保存两数状态
int x = 3, y = 9;
System.out.println(“交换前：” + x + “，“ + y)；
x = x ^ y;
y = x ^ y;
x = x ^ y;
System.out.println(“交换后 ：” + x + “，“ + y);

## 概念字典

Java：一门语言

J2EE：规范+概念+开发平台

Servlet：服务器端的java程序

JVM：java虚拟机

JSP：在html代码中嵌入java代码所形成的动态网页文件，在运行的时候，被JSP引擎转化为Servelet（java文件），调用Java编译器编译成class文件，最后JVM解释执行

Tomcat：JSP/Servelet的一个web容器，支持servelet规范，将JSP代码编译成JVM能够识别的java class

MVC：是一种架构模式，把软件分为模型，视图和控制器三个基本部分

Spring: 是java的一个应用框架，类似于tensorflow之于python

SpringBoot：Spring的简化版

Maven：一个字典，帮你管理jar包的依赖关系

Nginx：一款轻量级的Web服务器、反向代理服务器

## JVM中的字节码和机器码

一般的高级语言如果要在不同的平台上运行，至少需要编译成不同的目标代码。但引入Java虚拟机后，Java语言在不同平台上运行时不需要重新编译。Java虚拟机屏蔽了与具体平台相关的信息，使得Java语言编译程序只需生成在Java虚拟机上运行的目标代码**(字节码，class文件)**，就可以在多种平台上不加修改地运行。Java虚拟机在执行字节码时，把字节码**解释**成具体平台上的机器指令**(机器码，01组成)**执行。这就是Java的能够“**一次编译，到处运行**”的原因

## 编译器和解释器

编译器负责的是源码到机器码的过程

解释器负责的是从相对高级的代码解释称机器码，比如JVM就可以承担解释器的作用



