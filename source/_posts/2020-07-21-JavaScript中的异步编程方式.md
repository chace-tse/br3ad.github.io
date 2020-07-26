---
title: JavaScript中的异步编程方式
date: 2020-07-21 20:56:34
tags:
- 前端
- 前端基础
- 异步编程
- JavaScript异步编程
category:
- [前端]
- [JavaScript]
---

## 前沿

---

## 什么是异步（Asynchronous）？

简单来说就是一个任务分成两段，先执行一段，然后转而执行其他任务，等做好了准备，再回过头执行第二段。

比如，有一个任务是读取文件进行处理，异步的执行过程就是不连续的执行，就叫做异步（Asynchronous），相应地，连续的执行，就叫做同步（Synchronous）

**JavaScript中异步编程的方法有：**

- 回调函数
- 事件监听
- 发布/订阅
- `promise` 对象
- `generator`(ES6)
- `async` / `await`（ES7）

## 回调函数（callback function）

异步回调中最常见的形式可能就是Ajax了：

```javascript

```

## 事件监听

## Promise对象

## 发布/订阅

## `generator`

## `async`/`await`

> [async 函数的含义和用法](http://www.ruanyifeng.com/blog/2015/05/async.html)
> [Generator 函数的含义与用法](http://www.ruanyifeng.com/blog/2015/04/generator.html)
> [Generator 函数的异步应用传统方法](https://es6.ruanyifeng.com/#docs/generator-async)
> [JavaScript中的异步操作](https://www.jianshu.com/p/6f91e7696b91)
> [JavaScript异步编程六种方案](https://juejin.im/post/5c30375851882525ec200027)
