## cookie && session

## tpc/UDP/Ips

## 链表和数组

## 常见排序

## ssr

## 闭包

## this

## HTTPS && HTTP

## 定时器

## 多线程

## 浏览器渲染

## 跨域

## Redux 的 原理

## React 生命周期

## ES6 了解多少

## 如何理解原型链

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
