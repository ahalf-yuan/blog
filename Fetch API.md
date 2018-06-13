#  

> [这个API很“迷人”](https://www.w3ctech.com/topic/854)  
[传统 Ajax 已死，Fetch 永生](https://segmentfault.com/a/1190000003810652)  
[That's so fetch!](https://jakearchibald.com/2015/thats-so-fetch/)


**背景**  
js很长时间里通过 XMLHttpRequest(XHR) 进行异步请求，虽说它很有用，但它不是最佳API。它在设计上不符合职责分离原则，将输入、输出和用事件来跟踪的状态混杂在一个对象里。事件模型在处理异步上有点过时了。 

新的 Fetch API打算修正上面提到的那些缺陷，基于 promise 设计。 具体而言，它引入一个实用的函数fetch()用来简洁捕捉从网络上检索一个资源的意图。  
[低版本兼容polyfill](https://github.com/github/fetch)  

**特性检测**  
要检查是否支持Fetch API，可以通过检查 Headers, Request, Response 或者 fetch 在 window 或者 worker 作用域中是否存在。

**----**  
在Fetch API中，最常用的就是fetch()函数。它接收一个URL参数，返回一个promise来处理response。response参数带着一个Response对象。  
Fetch引入了3个接口，它们分别是 **Headers,Request 以及 Response**。他们直接对应了相应的HTTP概念，但是基于安全考虑，有些区别，例如支持CORS规则以及保证cookies不能被第三方获取。

**与XMLHttpRequest的区别**
- API的设计更加简洁
```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', url);
xhr.responseType = 'json';

xhr.onload = function() {
  console.log(xhr.response);
};

xhr.onerror = function() {
  console.log("Oops, error");
};

xhr.send();
```
```javascript
fetch(url).then(function(response) {
  return response.json();
}).then(function(data) {
  console.log(data);
}).catch(function(e) {
  console.log("Oops, error");
});
```
```javascript
fetch(url).then(response => response.json())
  .then(data => console.log(data))
  .catch(e => console.log("Oops, error", e))
```
```javascript
try {
  let response = await fetch(url);
  let data = response.json();
  console.log(data);
} catch(e) {
  console.log("Oops, error", e);
}
// 注：这段代码如果想运行，外面需要包一个 async function

(async () => {
  try {
    let response = await fetch(url);
    let data = response.json();
    console.log(data);
  } catch(e) {
    console.log("Oops, error", e);
  }
})()
```
duang~~ 的一声，使用 await 后，写异步代码就像写同步代码一样爽。await 后面可以跟 Promise 对象，表示等待 Promise resolve() 才会继续向下执行，如果 Promise 被 reject() 或抛出异常则会被外面的 try...catch 捕获。  

- Fetch API足够底层  
因为当前的WHATWG标准定义了XMLHttpRequest.send()方法其实等同于fetch的Requset对象。 Fetch中的Response.body实现了**getReader()方法用于渐增的读取原始字节流**。
```javascript
function streamingDemo() {
  //当数据全部被读完后会将done标记设置为true。 在这种方式下，每次你只需要处理一个chunk，而不是一次性的处理整个响应体。
  var req = new Request(URL, {method: 'GET', cache: 'reload'});
  fetch(req).then(function(response) {
        var reader = response.body.getReader();
        return reader.read();
    }).then(function(result, done) {
        if (!done) {
        // do something with each chunk
        }
    });
} 
```

- 对于传统的XMLHttpRequest而言，你必须使用它的一个实例来执行请求和检索返回的响应。在这种情况下请求和响应基本没法分开，但是通过Fetch API，我们还能够明确的配置请求对象。Request和Response都完全遵循HTTP标准。因此你可以通过Service Worker API将响应发送给你自己。 Service Worker允许通过截取来自浏览器的请求头和提供本地构造的响应头来替换来自服务器的响应头的方式来构建离线应用。除此之外，还可以使用缓存里的内容。 
```javascript
self.addEventListener('fetch', function(event) {
  if (event.request.url === new URL('/', location).href) {
    event.respondWith(
      new Response("<h1>Hello!</h1>", {
        headers: {'Content-Type': 'text/html'}
      })
    )
  }
});
```

- Fetch提供了对'no-cors'的简单处理，当然下面这种情况也无法获取response内部的资源。但这种情况对缓存还是有用的。
```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://www.baidu.com');
xhr.responseType = 'json';

xhr.onload = function() {
  console.log('here');
  console.log(xhr.response);
};

xhr.onerror = function() {
  console.log("Booo");
};

xhr.send();
//XMLHttpRequest cannot load https://www.baidu.com/. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'https://www.zhihu.com' is therefore not allowed access.
// "Booo"
```
```JavaScript
fetch('https://www.baidu.com', {
  mode: 'no-cors'
}).then(function(response) {
  console.log(response.type); // "opaque"
});
```
- XHR缺少流的处理，在request进行时，你可以得到.responseText，但是整个响应还是在缓存进内存，但是使用Fetch，可以获取底层的body流

- Fetch和其他新的API共同使用能发挥更大的作用，比如Cache API，Stream API

- XHR只能同域获取cookie，但是Fetch可以自己配置

- Fetch有Header Class，可以修改读取headers，并且提供了ES6的迭代器来操作