# day06 http首部

## 通用首部字段

### cache-control 用来操作缓存的工作机制
- public：表明其他用户也可利用缓存
- private：只对特定用户提供资源缓存的服务
- no-cache：不缓存过期的资源
- no-store: 请求或响应包含机密信息，不能缓存
- s-maxage：只适用于供多为用户使用的公共缓存服务器
- max-age：代表资源保存为缓存的最长时间
- min-fresh：要求缓存服务器返回至少还未过指定时间的缓存资源
- max-stale：指示缓存资源，即使过期也照常接受
- only-if-cached：要求缓存服务器不重新加载响应
- must-revalidate：向源服务器再次验证即将返回的响应缓存目前是否有效
- proxy-revalidate：要求所有的缓存服务器在接受到客户端带有该指令的请求返回响应之前，必须再次验证缓存的有效性
- no-transform：无论是在请求还是响应中，缓存都不能改变实体主体的媒体类型

### connection
- 控制不再转发给代理的首部字段
- 管理持久连接

http/1.1版本默认连接都是持久连接

### Date
首部字段Date表明创建http报文的日期和时间

### Pragma
历史遗留字段，仅作为与http/1.0的向后兼容而定义

### Trailer
事先说明在报文主题后记录了哪些首部字段

### Trailer Encoding
规定了传输报文主体时采用的编码方式

### Upgrade
用于检测http协议以及其他协议是否可使用更高版本进行通信

### Via
追踪客户端和服务器之间的请求和响应报文的传输路径

### Warning
告知用户一些与缓存相关问题的警告

## 请求首部字段
### Accept
通知服务器，用户代理能够处理的媒体类型及媒体类型优先级

### Accept-Charset
通知服务器用户代理支持的字符集及字符集的相对优先顺序

### Accept-Encoding
告知服务器用户代理支持的内容编码及内容编码的优先级顺序

### Accept-Language
告知服务器用户代理能够处理的自然语言集以及优先级

### Authorization
告知服务器，用户代理的认证信息（证书值）

### Expect
告知服务器，期望出现的某种特定行为

### From
告知服务器使用用户代理的用户的电子邮件地址

### Host
告知服务器，请求的资源所处的互联网主机名和端口号

### If-Match
服务器会比对If-Match的字段值和资源的ETag值，二者一致才会执行请求。

if-xxx这种央视的请求首部字段，都可成为条件请求。服务器接收到附带条件的请求后，只有判断指定条件为真时，才会执行请求。

### If-Modified-Since
用于确认代理或客户端拥有的本地资源的有效性

### If-None-Match
只有If-None-Match的字段值与ETag值不一致时，可处理该请求。与If-Match首部字段的作用相反。

### If-Range
告知服务器若指定If-Range字段值和请求资源的ETag值或时间相一致时，则作为范围请求处理。反之，则返回全体资源。

### If-Unmodified-Since
告知服务器，指定的请求资源只有在字段值内指定的日期时间之后，未发生更新的情况下，才能处理请求。

### Max-Forwards
服务器在往下一个服务器转发请求之前，Max-Forwards的值减1后重新赋值。当服务器接受到Max-Forwards值为0的请求时，则不进行转发，而是直接返回响应。

### Proxy-Authorization
告知服务器认证所需要的信息

### Range
告知服务器资源的指定范围

### Referer
告知服务器请求的原始资源的URI

### TE
告知服务器客户端能够处理响应的传输编码方式及优先级

### User-Agent
创建请求的浏览器和用户代理名称等信息传达给服务器

## 响应首部字段
### Accept-Ranges
用来告知客户端服务器是否能处理范围请求

### Age
告知客户端，源服务器多久前做了响应

### ETag
告知客户端实体标记

### Location
将响应接受方引导至某个与请求URI位置不同的资源

### Proxy-Authenticate
把代理服务器所要求的认证信息发送给客户端

### Retry-After
告知客户端应该在多久之后再次发送请求

### Server
告知客户端当前服务器上安装的http服务器应用程序的信息

### Vary
对缓存进行控制

### WWW-Authenticate
用于http访问认证

## 实体首部字段
包含在请求报文和响应报文中的实体部分所使用的首部

### Allow
通知客户端能够支持Request-URI指定资源的所有HTTP方法

### Content-Encoding
告知客户端服务器对实体的主体部分选用的内容编码方式
gzip/compress/deflate/identity

### Content-Language
告知客户端实体主体使用的自然语言

### Content-Length
表明了实体主体部分的大小

### Content-Location
报文主体返回资源对应的URI

### Content-MD5
检查报文主体在传输过程中是否保持完整，以便确认传输到达

### Content-Range
告知客户端作为响应返回的实体的哪个部分符合范围请求

### Content-Type
说明了实体主体内对象的媒体类型

### Expires
将资源失效的日期告知客户端

### Last-Modified
指明资源最终修改的时间

## 为Cookie服务的首部字段
cookie的工作机制是用户识别及状态管理

#### expires
指定浏览器可发送Cookie的有效期

#### path
限制指定Cookie的发送范围的文件目录

#### domain
domain属性指定的域名可做到与结尾匹配一致

#### secure
用于限制web页面尽在https安全连接时才可以发送Cookie

#### HttpOnly
使javascript脚本无法获得cookie

## 其他首部字段

#### X-Frame-Options
用于控制网站内容在其他Web网站的Frame标签内的显式问题

#### X-XSS-Protection
真滴跨站脚本共计XSS的一种策略

#### DNT
拒绝个人信息被收集

#### P3P
用于保护个人隐私

