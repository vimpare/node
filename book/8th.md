请求方法存在于报文的第一行的第一个单词，通常是大写。
如下为一个报文头的示例：
```
> GET /path?foo=bar HTTP/1.1> User-Agent: curl/7.24.0 (x86_64-apple-darwin12.0) libcurl/7.24.0 OpenSSL/0.9.8r zlib/1.2.5> Host: 127.0.0.1:1337> Accept: */*>HTTP_Parser
```
在解析请求报文的时候，将报文头抽取出来，设置为req.method。通常，我们只需要处理GET和POST两类请求方法，但是在RESTful类Web服务中请求方法十分重要，因为它会决定资源的操作行为。PUT代表新建一个资源，POST表示要更新一个资源，GET表示查看一个资源，而DELETE表示删除一个资源。


#### 路径解析

路径部分存在于报文的第一行的第二部分，如下所示：
`GET /path?foo=bar HTTP/1.1`

#### 查询字符串
查询字符串位于路径之后，在地址栏中路径后的?foo=bar&baz=val字符串就是查询字符串。这个字符串会跟随在路径后，形成请求报文首行的第二部分。

Node提供了querystring模块用于处理这部分数据，
```
var url = require('url');
var querystring = require('querystring');
var query = querystring.parse(url.parse(req.url).query);
更简洁的方法是给url.parse()传递第二个参数，如下所示：
var query = url.parse(req.url, true).query;
它会将
foo = bar & baz = val解析为一个 JSON对象，如下所示： 
{
    foo: 'bar',
    baz: 'val'
}
```
#### Cookie
如何标识和认证一个用户，最早的方案就是Cookie（曲奇饼）了
告知客户端的方式是通过响应报文实现的，响应的Cookie值在Set-Cookie字段中

    Expires和Max-Age是用来告知浏览器这个Cookie何时过期的，如果不设置该选项，在关闭浏览器时会丢失掉这个Cookie。
    HttpOnly告知浏览器不允许通过脚本document.cookie去更改这个Cookie值
    
    Secure。当Secure值为true时，在HTTP中是无效的，在HTTPS中才有效，表示创建的Cookie只能在HTTPS连接中被浏览器传递到服务器端进行会话验证，如果是HTTP连接则不会传递该信息，所以很难被窃听到。
    
    
一旦服务器端向客户端发送了设置Cookie的意图，除非Cookie过期，否则客户端每次请求都会发送这些Cookie到服务器端，一旦设置的Cookie过多，将会导致报头较大。    
    
  
  
#### Session

Cookie对于敏感数据的保护是无效的。
Ses-sion的数据只保留在服务器端，客户端无法修改

**如何将每个客户和服务器中的数据一一对应起来，这里有常见的两种实现方式。**
  第一种：基于Cookie来实现用户和数据的映射
  第二种：通过查询字符串来实现浏览器端和服务器端数据的对应
    
    
    
    
    
    
    
    
    
    
    
    
    
    
