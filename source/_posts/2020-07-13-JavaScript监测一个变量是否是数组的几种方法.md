---
title: JavaScript监测一个变量是否是数组的几种方法
date: 2020-07-13 16:37:41
tags:
- 前端
- 前端基础
- JavaScript
- JavaScript Array
- 监测数组
category:
- [前端]
- [JavaScript]
- [JavaScript原型]
---

**在JavaScript中，数据类型检测有如下方法：**

```javascript
typeof
instanceof
constructor
Object.prototype.toString.call
Array.isArray
```

## [`typeof()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)

> `typeof` 操作符返回一个字符串，表示未经计算的操作数的类型。

```javascript
// 基本类型
console.log(typeof null); // `object`
console.log(typeof '123'); // 'string'
console.log(typeof true); // 'boolean'
console.log(typeof undefined); // 'undefined'
console.log(typeof 123456); // 'number'

// 引用类型
console.log(typeof {}); // 'object'
console.log(typeof []); // 'object'
console.log(typeof Array); // 'function' Array类型的构造函数
console.log(typeof Object); // 'function' Object类型的构造函数
console.log(typeof function(){}); // 'function'
console.log(typeof Symbol); // 'function' Symbol类型的构造函数
console.log(typeof Number); // 'function' Number类型的构造函数
console.log(typeof String); // 'function' String类型的构造函数
console.log(typeof Boolean); // 'function' Boolean类型的构造函数

```

结论： 通过`typeof`肯定是不行的，对于一些基本类型而言，`typeof`是可以判断出数据类型，但是需要判断一些引用类型，不能具体到某一个类型，比如`array`

## 使用[`instanceof`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)

**instanceof是干嘛用的？**

> `instanceof`运算符用于监测构造函数的`prototype`属性是否出现在某个实例对象的原型链（prototype chain）上

简单理解就是：

> 监测某个实例是否属于某个类
> 所有出现在实例原型链上的类都会返回 `true`

使用的语法如下

```javascript
object instanceof constructor
```

举个例子：

```javascript
function Chace() {};
functiong Bar() {};
var c = new Chace();
c instanceof Chace; // true，因为 Object.getPrototypeOf(c) == Chace.prototype

c instanceof Bar; // false，因为Bar.prototype 不在c的原型链上

```

用`instanceof`判断是否数组

```javascript
const a = [];
const b = {};

console.log(a instanceof Array); // true，因为 a.constructor.prototype == Array.prototype;
console.log(a instanceof Object); // true 在数组a的原型链上也能找到Object构造函数 因为, a.constructor.prototype.__proto__.constructor.prototype == Object.prototype;

console.log(b instanceof Array); // false
console.log(b instanceof Object); // true，因为 b.constructor.prototype == Object.prototype;
```

用代码模拟`instanceof`的查找过程：

```javascript
const _instanceof = function (instance, Class) {
  // let proto = instanceof.__proto__
  let proto = Object.getPrototypeOf(instance);
  while (Class.prototype) {
    if (proto == Class.prototype) {
      return true;
    }
    // proto = proto.__proto__
    proto = Object.getPrototypeOf(proto);
  }
  return false;
};
console.log(_instanceof([], Array));
console.log(_instanceof([], Object));
```

使用`instanceof`存在一个问题，假定浏览器只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的`Array`构造函数，如果从一个框架向另一个框架传入一个数组，那么传入的数组与第二个框架中原生创建的数组分别具有各自不同的构造函数，为了解决这个问题，ECMAScript 5中新增了`Array.isArray()`方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的

```javascript
if (Array.isArray(value)) {
  // 对数组执行某些操作
}
```

## 用`constructor`方法

## [`Object.prototype.toString.call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

> `toString()` 方法返回一个表示该对象的字符串。

```javascript

```

## ES5中的API[`Array.isArray()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)

> ES5中新增了一个方法：`Array.isArray()` 用于确定传递的值是否是一个 `Array`。（只支持IE9+、Firefox 4+、Safari 5+、Opera 10.5+和Chrome，IE8之前的版本不兼容）

```javascript
let array = [1, 2, 3];
let obj = { foo: 123 };

Array.isArray(array); // true;
Array.isArray([]); // true;
Array.isArray(obj); // false
Array.isArray(undefined); // false
Array.isArray(null); // false
Array.isArray(Array.prototype); // true
```

**最佳写法：**

```javascript
var arr = [1, 2, 3, 4, 5, 7];
var arr2 = [{ abc: 1, abc: 2}];

function isArrayFn(value) {
  if (typeof Array.isArray === 'function') {
    return Array.isArray(value);
  } else {
    return Object.prototype.toString.call(value) === '[object Array]';
  }
}

console.log(isArrayFn(arr)); // true
console.log(isArrayFn(arr2)); // true
```

## 参考连接

> [MDN-JavaScript `typeof`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)
> [MDN-JavaScript 'instanceof'](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)
> [MDN-JavaScript `Object.toString`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)
> [MDN-JavaScript `Array.isArray`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)
> [MDN-JavaScript `Object.getPrototypeOf()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/GetPrototypeOf)
> [在JavaScript中，如何判断数组是数组？](https://segmentfault.com/a/1190000006150186)
