---
title: JavaScript 执行机制原理
date: 2020-01-13 10:14:47
tags:
  - 前端
  - 前端面试题
  - JavaScript 执行机制
  - JavaScript event loop
category:
- [前端]
- [JavaScript]
---


# JavaScript 运行机制原理


> “`JavaScript` 是单线程、异步、非阻塞、解释型脚本语言。”

## JavaScript 运行机制

### 同步任务(synchronous)


### 异步任务(asynchronous)


*在所有同步任务执行完之前，任何的异步任务是不会执行的*

**那么有哪些会进入异步任务队列？**
> `setTimeout`和`setlnterval`
> `JavaScript DOM`事件
> `ES6`中的`Promise`
> `Ajax`异步请求


### 微任务(Microtask)与宏任务(Macrotask)

> 异步任务又分为：微任务(Microtask)和宏任务(Macrotask)
> 宏任务队列可以有多个，微任务队列只有一个

**JavaScript异步任务中那些是微任务？那些是宏任务？**

> 微任务包括: `new Promise().then(回调)`, `process.nextTick`, `Object.observe(已废弃)`, `MutationObserver`(`html5`新特性)
> 宏任务包括：`script`(全局任务), `setTimeout`, `setInterval`, `setImmediate`, `I/O`, `UI rendering`。


## 理解`Event Loop`

**单线程如何实现异步？**
> 通过`Event loop`（事件循环）实现，从`Event loop`谈`JavaScript`运行机制



**请看下面例子：**

```javascript
var arr = [1, 2, 3, 4, 5, 6, 7];
for (var i = 0; i < arr.length; i++) {
  setTimeout(function() {
    console.log(i);
  });
};
// 打印出来的结果是7个7
```

思考一下最后结果会输出什么？

**答案：7个7**

**为什么不是按照我们预期的结果来输出？**

`setTimeout()`是个异步定时函数，`JavaScript`是单线程，所以就算延时为0，它也是要等到`for`循环语句执行完了，才到它执行，每执行一次`for`语句就会就会产生一个异步执行，放在等待队列里，所以最后执行时就是输出7个7了

**将上面的代码再进行改造一下：**

```javascript
// 方法一
var arr = [1, 2, 3, 4, 5, 6, 7];
for (let i = 0; i < arr.length; i++) {
  setTimeout(function() {
    console.log(i);
  });
};
// 0, 1, 2, 3, 4, 5, 6

// 方法二
var arr = [1, 2, 3, 4, 5, 6, 7];
for (var i = 0; i < arr.length; i++) {
  setTimeout(function(i) {
    console.log(i);
  }(i));
};
// 0, 1, 2, 3, 4, 5, 6

```


## 参考文章

> [Understanding JS: The Event Loop](https://hackernoon.com/understanding-js-the-event-loop-959beae3ac40)
> [The JavaScript Event Loop: Explained](https://blog.carbonfive.com/2013/10/27/the-javascript-event-loop-explained/)
> [JavaScript 运行机制详解：深入理解Event Loop](https://blog.csdn.net/Rnger/article/details/81908070)
> [阮一峰 - 什么是 Event Loop？](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)
> [阮一峰 - JavaScript 运行机制详解：再谈Event Loop](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)
> [稀土掘金 - 一次性搞懂JavaScript 执行机制](https://juejin.im/post/5b4dfb94f265da0f955cc606)
> [稀土掘金 - 这一次，彻底弄懂 JavaScript 执行机制](https://juejin.im/post/59e85eebf265da430d571f89)
> [稀土掘金 - 从浏览器多进程到JS单线程，JS运行机制最全面的一次梳理](https://juejin.im/post/5a6547d0f265da3e283a1df7#heading-6)
> [稀土掘金 - 微任务、宏任务与Event-Loop](https://juejin.im/post/5b73d7a6518825610072b42b)
> [Mozilla Developer Networks - Worker](https://developer.mozilla.org/en-US/docs/Web/API/Worker)
> [详解JavaScript中的Event Loop（事件循环）机制](https://zhuanlan.zhihu.com/p/33058983)
> [深入浅出JavaScript运行机制](https://segmentfault.com/a/1190000016834449)
