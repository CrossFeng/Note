# 创建第一个Node.js应用

1. 引入required模块 
2. 创建服务器
3. 接收请求与响应请求

```javascript
var http = require("http");
```

```javascript
http.createServer(function(request,response){
  response.writeHead(200,{'Content-Type':'text/plain'});
  response.end('Hello World\n');
}).listen(8888);
console.log('Server running at http://127.0.0.1:8888');
```

## 阻塞和非阻塞

```javascript
var fs = require("fs");
var data = fs.readFileSync('input.txt');

console.log(data.toString());
console.log("程序执行结束");
```

非阻塞

```javascript
var fs = require("fs");
fs.readFile('input.txt',function(err,data){
    if(err) return console.error(err);
  	console.log(data.toString());
});
```

## 时间循环

Node.js 事件循环 

Node.js 是单进程应用程序，但是通过事件和回调支持并发，性能很高

```javascript
//引入 events 
var events = require('events');
//创建 对象
var eventEmitter = new events.EventEmitter();
//绑定 事件以及事件处理程序
eventEmitter.on('eventName',eventHandler);
//通过程序触发事件
eventEmitter.emit('eventName');
```

