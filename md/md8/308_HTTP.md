# HTTP

## HTTP 与 HTTPS 的区别是什么？

HTTP 是明文传输协议，端口 80，通信不安全；HTTPS 在 HTTP 上加了 TLS 加密，端口 443，可以保证数据加密、身份验证和完整性，适合敏感数据传输。

## HTTP 常用状态码有哪些？

1xx 是信息性状态码，2xx 表示请求成功，3xx 是重定向，4xx 是客户端错误（如 404/401），5xx 是服务器错误（如 500/503）。

* 1xx：信息性状态码
  * 100 Continue：客户端可以继续发送请求主体
  * 101 Switching Protocols：协议切换

* 2xx：成功
  * 200 OK：请求成功
  * 201 Created：资源创建成功
  * 204 No Content：请求成功但无返回内容

* 3xx：重定向
  * 301 Moved Permanently：永久重定向
  * 302 Found：临时重定向
  * 304 Not Modified：资源未修改，使用缓存

* 4xx：客户端错误
  * 400 Bad Request：请求语法错误
  * 401 Unauthorized：未授权，需要认证
  * 403 Forbidden：禁止访问
  * 404 Not Found：资源不存在

* 5xx：服务器错误
  * 500 Internal Server Error：服务器内部错误
  * 502 Bad Gateway：网关错误
  * 503 Service Unavailable：服务不可用
  * 504 Gateway Timeout：网关超时

















