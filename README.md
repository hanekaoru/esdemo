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

```html
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



## http 请求方法

根据 http 标准，http 请求可以使用多种请求方式

http 1.0 定义了三种请求方法：GET, POST 和 HEAD 方法

http 2.0 新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法

* GET	请求指定的页面信息，并返回实体主体。

* HEAD 类似于 get 请求，只不过返回的响应中没有具体的内容，用于获取报头

* POST 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致 新的资源的建立 或 已有资源的修改

* PUT	从客户端向服务器传送的数据取代指定的文档的内容

* DELETE 请求服务器删除指定的页面

* CONNECT	HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器

* OPTIONS	允许客户端查看服务器的性能

* TRACE 回显服务器收到的请求，主要用于测试或诊断



## http 响应头信息

* Allow 服务器支持哪些请求方法（如 GET、POST 等）

* Content-Encoding 文档的编码（Encode）方法。只有在解码之后才可以得到 Content-Type 头指定的内容类型。利用 gzip 压缩文档能够显著地减少 HTML 文档的下载时间。因此，Servlet 应该通过查看 Accept-Encoding 头（即 ```request.getHeader("Accept-Encoding")```）检查浏览器是否支持 gzip，为支持 gzip 的浏览器返回经 gzip 压缩的 HTML 页面，为其他浏览器返回普通页面

* Content-Length 表示内容长度。只有当浏览器使用持久 HTTP 连接时才需要这个数据。如果你想要利用持久连接的优势，可以把输出文档写入 ByteArrayOutputStream，完成后查看其大小，然后把该值放入 Content-Length 头，最后通过 ```byteArrayStream.writeTo(response.getOutputStream()``` 发送内容

* Content-Type 表示后面的文档属于什么 MIME 类型。Servlet 默认为 text/plain，但通常需要显式地指定为 text/html。由于经常要设置 Content-Type，因此 HttpServletResponse 提供了一个专用的方法 ```setContentType```

* Date 当前的 GMT 时间。你可以用 setDateHeader 来设置这个头以避免转换时间格式的麻烦

* Expires 应该在什么时候认为文档已经过期，从而不再缓存它

* Last-Modified 文档的最后改动时间。客户可以通过 If-Modified-Since 请求头提供一个日期，该请求将被视为一个条件 GET，只有改动时间迟于指定时间的文档才会返回，否则返回一个 304（Not Modified）状态。Last-Modified 也可用 setDateHeader 方法来设置

* Location 表示客户应当到哪里去提取文档。Location 通常不是直接设置的，而是通过 HttpServletResponse 的 sendRedirect 方法，该方法同时设置状态代码为 302

* Refresh 表示浏览器应该在多少时间之后刷新文档，以秒计。除了刷新当前文档之外，你还可以通过 ```setHeader("Refresh", "5; URL=http://host/path")``` 让浏览器读取指定的页面，注意这种功能通常是通过设置 HTML 页面 HEAD 区的 ```＜META HTTP-EQUIV="Refresh" CONTENT="5;URL=http://host/path"＞``` 实现，这是因为，自动刷新或重定向对于那些不能使用 CGI 或 Servlet 的 HTML 编写者十分重要。但是，对于 Servlet 来说，直接设置 Refresh 头更加方便。 注意 Refresh 的意义是"N 秒之后刷新本页面或访问指定页面"，而不是"每隔 N 秒刷新本页面或访问指定页面"。因此，连续刷新要求每次都发送一个 Refresh 头，而发送 204 状态代码则可以阻止浏览器继续刷新，不管是使用 Refresh 头还是 ```＜META HTTP-EQUIV="Refresh" ...＞```。 注意 Refresh 头不属于 HTTP 1.1 正式规范的一部分，而是一个扩展，但 Netscape 和 IE 都支持它

* Server 服务器名字。Servlet 一般不设置这个值，而是由 Web 服务器自己设置

* Set-Cookie 设置和页面关联的 Cookie。Servlet 不应使用 ```response.setHeader("Set-Cookie", ...)```，而是应使用 HttpServletResponse 提供的专用方法 ```addCookie```

* WWW-Authenticate 客户应该在 Authorization 头中提供什么类型的授权信息？在包含 401（Unauthorized）状态行的应答中这个头是必需的。例如，```response.setHeader("WWW-Authenticate", "BASIC realm=＼"executives＼"")```，注意 Servlet 一般不进行这方面的处理，而是让 Web 服务器的专门机制来控制受密码保护页面的访问（例如.htaccess）



