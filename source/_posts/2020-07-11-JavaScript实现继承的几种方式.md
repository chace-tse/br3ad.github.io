---
title: JavaScript实现继承的几种方式
date: 2020-06-29 20:30:16
tags:
- 前端
- 前端基础
- JavaScript
- JavaScript 继承
category:
- [前端]
- [JavaScript]
---

## 面向对象程序设计（Object-oriented programming，OOP）

**什么是面向对象编程？（OOP）**

> 面向对象编程程序设计（Object-oriented programming，OOP） 是种具有对象概念的程序设计范型，同时也是一种程序开发的抽象方针。它可能包含数据、属性、代码与方法。对象则指的是类的实例。它将对象作为程序的基本单元，将程序和数据封装其中，以提高软件的重用性、灵活性和扩展性。————[维基百科](https://zh.wikipedia.org/zh-cn/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)

**面向对象都有哪些特性？**

> 封装性（Encapsulation）
> 继承性（Inheritance）
> 多态性（Polymorphism）
> 抽象性（Abstraction）

## 原型（Prototype）和原型链（Prototype chain）

**什么是原型以及什么是原型链**

> 原型：

> `prototype`属性：每一个函数都有一个`prototype`属性，这个属性是指向一个对象的引用，这个对象称作“原型对象”（prototype object）每一个函数都包含不同的原型对象。将函数用作构造函数的时候，新创建的对象会从原型对象上继承属性和方法。
> 原型链（prototype chain）：

## JavaScript中实现对象的继承

> 大部分面向对象的编程语言，都是通过“类”（class）实现对象的继承。传统上，**JavaScript语言的继承不通过class，而是通过“原型对象”（prototype）实现**

**面向对象程序（OOP）设计的目的是什么？**
> 在编程中促进更好的**灵活性**和**可维护性**，在大型软件工程中广为流行。凭借其对模块化的重视，面向对象的代码开发更简单，更容易理解，相比非模块化编程方法，它能更直接地分析, 编码和理解复杂的情况和过程。

**JavaScript 继承机制的设计思想就是，原型对象的所有属性和方法，都能被实例对象共享**

### 原型链（Prototype chain）继承

### 借用构造函数继承

### 组合继承

### 原型式继承

### 寄生式继承

### 寄生组合式继承

### 混入方式继承多个对象

### [`Object.create`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)实现类式继承

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
> [JavaScript常用八种继承方案](https://juejin.im/post/5bcb2e295188255c55472db0)
> [JavaScript实现继承的多种方式（ES5）](https://juejin.im/post/5b188852e51d4506df277095)
> [JavaScript面向对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)
> [阮一峰-Javascript继承机制的设计思想](http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html)
> [阮一峰-javascript继承思想](Javascript继承机制的设计思想)
> [阮一峰-javascript教程-对象与继承](https://javascript.ruanyifeng.com/oop/prototype.html)
> [阮一峰-javascript教程-对象的继承](https://wangdoc.com/javascript/oop/prototype.html)
> [阮一峰-面向对象编程的模式](https://javascript.ruanyifeng.com/oop/pattern.html)
> [阮一峰-Javascript 面向对象编程（一）：封装](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html)
> [阮一峰-Javascript面向对象编程（二）：构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)
> [阮一峰-Javascript面向对象编程（三）：非构造函数的继承](https://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)
> [阮一峰-面向对象编程](https://www.bookstack.cn/read/javascript-tutorial/16049))
