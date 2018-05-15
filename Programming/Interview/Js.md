## Javascript 存储方式
- cookie
    - 存在浏览器
    - 大小 4k 以内
    - 请求头上带数据,增大请求量
    - 主要用于购物车
    - 属性
        - Name
        - Value
        - Domain (作用域)，默认为请求的地址
        - Path(作用路径)，默认为 /
        - Expires/Max-Age(失效时间)
        - Secure(https 协议时生效，默认 false)
    - API
        - `document.cookie="name=coolfe"` 设置
        - `document.cookie.indexOf('cookieName' + '=')`
            - 加上等号的原因是避免在某些 Cookie 的值里有与 cookieName 一样的字符串
        - `document.cookie = "imgList=" + imgList + "; path=/;expires=" + exp.toGMTString()`
- Web Storage
    - localStorage
        - 一直会保存
        - 以键值对(Key-Value)的方式存储
        - 大小 5M
        - API
            - getItem(key) // 取记录
            - setItem(key,value) // 设置记录
            - removeItem(key) // 移除记录
            - clear() // 清除记录
    - sessionStorage
        - 关闭页面后即被清空
## tpc/UDP/Ips

## 链表和数组

## 常见排序

## ssr

## 闭包
- 有权访问另一个函数作用域中的变量的函数
- 优点
    - 可以读取函数内部的变量
    - 可以让这些局部变量保存在内存中，实现变量数据共享
- 缺点
    - 变量都被保存在内存中，内存消耗很大，滥用会造成网页的性能问题

## this
- 全局函数中，this == window 
- 当函数被作为某个对象的方法调用时， this 等于那个对象
```js
// a函数隐性的被window对象调用，所以是undefined
function a() {
    var name = 'coolfe';
    console.log(this.name);
}
a(); // => undefined
```
```js
// this指向调用它的上一级对象，所以是‘coolfe2'
var a = {
    name: 'coolfe',
    b: {
        name: 'coolfe2',
        fun: function() {
            console.log(this.name);
        }
    }
}
a.b.fun(); //=> coolfe2
```
```js
// 函数在赋值时，this指向变为了window对象
var a = {
    name : 'coolfe',
    sayName: function(){
        console.log(this.name);
    }
}
var b = a.sayName;
b(); //=> undefined
```

```js
// 对于构造函数，new 操作符会新建空对象，并使用类似 apply 的方法将 this 指向改为这个空对象
function Name() {
    this.name = 'coolfe';
}
var coolfe = new Name();
console.log(coolfe.name); //=> coolfe
```
## HTTPS && HTTP

## 定时器

## 多线程

## 浏览器渲染

## 跨域

## Redux 的 原理

## React 生命周期

## ES6 了解多少

## 如何理解原型链

## CSRF
- 跨站请求伪造
- 登陆成功一个网站后，访问恶意页面后，页面发了一个恶意请求，浏览器会默认带登陆成功的 cookie 过去，就能完成攻击
- 添加 token
- 添加验证码 

## XSS
- 跨站脚本攻击
- 过滤特殊字符

## JS 执行机制
> 事件循环(Event Loop)是 js 实现异步的一种方法，也是 js 的执行机制。
- macro-task(宏任务)：包括整体代码script，setTimeout，setInterval
- micro-task(微任务)：Promise，process.nextTick
- 事件循环的顺序，决定js代码的执行顺序。进入整体代码(宏任务)后，开始第一次循环。接着执行所有的微任务。然后再次从宏任务开始，找到其中一个任务队列执行完毕，再执行所有的微任务
- 首先判断是同步任务还是异步任务，同步任务直接进入主线程，异步任务会先进入 Event Table 并注册回调函数，回调函数执行好了，回调函数会进入 Event Queue 里面，然后 事件循坏会一直循坏判断 Stack 是否为空，为空的话 Event Queue 里面的函数会依次到 Stack 执行
```js
console.log('1');

setTimeout(function() {
    console.log('2');
    process.nextTick(function() {
        console.log('3');
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
process.nextTick(function() {
    console.log('6');
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})

setTimeout(function() {
    console.log('9');
    process.nextTick(function() {
        console.log('10');
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
})
// 1，7，6，8，2，4，3，5，9，11，10，12
```
```js
const first = () => (new Promise((resovle,reject)=>{
    console.log(3);
    let p = new Promise((resovle, reject)=>{
         console.log(7);
        setTimeout(()=>{
           console.log(5);
           resovle(6); 
        },0)
        resovle(1);
    }); 
    resovle(2);
    p.then((arg)=>{
        console.log(arg);
    });

}));

first().then((arg)=>{
    console.log(arg);
});
console.log(4);
//=> 3, 7, 4, 1, 2, 5
```
