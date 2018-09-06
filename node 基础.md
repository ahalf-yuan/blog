# node 基础

#### 闭包  
可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。
- 闭包有三个特性：
  1. 函数嵌套函数
  2. 函数内部可以引用外部的参数和变量
  3. 参数和变量不会被垃圾回收机制回收
- 闭包有什么用，使用场景  
之前**模块化**时，当我们需要在模块中定义一些变量，并希望这些变量一直保存在内存中但又不会“污染”全局的变量时，就可以用闭包来定义这个模块。  
高阶函数  
保护函数内的变量安全：如迭代器、生成器   
- 闭包的缺点  
闭包的缺点就是常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。

#### 可迭代对象和迭代器  
> https://juejin.im/post/5a31d4b66fb9a045211eb727 

![](/images/1536215780pr.png)   
**对象可迭代**：：某个对象实现了[Symbol.iterator]属性（函数），返回一个**迭代器**，迭代器对象有一个next方法，调用next方法可遍历对象数据，返回形如`{ value: undefined, done: true }`  
```js
const arr = [1, 3, 5, 7];
arr[Symbol.iterator] = function () {
  const ctx = this;
  const { length } = ctx;
  let index = 0;
  return {
    next: () => {
      if (index < length) {
        return { value: ctx[index++] * 2, done: false };
      } else {
        return { done: true };
      }
    }
  };
};

[...arr];       // [2, 6, 10, 14]

```

- String, Array, TypedArray, Map 和 Set 是 Javascript 中内置的可迭代对象  
- **数组解构**也会默认使用迭代器进行迭代  

**生成器既是可迭代对象也是迭代器**  
```js
const counter = (function* () {
  let c = 0;
  while(true) yield ++c;
})();

counter.next();   // { value: 1, done: false }，counter 是一个迭代器

counter[Symbol.iteratro]();
// counterGen {[[GeneratorStatus]]: "suspended"}， counter 是一个可迭代对象
```
- 生成器函数内部通过 `yield` 提前返回  
- 生成器的 `return` 方法会结束生成器

**生成器的异步应用**  
**co模块**：使用递归函数反复去执行 yield 语句，直到生成器函数迭代结束，co 模块是基于 Promise 实现的。
```js
// co 模块接受生成器函数，并且返回一个 Promise 对象

const promise = co(function* () {
  return yield Promise.resolve('Hello, co!');
})
promise
  .then(val => console.log(val))   // Hello, co!
  .catch((err) => console.error(err.stack));
```

#### async await  
https://davidwalsh.name/async-generators  

#### promise 相关  
- catch 后 then 还可以继续执行吗？
> [ES6 Promise Catch后面的then还是会执行？](https://www.zhihu.com/question/48765053)  

回答：catch 也返回了一个新Fulfilled状态的Promise，所以可以继续

- 
 
#### HTTP
> [HTTP/2.0 相比1.0有哪些重大改进？](https://www.zhihu.com/question/34074946)

- http 1.0  
浏览器对相同域名的请求会做出限制，所以 有的优化将静态资源放在多个 域名下  
- http 2.0  
（1）多路复用  
HTTP 基于 TCP，第一，TCP建立连接的消耗可以省略；第二，克服 TCP 慢启动的特点。  
（2）头部压缩  
（3）server push ？？？  

#### Objet 和 Map
都是hash结构，Map 的 key 不限于 字符串。。。

#### 项目 

pm2:  
process:  
config: 

#### 数据处理
1. flume: 收集日志
2. Kafka：消息队列，类似管道
3. storm: storm 拓扑处理数据
input 组件，output组件，bolt处理逻辑
4. es 或 hive

#### koa
类似 时间模型的 捕获和冒泡 阶段，next 之前类似捕获，next之后类似冒泡
介于请求 和 返回之间的处理过程，每个中间件完成特定的功能，用 next 来衔接

#### node 的优势：
服务端渲染 + 擅长 IO 密集型  

传统的网络服务技术，是每个新增一个连接（请求）便生成一个新的线程，这个新的线程会占用系统内存，最终会占掉所有的可用内存。而 Node.js 仅仅只运行在一个单线程中，使用非阻塞的异步 I/O 调用，所有连接都由该线程处理，在 libuv 的加分下，可以允许其支持数万并发连接（全部挂在该线程的事件循环中）
单线程带来的问题：
避免线程挂掉，如果处理了CPU密集型任务，或者异常阻塞，会导致整个服务失去反应。  


