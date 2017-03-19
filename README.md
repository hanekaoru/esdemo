## http 协议

http 协议是 超文本传输协议（Hyper Text Transfer Protocol）的缩写，是用于从万维网服务器传输超文本到本地浏览器的传送协议

http 是一个基于 TCP/IP 通信协议来传递数据（html文件，图片，查询结果等）

## http 工作原理

http 协议工作于 客户端-服务端 架构为上，浏览器作为 http 客户端通过 url 向 http 服务端（即 web 服务器）发送请求

web 服务器有：Apache服务器，IIS服务器等

web 服务器根据接收到的请求后，向客户端发送响应信息

http 默认端口号为 80，也是也可以更改为 8080 等其他端口

#### http 三点注意事项：

* http 是无链接：无连接的含义是限制每次连接只处理一个请求，服务器处理完客户的请求，并收到客户的应答后，即断开连接，采用这种方式可以节省传输时间

* http 是媒体独立的：这意味着，只要客户端和服务器知道如何处理的数据内容，任何类型的数据都可以通过 http 发送，客户端以及服务器指定使用适合的 mime-type 内容类型

* http 是无状态：http 协议是无状态协议，无状态是指协议对于事物处理没有记忆能力，缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大，另一方面，在服务器不需要先前信息的时候它的应答就较快

下图展示了 http 协议通信流程：

![img](http://www.runoob.com/wp-content/uploads/2013/11/cgiarch.gif)


## http 消息结构

http 是基于 客户端/服务端（C/S）的架构模型，通过一个可靠的链接来交换信息，是一个无状态的 请求/响应 协议

一个 http "客户端" 是一个应用程序（web 浏览器或其他任何客户端），通过连接到服务器达到向服务器发送一个或多个 http 的请求的目的

一个 http "服务器" 同样也是一个应用程序（通常是一个 web 服务，如 Apache Web 服务器或者 IIS 服务器等），通过接收客户端的请求并向客户端发送 http 响应数据

http 使用统一资源标识符（URL）来传输数据和建立连接


## 客户端请求消息

客户端发送一个 http 请求到服务器的请求消息包括以下格式：请求行（request line），请求头部（header），空行和请求数据四个部分组成，如下图所示：

![img](http://www.runoob.com/wp-content/uploads/2013/11/2012072810301161.png)



## 客户端响应消息

http 响应也由四个部分组成：状态行，消息报头，空行和响应正文

![img](http://www.runoob.com/wp-content/uploads/2013/11/httpmessage.jpg)


## 实例

一个典型的使用 GET 来传递数据的实例：

客户端请求：

```js
GET /hello.txt HTTP/1.1
User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3
Host: www.example.com
Accept-Language: en, mi
```

服务端响应：

```js
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2009 12:28:53 GMT
Server: Apache
Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
ETag: "34aa387-d-1568eb00"
Accept-Ranges: bytes
Content-Length: 51
Vary: Accept-Encoding
Content-Type: text/plain
```

输出结果：

```js
Hello World! My payload includes a trailing CRLF.
```
