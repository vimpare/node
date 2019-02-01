Node.js主要分为四大部分，Node Standard Library，Node Bindings，V8，Libuv
* Node Standard Library 是我们每天都在用的标准库，如Http, Buffer 模块
* Node Bindings 是沟通JS 和 C++的桥梁，封装V8和Libuv的细节，向上层提供基础API服务
* 这一层是支撑 Node.js 运行的关键，由 C/C++ 实现。
    * V8 是Google开发的JavaScript引擎，提供JavaScript运行环境，可以说它就是 Node.js 的发动机。
    * Libuv 是专门为Node.js开发的一个封装库，提供跨平台的异步I/O能力.
    * C-ares：提供了异步处理 DNS 相关的能力。
    * http_parser、OpenSSL、zlib 等：提供包括 http 解析、SSL、数据压缩等其他的能力。
    
    Talk is cheap, show me the code
    
