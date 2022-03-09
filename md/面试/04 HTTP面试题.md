## 1. HTTP状态码知道哪些？分别是什么意思？

​		2开头的表示成功，3开头的表示需要进一步操作，4开头的表示浏览器方面出错，5开头的表示服务器方面出错。

​		像200表示请求成功，201表示请求成功并创建了新的资源，202表示已经接受请求，但未处理完成。

​		301表示资源被永久转移到其它URL，302表示资源被临时转移到其它URL，303表示查看其它地址。

​		400表示客户端请求的语法错误，服务器无法理解，401表示当前请求需要用户身份验证，404表示请求的资源不存在。

​		500表示内部服务器错误，501表示服务器不支持请求的功能，无法完成请求，505表示服务器不支持请求的HTTP协议版本。



## 2. HTTP 缓存有哪几种？

​		有 ETag、Expires 和 CacheControl 。

​		ETag 是通过对比浏览器和服务器资源的特征值（如MD5）来决定是否要发送文件内容，如果一样就只发送 304（not modified）

​		Expires 是设置过期时间（绝对时间），但是如果用户的本地时间错乱了，可能会有问题

​		CacheControl: max-age=3600 是设置过期时长（相对时间），跟本地时间无关。

## 3. GET 和 POST 的区别

- GET 用于获取资源，POST 用于提交资源。
- GET参数通过URL传递，POST放在Request body中。
- GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
- GET请求在URL中传送的参数是有长度限制的，而POST没有。

## 4. Cookie V.S. LocalStorage V.S. SessionStorage V.S. Session

- Cookie V.S. LocalStorage
  1. 主要区别是 Cookie 会被发送到服务器，而 LocalStorage 不会
  2. Cookie 一般最大 4k，LocalStorage 可以有 5Mb 甚至 10Mb（各浏览器不同）
- LocalStorage V.S. SessionStorage
  1. LocalStorage 一般不会自动过期（除非用户手动清除），而 SessionStorage 在会话结束时过期（如关闭浏览器）
- Cookie V.S. Session
  1. Cookie 存在浏览器的文件里，Session 存在服务器的文件里
  2. Session 是基于 Cookie 实现的，具体做法就是把 SessionID 存在 Cookie 里

















