### Cookie的处理流程
* 服务器向客户端发送Cookie。
* 客户端浏览器将Cookie保存。
* 之后浏览器每次向服务器发起http请求都会将Cookie发送给服务器。

### 服务器向客户端发送Cookie
服务器向客户端发送Cookie通过HTTP响应报文实现，在Set-Cookie中设置需要向客户端发送的Cookie。
```
Set-Cookie: "name=value;domain=.domain.com;path=/;expires={date};HttpOnly;secure"
```

参数|说明
:--|:--
name|一个唯一确定的cookie名称，通过cookie的名称不区分大小写
value|存储在cookie中的字符串值
domain|表示cookie对哪个域是有效的。
path|表示这个cookie影响到的路径，浏览器会根据这项配置，向指定域中匹配的路径发送cookie
expires|设置cookie失效时间，如不设置此值，浏览器将在关闭时删除所有cookie
max-age|与expires作用相同，告诉浏览器此cookie多久后过期。正常情况下，其优先级高于expires
HttpOnly|告知浏览器不允许通过脚本document.cookie去更改这个值，同时对document.cookie也不可见。但在http请求时仍然会带上这个cookie
secure|安全标志，指定后只有在使用SSL链接时才能将cookie发送到服务器，否则不传递

### 服务器端处理Cookie
服务器端可通过HttpServletRequest获取客户端发起的http请求中携带的Cookie信息。其中javax.servlet.http.Cookie封装了客户端发送来的Cookie对象。
