## network
### http
> HTTP的基本优化: 影响一个 HTTP 网络请求的因素主要有两个：带宽和延迟。
#### http1.0

#### http1.1
#### http2.0
#### HTTP1.0和HTTP1.1的一些区别
> 1. 缓存处理，在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准，HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-None-Match等更多可供选择的缓存头来控制缓存策略。

> 2. 带宽优化及网络连接的使用，HTTP1.0中，存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，HTTP1.1则在请求头引入了range头域，它允许只请求资源的某个部分，即返回码是206（Partial Content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。

> 3. 错误通知的管理，在HTTP1.1中新增了24个错误状态响应码，如409（Conflict）表示请求的资源与资源的当前状态发生冲突；410（Gone）表示服务器上的某个资源被永久性的删除。

> 4. Host头处理，在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。HTTP1.1的请求消息和响应消息都应支持Host头域，且请求消息中如果没有Host头域会报告一个错误（400 Bad Request）。

> 5. 长连接，HTTP 1.1支持长连接（PersistentConnection）和请求的流水线（Pipelining）处理，在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在HTTP1.1中默认开启Connection： keep-alive，一定程度上弥补了HTTP1.0每次请求都要创建连接的缺点。

### https/http 区别
1. https需要ca证书，证书一般不是免费的
2. https和http的链接方式是不同的，使用的端口也是不同的，80和443
3. https可以有效防止运营商劫持
4. https使用的是ssl/tls加密的方式，传输都是使用的密文

### SPDY：HTTP1.x的优化
1. 降低延迟，使用多路复用的方式，不同的请求流使用同一个tcp链接
2. 优先级设置，可以设置不通的请求的优先级，让优先级高的请求先加载
3. header压缩，HTTP1.x的header很多时候都是重复多余的，可以选择不通的压缩算法压缩
4. 使用https的加密方式进行加密更安全
5. 服务端推送，如：我请求test.css 会加载test.css，服务端会将会加载test.js的文件推送给客户端.客户端再次尝试获取test.js时就可以直接从缓存中获取到，不用再发请求了。

### http2.0
1. http2.0是spdy的升级版本

#### http2.0和spdy的区别
1. http2.0支持不加密，spdy只支持加密
2. http2.0 header压缩的方式是hpack，spdy是deflate

#### http2.0和HTTP1.x的对比
1. 新的二进制格式
2. 多路复用
3. header压缩
4. 服务端推


### tcp/ip
###