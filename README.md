# node
在你的项目的根目录下创建一个叫server.js的文件，并写入以下代码：
```
var http = require("http");//请求（require）Node.js自带的 http 模块

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello World");
  response.end();
}).listen(8888);
```
搞定！你刚刚完成了一个可以工作的HTTP服务器。为了证明这一点，我们来运行并且测试这段代码。首先，用Node.js执行你的脚本：

```
node server.js
```
接下来，打开浏览器访问http://localhost:8888/，你会看到一个写着“Hello World”的网页。
**分析：**
我们调用http模块提供的函数： createServer 。这个函数会返回一个对象，这个对象有一个叫做 listen 的方法，这个方法有一个数值参数，指定这个HTTP服务器监听的端口号。

Node.js是事件驱动的  我们创建了服务器，并且向创建它的方法传递了一个函数。无论何时我们的服务器收到一个请求，这个函数就会被调用。我们不知道这件事情什么时候会发生，但是我们现在有了一个处理请求的地方：它就是我们传递过去的那个函数。至于它是被预先定义的函数还是匿名函数，就无关紧要了。

这个就是传说中的 回调 。我们给某个方法传递了一个函数，这个方法在有相应事件发生时调用这个函数来进行 回调

当收到请求时，使用 response.writeHead() 函数发送一个HTTP状态200和HTTP头的内容类型（content-type），使用 response.write() 函数在HTTP相应主体中发送文本“Hello World"。

最后，我们调用 response.end() 完成响应。

我们把我们的服务器脚本放到一个叫做 start 的函数里，然后我们会导出这个函数。

var http = require("http");

function start() {
  function onRequest(request, response) {
    console.log("Request received.");
    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
这样，我们现在就可以创建我们的主文件 index.js 并在其中启动我们的HTTP了，虽然服务器的代码还在 server.js 中。

创建 index.js 文件并写入以下内容：

var server = require("./server");

server.start();
正如你所看到的，我们可以像使用任何其他的内置模块一样使用server模块：请求这个文件并把它指向一个变量，其中已导出的函数就可以被我们使用了.


处理不同的HTTP请求在我们的代码中是一个不同的部分，叫做“路由选择”


需要查看HTTP请求，从中提取出请求的URL以及GET/POST参数:为了解析这些数据，我们需要额外的Node.JS模块，它们分别是url和querystring模块。
现在我们来给onRequest()函数加上一些逻辑，用来找出浏览器请求的URL路径：
```
var http = require("http");
var url = require("url");

function start() {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");
    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

child_process。之所以用它，是为了实现一个既简单又实用的非阻塞操作：exec()。

我们用它来获取当前目录下所有的文件（“ls -lah”）,然后，当/startURL请求的时候将文件信息输出到浏览器中。

https://www.nodebeginner.org/index-zh-cn.html#a-full-blown-web-application-with-nodejs     node入门
