#### axios

###### https://www.npmjs.com/package/axios                           // npm 文档

###### https://www.cnblogs.com/libin-1/p/6607945.html         // csdn 别人翻译的

不再继续维护vue-resource，并推荐大家使用  axios 开始，axios 被越来越多的人所了解。本来想在网上找找详细攻略，突然发现，axios  的官方文档本身就非常详细！！有这个还要什么自行车！！所以推荐大家学习这种库，最好详细阅读其官方文档。大概翻译了一下 axios  的官方文档，相信大家只要吃透本文再加以实践，axios 就是小意思啦！！

如果您觉得本文对您有帮助，不妨点个赞或关注收藏一下，您的鼓励对我非常重要。

## axios 简介

axios 是一个基于Promise 用于浏览器和 nodejs 的 HTTP 客户端，它本身具有以下特征：

------

- 从浏览器中创建 XMLHttpRequest
- 从 node.js 发出 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防止 [CSRF/XSRF](http://baike.baidu.com/link?url=iUceAfgyfJOacUtjPgT4ifaSOxDULAc_MzcLEOTySflAn5iLlHfMGsZMtthBm5sK4y6skrSvJ1HOO2qKtV1ej_)

## 浏览器兼容性

[![img](http://p1.bpimg.com/567571/991b798df8c9a528.png)](http://p1.bpimg.com/567571/991b798df8c9a528.png)

## 引入方式：

## 举个栗子：

------

### 执行 GET 请求

### 执行 POST 请求

### 执行多个并发请求

## axios API

------

可以通过将相关配置传递给 axios 来进行请求。

### axios(config)

### axios(url[, config])

### 请求方法别名

为了方便起见，已经为所有支持的请求方法提供了别名。

- axios.request（config）
- axios.get（url [，config]）
- axios.delete（url [，config]）
- axios.head（url [，config]）
- axios.post（url [，data [，config]]）
- axios.put（url [，data [，config]]）
- axios.patch（url [，data [，config]]）

**注意**
当使用别名方法时，不需要在config中指定url，method和data属性。

### 并发

帮助函数处理并发请求。

- axios.all（iterable）
- axios.spread（callback）

### 创建实例

您可以使用自定义配置创建axios的新实例。

axios.create（[config]）

### 实例方法

可用的实例方法如下所示。 指定的配置将与实例配置合并。

axios＃request（config）
axios＃get（url [，config]）
axios＃delete（url [，config]）
axios＃head（url [，config]）
axios＃post（url [，data [，config]]）
axios＃put（url [，data [，config]]）
axios＃patch（url [，data [，config]]）

## 请求配置

------

这些是用于发出请求的可用配置选项。 只有url是必需的。 如果未指定方法，请求将默认为GET。

使用 then 时，您将收到如下响应：

## 配置默认值

------

您可以指定将应用于每个请求的配置默认值。

### 全局axios默认值

### 自定义实例默认值

### 配置优先级顺序

配置将与优先顺序合并。 顺序是lib / defaults.js中的库默认值，然后是实例的defaults属性，最后是请求的config参数。 后者将优先于前者。 这里有一个例子。

## 拦截器

------

你可以截取请求或响应在被 then 或者 catch 处理之前

如果你以后可能需要删除拦截器。

你可以将拦截器添加到axios的自定义实例。

## 处理错误

------

您可以使用validateStatus配置选项定义自定义HTTP状态码错误范围。

## 消除

------

您可以使用取消令牌取消请求。

> axios cancel token API基于可取消的promise提议，目前处于阶段1。

您可以使用CancelToken.source工厂创建一个取消令牌，如下所示：

您还可以通过将执行器函数传递给CancelToken构造函数来创建取消令牌：

> 注意：您可以使用相同的取消令牌取消几个请求。

## 使用application / x-www-form-urlencoded格式

------

默认情况下，axios将JavaScript对象序列化为JSON。 要以应用程序/ x-www-form-urlencoded格式发送数据，您可以使用以下选项之一。

### 浏览器

在浏览器中，您可以使用URLSearchParams API，如下所示：

> 请注意，所有浏览器都不支持URLSearchParams，但是有一个polyfill可用（确保polyfill全局环境）。

或者，您可以使用qs库对数据进行编码：

### Node.js

在node.js中，可以使用querystring模块，如下所示：

你也可以使用qs库。

## Promise

------

axios 依赖本机要支持ES6 Promise实现。 如果您的环境不支持ES6 Promises，您可以使用polyfill。

## TypeScript

------

axios包括TypeScript定义。

------

axios在很大程度上受到Angular提供的$http服务的启发。 最终，axios努力提供一个在Angular外使用的独立的$http-like服务。





 

 

 

 

 