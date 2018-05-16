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

## 链表和数组
- 数组是将元素在内存中连续存放，由于每个元素占用内存相同，可以通过下标迅速访问数组中任何元素。但是如果要在数组中增加一个元素，需要移动大量元素，在内存中空出一个元素的空间，然后将要增加的元素放在其中。同样的道理，如果想删除一个元素，同样需要移动大量元素去填掉被移动的元素。如果应用需要快速访问数据，很少或不插入和删除元素，就应该用数组
- 链表恰好相反，链表中的元素在内存中不是顺序存储的，而是通过存在元素中的指针联系到一起。比如：上一个元素有个指针指到下一个元素，以此类推，直到最后一个元素。如果要访问链表中一个元素，需要从第一个元素开始，一直找到需要的元素位置。但是增加和删除一个元素对于链表数据结构就非常简单了，只要修改元素中的指针就可以了。如果应用需要经常插入和删除元素你就需要用链表数据结构了
- 区别
    - 数组静态分配内存，链表动态分配内存
    - 数组在内存中连续，链表不连续 
    - 数组元素在栈区，链表元素在堆区
    - 数组利用下标定位，时间复杂度为O(1)，链表定位元素时间复杂度O(n)
    - 数组插入或删除元素的时间复杂度O(n)，链表的时间复杂度O(1)

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
// 函数在赋值时，this 指向变为了 window 对象
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

## call/apply/bind
- 区别：call/apply 是改变 this 指向立即执行，而 bind 只是改变 this 指向，返回新函数，并且绑定后，this 指向就不会被改变；同时 call/apply 接受多个参数时，apply 需要以数组形式传入
```js
var a = {
    name: 'coolfe',
    sayName: function() {
        console.log(this.name);
    }
}
var b = a.sayName();
b();

b.call(a)
b.apply(a)
b.bind(a)()
```

## HTTPS && HTTP
- 在HTTP(应用层) 和TCP(传输层)之间插入一个SSL协议, 就是HTTPS
- HTTPS经由HTTP进行通信，但利用SSL/TLS来加密数据包。HTTPS开发的主要目的，是提供对网站服务器的身份认证，保护交换数据的隐私与完整性
- 区别
    - HTTP 的 URL 由 “http://” 起始且默认使用端口 80 不同，HTTPS 的 URL 由 “https://” 起始且默认使用端口 443
    - Https 方式访问，客户端到服务器端传输的数据是加密的，即使被截获也没法破解，安全性很高；http 方式访问，账户密码是明文传输的，极易泄露

## ssl，tls
- http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html


## 四次握手
## tpc/UDP/Ips

## 定时器
```js
for(var i = 0; i< 5; i++) {
    setTimeout(function(a){
        console.log(a);
    }(i),5000)
}
```

## 多线程

## 浏览器渲染

## 跨域
- 协议、端口、域名不同都会触发

## Redux 的 原理

## React 生命周期
- state
- props
- 

## ES6 了解多少
- import export
- let const
- 箭头函数
- extends 继承
- Set/Map
- Array.from
- class
- 模块字符串
- Promise
```js
const promise = new Promise(function(resolve, reject) {
  // ... some code
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

## 如何理解原型链
- 试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的__proto__（即它的构造函数的prototype）中寻找

## 浏览器从加载到渲染的过程，比如输入一个网址到显示页面的过程
- 加载过程：
    - 浏览器根据 DNS 服务器解析得到域名的 IP 地址
    - 向这个 IP 的机器发送 HTTP 请求
    - 服务器收到、处理并返回 HTTP 请求
    - 浏览器得到返回内容

- 渲染过程：
    - 根据 HTML 结构生成 DOM 树
    - 根据 CSS 生成 CSSOM
    - 将 DOM 和 CSSOM 整合形成 RenderTree
    - 根据 RenderTree 开始渲染和展示
    - 遇到<script>时，会执行并阻塞渲染

## CSRF
- 跨站请求伪造
- 登陆成功一个网站后，访问恶意页面后，页面发了一个恶意请求，浏览器会默认带登陆成功的 cookie 过去，就能完成攻击
- 验证 Referer 字段
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



## tcp协议，ack，seq
- TCP（Transmission Control Protocol 传输控制协议）是一种面向连接的、可靠的、基于字节流的传输层通信协议

## 三次握手
- 第一次握手：建立连接。客户端发送连接请求报文段，将SYN位置为1，Sequence Number为x；然后，客户端进入SYN_SEND状态，等待服务器的确认；
- 第二次握手：服务器收到SYN报文段。服务器收到客户端的SYN报文段，需要对这个SYN报文段进行确认，设置Acknowledgment Number为x+1(Sequence Number+1)；同时，自己自己还要发送SYN请求信息，将SYN位置为1，Sequence Number为y；服务器端将上述所有信息放到一个报文段（即SYN+ACK报文段）中，一并发送给客户端，此时服务器进入SYN_RECV状态；
- 第三次握手：客户端收到服务器的SYN+ACK报文段。然后将Acknowledgment Number设置为y+1，向服务器发送ACK报文段，这个报文段发送完毕以后，客户端和服务器端都进入ESTABLISHED状态，完成TCP三次握手。

## http2.0头部压缩，cookie只传一次(!)

## cdn 
- 内容分发网络

## 对象浅拷贝
```js
function shallowClone(copyObj) {
    var obj = {};
    for ( var i in copyObj) {
        obj[i] = copyObj[i]
    }
    return obj;
}
var x = {
  a: 1,
  b: { f: { g: 1 } },
  c: [ 1, 2, 3 ]
};
var y = shallowClone(x);
```
```js
var x = {
  a: 1,
  b: { f: { g: 1 } },
  c: [ 1, 2, 3 ]
};
var y = Object.assign({}, x);
```

## 对象深拷贝
```js
var obj={  
    a:{b:10}  
}  
function deep_copy (obj) {  
    //利用递归的方式  
    var newOBJ={};  
    if(typeof obj!='object'){  
        return obj;//终止条件，如果不是对象就放回该值  
    }  
    for (var arrt in obj) {  
        newOBJ[arrt]=deep_copy(obj[arrt]);//再一次拷贝（递归）  
    };  
    return newOBJ;  
}  

var obj2=deep_copy(obj);  
obj2.a.b=20;  
alert(obj.a.b);//10  
```

## 缓存
- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Caching_FAQ
- http://www.alloyteam.com/2012/03/web-cache-2-browser-cache/
- 1、cache-control,expires,中的信息来确定是否使用200
- 2、etag,last-modify来确定是否使用304

## 设计模式（!）
- http://www.alloyteam.com/2012/10/commonly-javascript-design-patterns-simple-factory-pattern/

## JavaScript 事件
- onblur
- onchange
- onclick
- ondblclick
- onfocus
- onkeydown
- onkeyup
- onload
- onmousemove
- onmouseout
- onreset

## async && defer
- 延迟脚本：  defer 浏览器会优先解析完没有 defer 属性的元素代码，会按照书写顺序执行
    - `<script type="text/javascript" defer="defer" src="examplel.js"></script>`
- 异步脚本： async 
    - `<script type="text/javascript" async src="examplel.js"></script>`
- [defer_async]
- 总结： async 和 defer 都是异步，不会影响 HTML 解析，不同的是 async 下载后立即执行， defer 等到全部解析完才执行

## 性能优化
- 减少页面体积，提升网络加载
    - 静态资源的压缩合并（JS 代码压缩合并、CSS 代码压缩合并、雪碧图）
    - 静态资源缓存（资源名称加 MD5 戳）
    - 使用 CDN 让资源加载更快
- 优化页面渲染
    - CSS 放前面，JS 放后面
    - 懒加载（图片懒加载、下拉加载更多）
    - 减少DOM 查询，对 DOM 查询做缓存
    - 减少DOM 操作，多个操作尽量合并在一起执行（DocumentFragment）
    - 事件节流
    - 尽早执行操作（DOMContentLoaded）
    - 使用 SSR 后端渲染，数据直接输出到 HTML 中，减少浏览器使用 JS - 模板渲染页面 HTML 的时间

# webpack配置
- entry
- output
    - path
    - filename
- loader
    - `module: {rules: [{ test: /\.txt$/, use: 'raw-loader' }]}`
- plugins
    - `const HtmlWebpackPlugin = require('html-webpack-plugin');`
    - `plugins: [ new webpack.optimize.UglifyJsPlugin(),]`

## 离线包设计(!)

## js报错监控(!)

### 参考链接
- https://juejin.im/post/5af3cc4af265da0ba3521028
