**express**
基于 Node.js 平台  
```$ npm install express --save```

**Express 应用程序生成器**
express-generator 可以快速创建一个应用的骨架
```npm install express-generator -g```
如下命令创建了一个名称为 myapp 的 Express 应用。此应用将在当前目录下的 myapp 目录中创建，并且设置为使用 Pug 模板引擎（view engine）：
```express --view=pug myapp```
然后安装所有依赖包：
```
$ cd myapp
$ npm install
```
在 Windows 中，通过如下命令启动此应用：

> set DEBUG=myapp:* & npm start
然后在浏览器中打开 http://localhost:3000/ 网址就可以看到这个应用

**Basic routing**

```app.METHOD(PATH, HANDLER)```
* app is an instance of express.
* METHOD is an HTTP request method, in lowercase.
* PATH is a path on the server.
* HANDLER is the function executed when the route is matched

**Routing路由**
column0 | column1
------- | -------
 '/ab+cd' | match abcd, abbcd, abbbcd, and so on.
 '/ab*cd' | match abcd, abxcd, abRANDOMcd, ab123cd, and so on
 /a/ | match anything with an “a” in it.

**Route parameters**

要使用路由参数定义路由，只需在路径路径中指定路由参数，如下所示
```
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params)
})
```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }

Route handlers:
```
app.get('/example/b', function (req, res, next) {
  console.log('the response will be sent by the next function ...')
  next()
}, function (req, res) {
  res.send('Hello from B!')
})
```
```
var cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

var cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

var cb2 = function (req, res) {
  res.send('Hello from C!')
}

app.get('/example/c', [cb0, cb1, cb2])
```

**Response methods**
column0 | column1
------- | -------
res.download() | Prompt a file to be downloaded.
res.end() | End the response process.
res.json() | Send a JSON response.
res.jsonp() | Send a JSON response with JSONP support.
res.redirect() | Redirect a request.
res.render() | Render a view template.
res.send() | Send a response of various types.
res.sendFile() | Send a file as an octet stream.
res.sendStatus() | Set the response status code and send its string representation as the response body.


**app.route()**
```
app.route('/book')
  .get(function (req, res) {
    res.send('Get a random book')
  })
  .post(function (req, res) {
    res.send('Add a book')
  })
  .put(function (req, res) {
    res.send('Update the book')
  })
  ```

  **express.Router**
  Create a router file named birds.js in the app directory, with the following content:
```
var express = require('express')
var router = express.Router()

// middleware that is specific to this router
router.use(function timeLog (req, res, next) {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page')
})
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds')
})

module.exports = router
```
Then, load the router module in the app:
```
var birds = require('./birds')

// ...

app.use('/birds', birds)
```

位于网络传输层（TCP/UDP）与（终端）应用程序之间的软件就称为"中间件,Web服务器就是一种"中间件"，它位于传输层与运行在其上的Web应用（如一个购物网站）之间。
"中间件"可以由很多层的"中间层"有序组成，express的Router就是用来作为独立于应用的"中间层"的对象。
一个Router可以use()其他多个Router，同理一个Application可以use()多个Router
同一个请求会被所匹配route的所有Router的所有handler按照挂载的顺序（沿着"中间件"的栈）进行处理，并沿着反方向进行响应
```
router.use(function(req, res, next) {
    //路由，类似于java中的拦截器功能，在请求到达后台之前，先在这里处理。
    //  some logic here ..
    req.query["name"] = "tom";
    console.info('进入路由，添加一个参数name=tom');
    //next的作用是将请求转发，这个必须有，如果没有，请求到这就挂起了。
    next();
});
```
