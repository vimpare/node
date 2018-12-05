Chrome V8 是 JavaScript 引擎
Node.js 内置 Chrome V8 引擎，所以它使用的 JavaScript 语法
JavaScript 语言的一大特点就是单线程，也就是说，同一个时间只能做一件事
Node不是语言，不是框架，只是基于V8运行时环境
异步是解决并发的最佳实践

c语系:
函数化的语言风格
指针支持
判断和循环


OO(Object Oriented,面向对象

ypeScript 的强大之处是要用过才知道的。

1）规模化编程，像Java那种，静态类型，面向对象，前端只有TypeScript能做到
2）亲爹是微软安德斯·海尔斯伯格，不知道此人的请看borland传奇去
3）开源，未来很好
4）组合拳：TypeScript + VSCode = 神器

Node.js的异步是整个学习Node.js过程中重中之重
异步流程控制学习重点
2）Api写法：Error-first Callback 和 EventEmitter
3）中流砥柱：Promise
4）终极解决方案：Async/Await

Node.js 文档里最常采用下面这样的回调方式：

function(err, res) {
  // process the error and result
}

回调函数的第一个参数返回的error对象，如果error发生了，它会作为第一个err参数返回，如果没有，一般做法是返回null。
回调函数的第二个参数返回的是任何成功响应的结果数据。如果结果正常，没有error发生，err会被设置为null，并在第二个参数就出返回成功结果数据

EventEmitter

事件模块是 Node.js 内置的对观察者模式“发布/订阅”（publish/subscribe）的实现，通过EventEmitter属性，提供了一个构造函数。该构造函数的实例具有 on 方法，可以用来监听指定事件，并触发回调函数。任意对象都可以发布指定事件，被 EventEmitter 实例的 on 方法监听到。

在node 6之后，可以直接使用require('events')类
```
var EventEmitter = require('events')
var util = require('util')

var MyEmitter = function () {
 
}

util.inherits(MyEmitter, EventEmitter)

const myEmitter = new MyEmitter();

myEmitter.on('event', (a, b) => {
  console.log(a, b, this);
    // Prints: a b {}
});

myEmitter.emit('event', 'a', 'b');
```

使用 Dash 或 Zeal 查看离线文档，经常查看离线文档，对Api理解会深入很多

var promise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…

  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});
每个Promise定义都是一样的，在构造函数里传入一个匿名函数，参数是resolve和reject，分别代表成功和失败时候的处理。
如果Promise成功执行resolve了，那么它就会将resolve的值传给最近的then函数，作为它的then函数的参数。如果出错reject，那就交给catch来捕获异常就好了。


response.redirect方法允许网址的重定向。
