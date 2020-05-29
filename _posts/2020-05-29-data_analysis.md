---
layout: post
title: "Data analysis"
date: 2020-05-29 10:44:32
image: '/assets/img/'
description: 'Data analysis note'
tags:
- data analysis
categories:
- Internship
twitter_text: 'Do you know these?'

---

## Everyday sentence

2020/05/29 update: 

This doc was originally established on 2020/04/28, now update to record my Internship. Mainly about a Smart City Platform and its relevant knowlege, especially in computer network and database.

Many thanks to Huang Junli, Bruce Wu and all the others group members.  (FYI: xiaolin coding)

## Pandas的基础操作

pd.read_csv('xxx.csv', names=new_columns, header=0)读取文件

pandas读取成的结构叫dataframe，他其中的每一列都叫一个series，操作类似于numpy中的矩阵，但是它还拥有行名和列名。

df.columns 可以查看所有列名。访问可以直接跟在点号后面或者以字典的方式访问。`DataFrame(df, columns=['Change', 'Ratings'])`可以取出某一些子列形成新的dataframe。赋值和修改可以用字典的方法，递交一个series列。如果用pd.Series(xxx, index = [ ])，index里还可以指定xxx的数值赋在第几个位置。

df.columns可以在直接传入列名的列表来实现批量修改，或者`df.rename(columns={'a': 'A'}，inplace=True)`取修改列名。相应的index参数是行名。

df.sum()对列求和，sum(1)对行求和。df.apply( )对每个元素进行操作，里面可以设置一个lamda函数。或者直接df ** 2也等同于对元素操作。

列扩充直接进行赋值，行扩充用df.append( )里面放一个列名对应的键值字典，index参数指定行名。

 df_b.join(df_a) 进行合并，如果索引不完全相同的话就只保留dfb的索引，缺失值用NaN填补。如果想合并并集就加上参数how='outer'

## Unicode和UTF-8的区别

他们都是字符流和字节流的转换方法。UTF-8还包含编码和解码的过程，在内存和资源的占用上会更小，但由于可变长的性质也不太好琢磨，所以utf-8编码在做网络传输和文件保存的时候，将unicode编码转换成utf-8编码；当从文件中读取数据到内存中的时候，将utf-8编码转换为unicode编码

- Unicode 是「字符集」
- UTF-8 是「编码规则」

## Tornado Web

tornado是使用python编写的一个强大的，可拓展的web服务器，是一个编写对HTTP请求响应的框架

它是一个异步的服务器，可以用于减轻基于线程的服务器限制，当负载增加的时候，类似于Node.js, lighttpd, tornado这样的服务器使用协作的多任务方式进行优雅的拓展（挂起请求，等待资源就绪之后调用回调函数）

```python
# 导入tornado的模块
import textwrap
import tornado.httpserver
import tornado.ioloop
import tornado.options
import tornado.web
# 从命令行中读取设置
from tornado.options import define, options

# 如果一个与define语句中同名的设置在命令行中给出，那么它将成为全局option的一个属性，如果使用了--help选项，就会打印文本。type是类型验证，不合适的时候会抛出一个异常
define("port", default=8000, help="run on the given port", type=int)

# 请求处理函数类，当处理一个请求时，Tornado将这个类实例化，并调用与HTTP请求方法所对应的方法 
class IndexHandler(tornado.web.RequestHandler):
    # 对HTTP的GET请求作出响应
    def get(self):
      # 查询字符串中取得参数greeting的值，如果没有就是第二个参数的作为默认值
        greeting = self.get_argument('greeting', 'Hello')
        # 写入HTTP响应
        self.write(greeting + ', friendly user!')

# 反转类
class ReverseHandler(tornado.web.RequestHandler):
    # 多了一个input，传进来的是匹配正则第一个括号里的内容
    def get(self, input):
        self.write(input[::-1])

# 处理不同路径的请求        
class WrapHandler(tornado.web.RequestHandler):
    # 用于接收HTTP的POST方法的请求
    def post(self):
        # 获取参数
        text = self.get_argument('text')
        width = self.get_argument('width', 40)
        # 用textwrap模块来制定样式写进服务器端的body里
        self.write(textwrap.fill(text, int(width)))

# 主函数入口
if __name__ == "__main__":
    # 解析命令行
    tornado.options.parse_command_line()
    # 创建Application实例，传递参数告诉tornado应该用哪个类来响应请求
    # 参数列表是一个元组列表，列表中的第一个元素是一个用于匹配的正则表达式，第二个是一个RequestHandler类
    # 正则表达式被看作已经包含行开始^和结束锚点$
    app = tornado.web.Application(
        handlers=[
            (r"/reverse/(\w+)", ReverseHandler),
            (r"/wrap", WrapHandler),
            (r"/", IndexHandler)
        ]
    )
    # 将其传递给HTTP server对象
    http_server = tornado.httpserver.HTTPServer(app)
    # 在命令行指定的端口进行监听
    http_server.listen(options.port)
    # 创建IOLoop实例
    tornado.ioloop.IOLoop.instance().start()
```

可以用curl在命令行窗口进行功能测试，get请求后面直接加URL，其中符号前面需要加转义符。post请求加-d 后接参数，最后放URL

运行结束后会返回HTTP状态码，如果出现错误想要自定义返回的东西，可以在RequestHandler类中重写write\_error(self, status_code, **kwargs)的方法，方法内还是用write函数

## GET 和 POST

在万维网世界中，TCP就像汽车，用TCP传输数据的时候很可靠，不会出现丢件少件的情况，但是如果路上的车是无差别的，又会引起混乱，所以HTTP充当的是交通规则的角色，HTTP分了几个服务类别（GET，POST，PUT，DELETE等）

当执行GET请求的时候，要给汽车贴上GET的标签，把传送的数据放在url里便于记录。处理POST请求的时候，贴上post标签，然后把货物放在body里

他们有一个重大区别： GET产生一个TCP数据包，POST产生两个TCP数据包。GET请求的时候，浏览器会把header和data一并发送出去，POST请求的时候浏览器先发送header，服务器响应100 continue，然后再发送data。但是有些浏览器会只发送一次，用GET代替POST优化网站性能

## 安全和幂等

安全，指请求方法不会破坏服务器上的资源

幂等，意思是多次执行相等的操作，结果都是相同的

所以GET是安全且幂等的，POST都不是

## POSTMAN

用来便捷测试web请求情况，其他多不多说了，提几句有关身份验证的东西

一般分为四种，第一种是基础验证，直接把用户名和密码放在请求的header中；第二种Digest auth，复杂一些，生成authorization header；第三和第四种是OAuth 1.0，OAuth 2.0，不清楚

## HTTP

超文本传输协议，超文本是指除了普通的文本之外，还包含图片，视频，超链接，常见的比如Html。所以HTTP 是一个在计算机世界里专门在「两点」之间「传输」文字、图片、音频、视频等「超文本」数据的「约定和规范」。

常见的字段：

> host：客户端发送请求时，用来指定域名，可以访问同一服务器上的不同网站
>
> Content-Length：表明本次回应的数据长度
>
> Connection：客户端要求服务器使用 TCP 持久连接，以便其他请求复用。HTTP/1.1 版本的默认连接都是持久连接，但为了兼容老版本的 HTTP，需要指定 `Connection` 首部字段的值为 `Keep-Alive`
>
> Content-Type：服务器回应的时候告诉客户端本次数据是什么格式
>
> Accept：客户端请求的时候，用Accept字段声明自己接受哪些格式
>
> Content-Encoding：数据的压缩方法，表示服务器返回的数据使用了什么压缩格式
>
> Accept-Encoding：说明自己可以接受哪些压缩方法

## HTTP特性

简单，灵活，易于拓展，应用广泛，跨平台

> 简单：报文格式就是header + body，头部信息也是key-value的格式
>
> 灵活和易于拓展：各类方法允许自定义和扩充，工作在OSI第七层，HTTPS在HTTP和TCP层之间增加了SSL/TLS安全传输层，HTTP/3把TCP层换成了基于UDP的QUIC

无状态，明文传输，不安全

> 无状态：在进行有关联性的操作，如登录->添加购物车->下单->结算->支付的时候，每一次都要问一遍身份信息。可以用Cookie解决，这是一种通过在请求和响应报文中写入Cookie信息来控制客户端状态的方法
>
> 明文传输：F12或者Wireshark抓包可以肉眼查看，为我们的调试工作带来便利，但是也很容易被窃取
>
> 不安全：不验证通信方的身份，可能遭遇伪装。无法验证报文的完整性，所以有可能被篡改

## HTTP/1.1，HTTP/2，HTTP/3

HTTP/1.1相比于1.0

> 长连接：为了改进每发起一个请求都要建立一次TCP连接的问题，持久连接减少了重复建立和断开的额外开销，减轻了服务器端的负载
>
> 管道网络传输：一个请求发出去以后不用等其回来就可以发送第二个请求，可以减少整体的响应时间

HTTP2相比于1.1

> 头部压缩：如果发出多个请求的头是一样或者类似的，协议会消除重复的部分（HPACK算法，客户端和服务器同时维护一张头信息表，所有字段都会存入这个表，生成一个索引号，以后就不再发送同样的字段了，只发送索引号）
>
> 二进制格式：放弃纯文本形式的报文，采用二进制格式，头信息和数据体都是二进制，并且统称为帧
>
> 数据流：每个请求或者回应的所有数据包被称为一个数据流，每个数据流都有一个独一无二的编号，客户端发出的数据流编号为奇数，服务端发送的编号为偶数。客户端还可以指定数据流的优先级，优先级高的请求，服务器就先响应
>
> 多路复用：可以在一个连接中并发多个请求或回应，而不用按照顺序一一对应，也就是说响应可能不是顺序的。这样不需要排队等待，消除了队头堵塞问题，降低了延迟，大幅度提高了连接的利用率
>
> 服务器推送：浏览器刚请求HTML的时候，服务器就提前把可能会用到的JS，CSS文件等静态资源主动发送给客户端，减少等待的时间

HTTP3相比于2

> 2的主要问题在于多个HTTP请求在复用一个TCP连接，如果一旦发生了丢包，TCP重传机制，这样在一个TCP连接中所有的HTTP请求都必须等这个丢了的包被重传回来
>
> 3把TCP协议层改成了UDP，为了改进UDP的不可靠性，使用了QUIC协议
>
> QUIC是一个在UDP之上的伪TCP+TLS+HTTP/2的多路复用协议，有自己的一套机制可以保证传输的可靠性，当某个流发生丢包的时候，只会阻塞这个流，其他流不会收到影响
>
> TLS升级成了1.3版本，头部压缩算法也升级为Qpack
>
> QUIC把之前TCP和TLS/1.3的6次交互合并成了3次

## 重提HTTP和HTTPS

中间加入了SSL/TLS安全协议，使得在三次握手之后还要进行SSL/TLS握手过程，才可以进入加密报文传输

HTTP端口号是80，HTTPS端口号是443

针对HTTP的窃听，篡改，冒充风险，采用了信息加密，校验机制和身份证书来应对

## 安全是如何实现的

混合加密，摘要算法，数字证书

> 混合加密： 公开密钥加密方式处理起来比共享密钥加密要慢，但比共享密钥安全。所以HTTPS在通信建立前采用非对称加密的方式交换会话密钥，在通信过程中采用对称加密的会话密钥加密明文数据
>
> 摘要算法：客户端在发送明文之前会通过摘要算法算出明文的指纹，发送的时候把指纹+明文一同加密成密文之后再发送给服务器，服务器解密后，用相同的摘要算法对明文进行指纹计算，比较携带的指纹，若相同就是完整的
>
> 数字证书：客户端先向服务器端索要公钥，然后用公钥加密信息，服务器收到密文后，用自己的私钥进行解密。数字证书是借助了第三方权威机构CA，将公钥放在数字证书里，只要证书是可信的，公钥就是可信的

SSL/TLS 协议基本流程：

- 客户端向服务器索要并验证服务器的公钥
- 双方协议产生会话密钥
- 采用会话密钥进行加密通信

建立的握手阶段描述（1.2四次握手，1.3优化为三次）：

> ClientHello请求：客户端向服务器发送客户端支持的SSL/TLS协议版本，客户端生产的随机数（后续用于生产会话密钥）和客户端支持的密码套件（如RSA加密算法）
>
> SeverHello：服务器发送回应，确认协议版本，服务器生产随机数，用于后续生产会话密钥，确认密码套件，服务器的数字证书
>
> 客户端回应：客户端收到服务器的回应之后，首先通过浏览器或者操作系统中的CA公钥，确认服务器的数字证书的真实性，取出服务器公钥加密报文，发送一个随机数，加密算法改变通知，客户端握手结束通知，同时把摘要算出来供服务端校验
>
> 服务器的最后回应：服务器收到客户端的第三个随机数之后，通过协商的加密算法，计算出本次的会话密钥，发送回应（加密通信算法改变通知，服务器握手结束通知，表示握手阶段结束，同时把之前所有内容发生的数据做个摘要，供客户端校验）

接下来就进入了加密通信，使用普通的HTTP协议，用会话密钥来加密内容

## 数据库连接

亲测在python3上最好用的是Pymysql, 先connect上（关闭用close() )，然后创建一个cursor对象

在其上用execute("sql")方法执行查询语句

fetchone() 方法获取单条数据

fetchall() 方法获取所有数据的列表，每条数据被包装成列表里的一个元组

> 创建表：先DROP TABLE IF EXISTS Tablename，再创建表
>
> 表更改：用 try:   cursor.execute(sql), db.commit()  except:   # 如果发生错误则回滚   db.rollback()

除此之外，还有一些其他类似的方法，比如psycopg2，这是用于连接postgreSQL的。还有sqlalchemy的create_engine，用string中的Template方法把字符串转化为sql，再结合pd.read_sql_query和to_sql方法实现读取和更新

另外，在sqlalchemy中其实也可以绕过sql语句的部分，它作为一个ORM框架，可以把数据库表的一行记录与一个对象互相做自动转换，做法如下：

```python
# 导入:
from sqlalchemy import Column, String, create_engine
from sqlalchemy.orm import sessionmaker
from sqlalchemy.ext.declarative import declarative_base

# 创建对象的基类:
Base = declarative_base()

# 定义User对象:
class User(Base):
    # 表的名字:
    __tablename__ = 'user'

    # 表的结构:
    id = Column(String(20), primary_key=True)
    name = Column(String(20))

# 初始化数据库连接:
engine = create_engine('mysql+mysqlconnector://root:password@localhost:3306/test')
# 创建DBSession类型:
DBSession = sessionmaker(bind=engine)
session = DBSession()
# session有add，commit, close方法
# session.query(User).filter(User.id=='5').one()
```

总结来说就是把表转化为类，把记录转化为对象，把字段转化为对象属性。不同的表对应不同的类，类间的关系可以通过relationship和ForeignKey来实现

