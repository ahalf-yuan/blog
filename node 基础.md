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



