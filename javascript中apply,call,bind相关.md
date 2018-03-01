# javascript中apply,call,bind相关  
- #### apply和call的区别  
```javascript
function func(arg1, arg2){
}

// 调用时参数区别,call 需要把参数按顺序传递进去，而 apply 则是把参数放在数组里
func.bind(this, arg1, arg2)
func.apply(this, [arg1, arg2])
```  
- #### 常用  
1. Array push  
```javascript
let arr1 = ['1', '2', '3']
let arr2 = ['4', '5', '6']
Array.prototype.push.apply(arr1, arr2)

// arr1 results
[ '1', '2', '3', '4', '5', '6' ]
```  
2. Math max, min  
```javascript
let numbers = [5, 458 , 120 , -215 ];
let maxNum = Math.max.apply(Math, numbers)
let minNum = Math.min.apply(Math, numbers)

// results
458
-215
```  
3. isArray
```javascript
function isArray(obj) {
	return Object.prototype.toString.call(obj) === '[object Array]'
}
```  
4. 类（伪）数组使用数组方法    

Javascript中存在一种名为伪数组的对象结构。比较特别的是 `arguments对象`，还有像调用 getElementsByTagName , document.childNodes 之类的，它们返回`NodeList对象`都属于伪数组。不能应用 Array下的 push , pop 等方法。

但是我们能通过 Array.prototype.slice.call 转换为真正的数组的带有 length 属性的对象，这样 domNodes 就可以应用 Array 下的所有方法了。
```javascript  
var domNodes = Array.prototype.slice.call(document.getElementsByTagName("*"))
```  
- ##### 伪数组？ 
> 伪数组是一个含有length属性的json对象，  
按照索引的方式存储数据  
并不具有数组的一些方法，只能能通过Array.prototype.slice转换为真正的数组，并且带有length属性的对象。  

```json
var obj = {"0":"a","1":"b","length":2}; // 伪数组
```  
- ##### 伪数组转换成真正的数组   
`Array.prototype.slice.call(ArrayLike)`   
`[].slice.call(ArrayLike)` 


- ##### 区别  
>	[].slice实际是先创建了一个Array的实例[],然后调用这个实例上的方法，而这个方法是Array的prototype上的，也就是Array.prototype.slice。  
    两种调用的不同：[].slice中的this指向[]实例，Array.prototype.slice的this指向Array.prototype   

- ##### 数组方法的调用？  
	`arr.slice()`，arr实际是Array的实例，调用了Array原型链上的slice方法
```javascript
let arr = ['aa', 'bb', 'cc']
let arr2 = arr.slice()
```
- #### bind
	MDN的解释是：bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind() 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。  
    
```javascript
var foo = {
    bar : 1,
    eventBind: function(){
        $('.someClass').on('click',function(event) {
            /* Act on the event */
            console.log(this.bar);      //1
        }.bind(this));
    }
}
```  
- #### 三者区别  
	区别是，当你希望改变上下文环境之后并非立即执行，而是回调执行的时候，使用 bind() 方法。而 apply/call 则会立即执行函数。  
    
- #### bind的实现  
	“穷人版” 的 polyfill
    ```javascript
    Function.prototype.bind = Function.prototype.bind || function(context) {
      var that = this;
      return function() {
        return that.apply(context, arguments);
      }
    }
    ```  
   以上实现的问题： 
   待补充 
   
   ```javascript
   if (!Function.prototype.bind) {
        Function.prototype.bind = function () {
            var self = this,                        // 保存原函数
                context = [].shift.call(arguments), // 保存需要绑定的this上下文
                args = [].slice.call(arguments);    // 剩余的参数转为数组
            return function () {                    // 返回一个新函数
                self.apply(context,[].concat.call(args, [].slice.call(arguments)));
            }
        }
    }
   ```





