#JS相关

[近一万字的ES6语法知识点补充](https://juejin.im/post/5c6234f16fb9a049a81fcca5) 

[每个 JavaScript 工程师都应懂的33个概念](https://github.com/stephentian/33-js-concepts) 

[前端面试题讲解(THIS、构造函数、面向对象、堆栈内存以及闭包)](https://www.bilibili.com/video/av24383268) 

[JavaScript的es6详解](https://www.bilibili.com/video/av25438199) 


##跨域

原因：浏览器同源策略

不同协议，不同域名（不同二级域名），不同端口都会造成跨域

常见的方法 jsonp CORS 

###jsonp

通过动态向HTML插入script标签来请求，只能get，不能post

###CORS 

实现CORS通信的关键是服务器。只要服务器实现了CORS接口，就可以跨源通信。


##浏览器中的Event Loop

**同步任务和异步任务**

Javascript单线程任务被分为**同步任务**和**异步任务**，同步任务会在调用栈中按照顺序等待主线程依次执行，异步任务会在异步任务有了结果后，将注册的回调函数放入任务队列中等待主线程空闲的时候（调用栈被清空），被读取到栈内等待主线程的执行。

![Alt](./images/eventloop.png)

**事件循环的进程模型**

**MacroTask（宏任务）**

setTimeout、setInterval、等

**MicroTask（微任务）**
Promise等。

执行栈在执行完同步任务后，查看执行栈是否为空，如果执行栈为空，就会去检查微任务(microTask)队列是否为空，如果为空的话，就执行Task（宏任务），否则就一次性执行完所有微任务。
每次单个宏任务执行完毕后，检查微任务(microTask)队列是否为空，如果不为空的话，会按照先入先出的规则全部执行完微任务(microTask)后，设置微任务(microTask)队列为null，然后再执行宏任务，如此循环。


摘自[一次弄懂Event Loop](https://juejin.im/post/5c3d8956e51d4511dc72c200) 


**举一些ES6对String字符串类型做的常用升级优化?**

如ES6在String原型上新增了includes()方法，用于取代传统的只能用indexOf查找包含字符的方法(indexOf返回-1表示没查到不如includes方法返回false更明确，语义更清晰),

**举一些ES6对Array数组类型做的常用升级优化**

- 数组解构赋值

在声明较多变量时，不用再写很多let(var),且映射关系清晰，且支持赋默认值

- 扩展运算符
ES6新增的扩展运算符(...)(重要),可以轻松的实现数组和松散序列的相互转化，可以取代arguments对象和apply方法，轻松获取未知参数个数情况下的参数集合。（尤其是在ES5中，arguments并不是一个真正的数组，而是一个类数组的对象，但是扩展运算符的逆运算却可以返回一个真正的数组）。扩展运算符还可以轻松方便的实现数组的复制和解构赋值（let a = [2,3,4]; let b = [...a]）

ES6在Array原型上新增了find()、includes(), fill()

**举一些ES6对Number数字类型做的常用升级优化**

ES6在Number原型上新增了isFinite(), isNaN()方法，用来取代传统的全局isFinite(), isNaN()方法检测数值是否有限、是否是NaN。


**举一些ES6对Object类型做的常用升级优化?(重要)**

语法变得更简洁了，语义更加清晰

 ES6对象也可以像数组解构赋值那样
 
 进行变量的解构赋值.对象的扩展运算符(...)。

```js
let MyOwnMethods = {keys, values, entries}; // let MyOwnMethods = {keys: keys, values: values, entries: entries}
```

ES6在Object原型上新增了assign()方法，用于对象新增属性或者多个对象合并.

ES6在Object原型上还新增了Object.keys()，Object.values()，Object.entries()方法，用来获取对象的所有键、所有值和所有键值对数组


**举一些ES6对Function函数类型做的常用升级优化?**

箭头函数里没有自己的this,这改变了以往JS函数中最让人难以理解的this运行机制。

**箭头函数内的this指向的是函数定义时所在的对象**

**for...in 和for...of有什么区别？**

ES6规定，有所部署了载了Iterator接口的对象(可遍历对象)都可以通过for...of去遍历，而for..in仅仅可以遍历对象

symbol是第六种原始数据类型，所有Symbol()生成的值都是独一无二的，可以从根本上解决对象属性太多导致属性名冲突覆盖的问题。

Set是一种类似数组的新的数据结构，但是它的成员是惟一的，不重复的。（可以轻松实现去重）

Map是Object的超集，打破了一传统键值对形式定义对象，对象的key不再局限于字符串。


摘自[ES6](https://github.com/poetries/FE-Interview-Questions/blob/master/ES6.md) 

**JS垃圾收集机制**

js具有自动回收垃圾的机制，即执行环境会负责管理程序执行中使用的内存。在C和C++等其他语言中，开发者的需要手动跟踪管理内存的使用情况。在编写js代码时候，开发人员不用再关心内存使用的问题，所需内存的分配 以及无用的回收完全实现了自动管理。

**常见的内存泄漏**

1.意外的全局变量

那些用来临时存储大量数据的全局变量，确保在处理完这些数据后将其设置为null或重新赋值。

2.对象的循环引用

3.被遗忘的计时器和回调函数

4.DOM泄漏

JS和DOM互相引用，造成泄漏

**Javascript如何实现继承？**

构造函数绑定：使用 call 或 apply 方法，将父对象的构造函数绑定在子对象上

```javascript
function Cat(name,color){
 　Animal.apply(this, arguments);
 　this.name = name;
 　this.color = color;
}
```

实例继承：将子对象的 prototype 指向父对象的一个实例
```javascript
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;
```

```javascript
 function extend(Child, Parent) {
  　　　var p = Parent.prototype;
  　　　var c = Child.prototype;
  　　　for (var i in p) {
  　　　   c[i] = p[i];
  　　　}
  　　　c.uber = p;
  　 }
```
原型继承：将子对象的 prototype 指向父对象的 prototype
```javascript
 function extend(Child, Parent) {
        var F = function(){};
      　F.prototype = Parent.prototype;
      　Child.prototype = new F();
      　Child.prototype.constructor = Child;
      　Child.uber = Parent.prototype;
    }
```
ES6 语法糖
```javascript
class son extend father{
  constractor(){
    super();
  }
  ...
}
```




**控制台的妙用**

```js
console.dir  查看所有属性
console.table  列表形式列出信息（测试接口非常好用）
getEventListeners(DOM),返回所选DOM上绑定的所有事件
```

**偏函数**

```js
function add(a,b){
  return a+b;
}

function partion(fn,a){
  return function(b){
      return fn(a,b);
  }
}

-----------------------------

function add(a,b){
    return a + b;
}
var obj = {};
obj.parAdd = add.bind(obj,1);
console.log(obj.parAdd(2));//结果3
```
**防抖**
```js
function debounce(fn, wait) {
    var timer = null;
    return function (...arg) {
        if (!timer) {
            timer = setTimeout(() => {
                fn(...arg);

            }, wait)


        } else {
            clearTimeout(timer);
            timer = setTimeout(() => {
                fn(...arg);

            }, wait)
        }

    }

}
```

**实现bind**
```js
Function.prototype.mybind = function(...args) {
    var self = this;//取当前函数
    var content = args.splice(0,1)//取需要绑定的上下文,args剩下的是绑定时传入的参数
    return function(...args2){//args2是绑定返回的新函数出入的参数
        return self.apply(content,args.concat(args2))
    }
}


var a = { a: 1, c: 2 }

function b(...arg) {
    console.log(this);
    console.log(arg);
    // console.log(b);
}
var c = b.mybind(a, 111);
c(222);
```

**手写简单的promise**
```js


个人理解promise其实是一个状态机，就是根据操作去改变状态，然后再根据状态进行相应的操作。

const PENDING = 'pending'
const FULFILLED = 'fulfilled'
const REJECTED = 'rejected'
const RESOLVED = 'resolved'
class myPromise {
    constructor(fn) {//首先要清楚，promise里面,then，all,recace是存在于原型链的，而其他都是自己私有的方法，所以放在constructor里
        this.state = PENDING;
        this.data = null;//初始化当前实例的数据
        this.resolveArr = [];
        this.resolve = (data) => {
            //当我们调用reslove的时候，其实说明我们当前的操作完成了，
            this.state = RESOLVED;//所以我们首先应该改变状态
            this.data = data;//传递拿到的数据

            this.resolveArr.forEach(fn => { fn(this.data) })
            //上面这行代码我觉得很精华，场景一，我们在一开始创建Promise时运行的是同步任务，那我们
            //执行resolve，然后执行then，传递下去。
            // 但是如果我们一开始创建的任务里面是异步的，比如说是进行ajax调用，那我们在调用ajax的时候，浏览器会进行
            // 网络IO，但是继续往下运行代码，因为非阻塞啊，所以then执行，但这个时候，我们data为传递，所以，then执行的
            // 是把用户的处理函数放入队列，等resolve的时候去扫这个队列，如果有任务然后才去执行。

        }
        this.reject = (data) => {
            //reject同resolve
            this.state = REJECTED;
            this.data = data;
        }
        try {//上来直接执行函数，如果出现错误，则catch直接捕捉到执行reject
            fn(this.resolve, this.reject)
        } catch (e) {
            this.reject(e);
        }
    }

    then(resFn, rejFn) {
        //then调用的时候首先先去判断状态，因为then是根据状态然后去调用相应的处理函数
        if (this.state === PENDING) {//代表第一次用户的操作在V8执行到then的时候还没有完成（比如说一开始用户传入了宏任务函数setTimeOut之类）
            //那我们能做的是把用户传入的函数放入一个队列中，等状态改变了然后再执行。
            this.resolveArr.push(resFn);
        } else if (this.state === RESOLVED) {//代表第一次的操作已经完成，而且用户已经调用了resolve,所以我们要执行我们then的处理逻辑
            resFn(this.data)//调用用户传入的成功函数，我们把状态机的数据注入进去
        } else {
            //代表用户调用了reject函数，然后状态机已经为rej状态
            rejFn(this.data)//直接调用用户传入的reject函数，我们注入数据
        }
    }

}

var a = new myPromise((res) => {
    setTimeout(() => { res(1) }, 1000)//注意,setTimeout里面的代码是在then执行之后运行的！
})
a.then((data) => { console.log(data) })



```