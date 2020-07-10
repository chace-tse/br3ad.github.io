---
title: JavaScript中常用的继承方案
date: 2020-06-29 20:30:16
- 前端
- 前端基础
- JavaScript
- JavaScript 基础
- JavaScript 继承
category:
- [前端]
- [JavaScript]
---

> 大部分面向对象的编程语言，都是通过“类”（class）实现对象的继承。传统上，**JavaScript语言的继承不通过class，而是通过“原型对象”（prototype）实现**

**什么是原型以及什么是原型链**

> 原型（prototype）：
> 原型链（prototype chain）：

**JavaScript 继承机制的设计思想就是，原型对象的所有属性和方法，都能被实例对象共享**

## 原型链继承

## 借用构造函数继承

## 组合继承

## 原型式继承

## 寄生式继承

## 寄生组合式继承

## 混入方式继承多个对象

## [`Object.create`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)实现类式继承

```javascript
// Shape - superclass
function Shape () {
  this.x = 0;
  this.y = 0;
}
// superclass method
Shape.prototype.move = function (x, y) {
  this.x += x;
  this.y += y;
  console.log('Shape moved')
}

// Rectangle - superclass
function Rectangle() {
  Shape.call(this); // call super constructor
}

// subclass extends superclass

```

## ES6 `Class`类继承`extends`

## 参考链接

> [MDM-继承与原型链](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
> [Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)
> [JavaScript常用八种继承方案](https://juejin.im/post/5bcb2e295188255c55472db0)
> [JavaScript实现继承的多种方式（ES5）](https://juejin.im/post/5b188852e51d4506df277095)
> [阮一峰-javascript继承思想](Javascript继承机制的设计思想)
> [阮一峰-javascript教程-对象与继承](https://javascript.ruanyifeng.com/oop/prototype.html)
> [阮一峰-javascript教程-对象的继承](https://wangdoc.com/javascript/oop/prototype.html)
