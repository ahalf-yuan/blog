# require & import  
> 参考  
[link-01](https://www.cnblogs.com/libin-1/p/7127481.html)   ---> 内容太多，跳读  
[阮一峰ES6](http://es6.ruanyifeng.com/#docs/module#import)   ---> 教程
 
#### previously  
es6以前，通行但非官方标准：CommonJS 和 AMD  
- ##### node服务端 
主CommonJS使用的require方式  
暴露模块使用 `module.exports和exports`  
加载模块使用全局方法 `require()`  
- ##### AMD的诞生 -- *CommonJS同步加载在浏览器端局限*
CommonJS规范在浏览器环境的局限，比如以下两行代码：  
```javascript
var math = require('math');
math.add(2, 3);
```  
这对服务器端不是一个问题，因为所有的模块都存放在本地硬盘，可以同步加载完成，等待时间就是硬盘的读取时间。  
但是，对于浏览器，这却是一个大问题，因为模块都放在服务器端，等待时间取决于网速的快慢，可能要等很长时间，浏览器处于”假死”状态。  
因此，浏览器端的模块，不能采用”同步加载”（synchronous），只能采用”异步加载”（asynchronous）。这就是AMD规范诞生的背景。

    AMD是”Asynchronous Module Definition”的缩写，意思就是”异步模块定义”。
    它采用异步方式加载模块，模块的加载不影响它后面语句的运行。
    所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。  
    
> ？？AMD实现
    
- ##### CMD规范  
CMD (Common Module Definition), 是seajs推崇的规范，CMD则是依赖就近，用的时候再require。它写起来是这样的： 
```javascript
define(function(require, exports, module) {
	var clock = require('clock');
	clock.start();
});
```  
- ##### AMD和CMD的区别  
AMD和CMD最大的区别是对依赖模块的执行时机处理不同，而不是加载的时机或者方式不同，二者皆为异步加载模块。  
AMD依赖前置，js可以方便知道依赖模块是谁，立即加载；  
而CMD就近依赖，需要使用把模块变为字符串解析一遍才知道依赖了那些模块，这也是很多人诟病CMD的一点，牺牲性能来带来开发的便利性，实际上解析模块用的时间短到可以忽略。

#### Now  
export/import  
- ##### require & import  
  require是运行时加载模块  
  import是静态编译时加载  
  require是请求整个包对象而import是只请求模块中需要的请求的部分  
  
import()函数，完成动态加载

### 问题
- ##### 问题1  [链接](http://imweb.io/topic/582293894067ce9726778be9)  
`why???`  ES6发布的module并没有直接采用CommonJS，甚至连require都没有采用，也就是说require仍然只是node的一个私有的全局方法，module.exports也只是node私有的一个全局变量属性，跟标准半毛钱关系都没有。  








