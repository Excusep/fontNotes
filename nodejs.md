#### nodejs

http://www.runoob.com/nodejs/nodejs-callback.html

简单的说 Node.js 就是运行在服务端的 JavaScript。

Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。

Node.js 是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。



##### nodejs三部分

* 引入required模块

  ```
  // require指令来载入http模块	
  var http = require("http");
  ```

* 创建服务器

  ```
  
  var http = require('http');
  
  http.createServer(function (request, response) {
  
      // 发送 HTTP 头部 
      // HTTP 状态值: 200 : OK
      // 内容类型: text/plain
      response.writeHead(200, {'Content-Type': 'text/plain'});
  
      // 发送响应数据 "Hello World"
      response.end('Hello World\n');
  }).listen(8888);
  
  // 终端打印如下信息
  console.log('Server running at http://127.0.0.1:8888/');
  ```

  

* 接受请求与相应请求



##### REPL（交互式解释器）

表示一个电脑的环境

* 读取：读取用户输入，解析输入了Javascript 数据结构并存储在内存中 
* 执行：执行输入的数据结构 
* 打印：输出结果 
* 循环：循环操作以上步骤直到用户两次按下 **ctrl-c** 按钮退出



##### Buffer

Buffer 提供了以下  API 来创建 Buffer 类：

- **Buffer.alloc(size[, fill[, encoding]])：** 返回一个指定大小的 Buffer 实例，如果没有设置 fill，则默认填满 0
- **Buffer.allocUnsafe(size)：** 返回一个指定大小的 Buffer 实例，但是它不会被初始化，所以它可能包含敏感的数据
- **Buffer.allocUnsafeSlow(size)**
- **Buffer.from(array)：** 返回一个被 array 的值初始化的新的 Buffer 实例（传入的 array 的元素只能是数字，不然就会自动被 0 覆盖）
- **Buffer.from(arrayBuffer[, byteOffset[, length]])：** 返回一个新建的与给定的 ArrayBuffer 共享同一内存的 Buffer。
- **Buffer.from(buffer)：** 复制传入的 Buffer 实例的数据，并返回一个新的 Buffer 实例
- **Buffer.from(string[, encoding])：** 返回一个被 string 的值初始化的新的 Buffer 实例



Node.js 目前支持的字符编码包括：

- **ascii** - 仅支持 7 位 ASCII 数据。如果设置去掉高位的话，这种编码是非常快的。
- **utf8** - 多字节编码的 Unicode 字符。许多网页和其他文档格式都使用 UTF-8 。
- **utf16le** - 2 或 4 个字节，小字节序编码的 Unicode 字符。支持代理对（U+10000 至 U+10FFFF）。
- **ucs2** - **utf16le** 的别名。
- **base64** - Base64 编码。
- **latin1** - 一种把 **Buffer** 编码成一字节编码的字符串的方式。
- **binary** - **latin1** 的别名。
- **hex** - 将每个字节编码为两个十六进制字符。





##### **request** 和 **response** 对象的具体介绍：

（一）Request 对象 -  request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性。

* req.app：当callback为外部文件时，用req.app访问express的实例
* req.baseUrl：获取路由当前安装的URL路径
* req.body / req.cookies：获得「请求主体」/ Cookies
* req.fresh / req.stale：判断请求是否还「新鲜」
* req.hostname / req.ip：获取主机名和IP地址
* req.originalUrl：获取原始请求URL
* req.params：获取路由的parameters
* req.path：获取请求路径
* req.protocol：获取协议类型
* req.query：获取URL的查询参数串
* req.route：获取当前匹配的路由
* req.subdomains：获取子域名
* req.accepts()：检查可接受的请求的文档类型
* req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages：返回指定字符集的第一个可接受字符编码
* req.get()：获取指定的HTTP请求头
* req.is()：判断请求头Content-Type的MIME类型



（二）Response 对象  - response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据。

* res.app：同req.app一样
* res.append()：追加指定HTTP头
* res.set()在res.append()后将重置之前设置的头
* res.cookie(name，value [，option])：设置Cookie
* opition: domain / expires / httpOnly / maxAge / path / secure / signed
* res.clearCookie()：清除Cookie
* res.download()：传送指定路径的文件
* res.get()：返回指定的HTTP头
* res.json()：传送JSON响应
* res.jsonp()：传送JSONP响应
* res.location()：只设置响应的Location HTTP头，不设置状态码或者close response
* res.redirect()：设置响应的Location HTTP头，并且设置状态码302
* res.render(view,[locals],callback)：渲染一个view，同时向callback传递渲染后的字符串，如果在渲染过程中有错误发生next(err)将会被自动调用。callback将会被传入一个可能发生的错误以及渲染后的页面，这样就不会自动输出了。
* res.send()：传送HTTP响应
* res.sendFile(path [，options][，fn])：传送指定路径的文件 -会自动根据文件extension设定Content-Type
* res.set()：设置HTTP头，传入object可以一次设置多个头
* res.status()：设置HTTP状态码
* res.type()：设置Content-Type的MIME类型