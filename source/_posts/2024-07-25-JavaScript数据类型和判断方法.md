---
title: JavaScript数据类型和判断方法
date: 2024-07-25 07:43:52
tags: 
  - JavaScript
  - 数据类型
  - 数据类型的判断
categories: 
  - [面试]
  - [前端面试]
  - [JavaScript]
---


## JavaScript 数据类型

___

### 基本数据类型和引用数据类型

- `ECMASciprt`包括两个不同类型的值：基本数据类型和引用数据类型。
- 基本数据类型指的是简单的数据段，引用数据类型指的是有多个值构成的对象。
- 把变量赋值给一个变量时，解析器首先要确认的就是这个值是基本类型值还是引用类型值。

**常见的基本类型：**

> `Number`、`Boolean`、`String`、`null`、`undefined`、`Symbol`（ES6新增）、`BigInt`（ES2020）

**引用类型：**

> `Object`（对象）、`Array`（数组）、`Function`（函数）、`RegExp`(正则)、`Date`(日期)、`Map`（键值对）

## 如何判断数据类型

___

### `typeof`判断

`typeof` 运算符返回一个字符串，表示操作数的类型。`number`、`string`、`boolean`、`object`、`undefined`、`function`。`typeof`可以对基本类型`number`、`string`、`boolean`、`undefined`做出准确的判断（`null`除外，`typeof null==="object"`,这是由于历史的原因)对于引用类型，除了`function`之外返回的都是`object`。

```javascript
  console.log(typeof 123); // "number"
  console.log(typeof "Hello World"); // "string"
  console.log(typeof true); // "boolean"
  console.log(typeof undefined); // "undefined"
  console.log(typeof null)； // "object"
  console.log(typeof {}); // "object"
  console.log(typeof []); // "object"
  console.log(typeof function(){}); // "function"
  console.log(typeof NaN); // "number"
  console.log(typeof document.all); // "undefined"
  console.log(typeof new Date()); // "object"
  console.log(typeof new RegExp()); // "object"
```

### `instanceof`判断

`instanceof` 运算符用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。

#### 语法

```javascript
  object instanceof constructor
```

#### 例子

```javascript
  const arr = [1, 2, 3];
  console.log(arr instanceof Array); // true
  console.log(arr instanceof Object); // true

  const obj = { name: "Chace", age: 31 };
  console.log(obj instanceof Object); // true
  console.log(obj instanceof Array); // false

  function Person(){};
  console.log(new Person() instanceof Person); // true
  console.log(new Person() instanceof Object); // true
```

**注意:**`instanceof`运算符只能用于对象，不适用原始类型的值，且大小写不能错。
请看下面例子：

```javascript
  "hello world" instanceof String // false
  123 instanceof Number; // false
  null instanceof Object // false
  undefined instanceof Object // false
```

### `constructor` 判断

`constructor` 指向创建该实例对象的构造函数

**注意** `null` 和 `undefined` 没有 `constructor`，以及 `constructor` 可以被改写，不太可靠

```javascript
  const arr = [1, 2, 3];
  console.log(arr.constructor === Array); // true

  const obj = {name: "Chace", age: 31};
  console.log(obj.constructor === Object); // true

```

为了规范，在重写对象原型时一般都需要重新给`constructor`赋值，以保证实例对象的类型不被改写。

### `Object.prototype.toString()`

`toString()` 方法返回一个表示该对象的字符串。
适用于所有类型的判断检测，注意区分大小写. `toString()`,在`Object`原型上返回数据格式,

`toString()`是`Object`原型对象上的一个方法，该方法默认返回其调用者的具体类型，严格的讲，是`toString()`运行时`this`指向的对象类型, 返回的类型格式为`[object, xxx]`,`xxx`是具体的数据类型，其中包括：`String`, `Number`, `Boolean`, `Undefined`, `Null`, `Function`, `Date`, `Array`, `RegExp`,`Error`, `HTMLDocument`..., 基本上所有对象的类型都可以通过这个方法获取到。

```javascript
  Object.prototype.toString.call(`Hello World`); // `[object String]`
  Object.prototype.toString.call(123); // `[object Number]`
  Object.prototype.toString.call(true); // `[object Boolean]`
  Object.prototype.toString.call(undefined); // `[object Undefined]`
  Object.prototype.toString.call(null); // `[object Null]`
  Object.prototype.toString.call(new Function()); // `[object Function]`
  Object.prototype.toString.call(new Date()); // `[object Date]`
  Object.prototype.toString.call([]); // `[object Array]`
  Object.prototype.toString.call(new RegExp()); // `[object RegExp]`
  Object.prototype.toString.call(new Error()); // `[object Error]`
  Object.prototype.toString.call(document); // `[object HTMLDocument]`
  Object.prototype.toString.call(window); // `[object Window]`

  // 注意的是，Object.prototype.toString.call 方法返回的字符串格式为 "[object 类型]"

  // 封装
  function typeOf(data) {
    return Object.prototype.toString.call(data).slice(8, -1);
  }

  // 测试
  console.log(typeOf(1)); // Number
  console.log(typeOf("1")); // String
  console.log(typeOf(true)); // Boolean
  console.log(typeOf(null)); // Null
  console.log(typeOf(undefined)); // Undefined
  console.log(typeOf(Symbol(1))); // Symbol
  console.log(typeOf({})); // Object
  console.log(typeOf([])); // Array
  console.log(typeOf(function () {})); // Function
  console.log(typeOf(new Date())); // Date
  console.log(typeOf(new RegExp())); // RegExp

```


## 参考连接

> + [*JavaScript 数据类型和数据结构*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures)
> + [typeof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)
> + [instanceof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)
> + [constructor构造函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes/constructor)
> + [Object.prototype.toString()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)
> + [*JS数据类型分类和判断*](https://juejin.cn/post/6844903623231537159)
> + [*JavaScript：数据类型/基本数据类型/引用数据类型/特殊类型/ES6提供的类型*](https://blog.csdn.net/snowball_li/article/details/122047694)
