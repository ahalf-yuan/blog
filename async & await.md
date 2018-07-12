# async & await  
When an async function is called, it returns a Promise. When the async function returns a value, the Promise will be resolved with the returned value.  When the async function throws an exception or some value, the Promise will be rejected with the thrown value.

An async function can contain an await expression, that pauses the execution of the async function and waits for the passed Promise's resolution, and then resumes the async function's execution and returns the resolved value.

Examples:

![](/images/1520508818ev.png)
![](/images/1520509266rf.png)  


> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)  
> [https://tutorialzine.com/2017/07/javascript-async-await-explained](https://tutorialzine.com/2017/07/javascript-async-await-explained)   
> [await-vs-return-vs-return-await](https://jakearchibald.com/2017/await-vs-return-vs-return-await/)  
> [Where Did Async/Await Come from and Why Use It?](https://appendto.com/2017/06/asyncawait-come-use/)  



##
### using async/await with a forEach loop
> [Using async/await with a forEach loop](https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop)  
[Resolve promises one after another (i.e. in sequence)?](https://stackoverflow.com/questions/24586110/resolve-promises-one-after-another-i-e-in-sequence)  

以下这种写法是❌错误的
```js
const arr = [1, 4, 8]

function sleep(time, n) {
	setTimeout(() => {
		console.log(n)
		return n
	}, time)
}

// error
async function print() {
	arr.forEach(async item => {
		await sleep(3000, item)
	})
}
```
✅正确的写法
```js
// in sequence
const arr = [1, 4, 8]

function sleep(time, n) {
	setTimeout(() => {
		console.log(n)
		return n
	}, time)
}

async function print() {
	for (const n of arr) {
		await sleep(1000 * n, n)
	}
}
```

// in parallel
```js
const arr = [1, 4, 8]

function sleep(time, n) {
	setTimeout(() => {
		console.log(n)
		return n
	}, time)
}

async function print() {
	await Promise.all(arr.map(async item => {
		await sleep(3000, item)
	}))
}
```
原因：
>Using Babel will transform async/await to generator function and using forEach means that each iteration has an individual generator function, which has nothing to do with the others. so they will be executed independently and has no context of next() with others. Actually, a simple for() loop also works because the iterations are also in one single generator function.




