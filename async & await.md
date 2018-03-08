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
