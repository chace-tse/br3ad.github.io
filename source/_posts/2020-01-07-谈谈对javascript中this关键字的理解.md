---
title: 谈谈对JavaScript中this、call()、apply()、bind()的理解
date: 2020-01-07 12:12:11
tags:
  - 前端
  - 前端面试题
  - JavaScript this
  - JavaScript 作用域问题
category:
- [前端]
- [JavaScript]
---

## MDN

> *[`JavaScript this`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)*
> *[`JavaScript Function.prototype.call()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)*
> *[`JavaScript Function.prototype.apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)*
> *[`JavaScript Function.prototype.bind()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)*


## [*`this`的概念*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)理解

> ***[`this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this) 永远指向一个对象，并且指向最后调用它的那个对象；***
> ***[`this`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this) 的指向完全取决于函数调用的位置；***


## [*`this`*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)的指向

> *在绝大多数情况下，函数的调用方式决定了`this`的值。`this`不能在执行期间被赋值，并且在每次函数被调用时this的值也可能会不同。ES5引入了bind方法来设置函数的this值，而不用考虑函数如何被调用的，ES2015 引入了支持this词法解析的箭头函数（它在闭合的执行环境内设置this的值）。[(来自MDN)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)*

<!-- > **`this` 永远指向最后调用它的那个对象**
> **`this` 永远指向一个对象；**
> **`this` 的指向完全取决于函数调用的位置；**
> **`this` 会根据运行环境的改变而改变，同时，函数中的`this`也只能在运行时才能最终确定运行环境；**
> **如果返回值是一个对象，那么`this`指向的就是那个返回的对象，如果返回值不是一个对象那么`this`还是指向函数的实例。** -->
### 全局环境(Global context)

> *无论是否在严格模式下，在全局执行环境中（在任何函数体外部）`this` 都指向全局对象 [(来自MDN)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)*

```javascript
conosole.log(this === window); // true
a = 37;
console.log(window.a); // 37
this.b = 'Br3ad';
console.log(window.b); // Br3ad
console.log(b); // Br3ad
```

### 函数（运行内）环境(Function context)

> *在函数内部，`this`的值取决于函数被调用的方式。[(来自MDN)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)*

#### 简单调用

**非严格模式下：**
因为下面的代码不在严格模式下，且 `this` 的值不是由该调用设置的，所以 `this` 的值默认指向全局对象(`window`)。

```javascript
// non-strict mode
function func1 () {
  return this;
};
// 在浏览器中：
func1() === window; // true
// 在node中：
func1() === global; // true
```

**严格模式下：**
`this`将保持他进入执行环境时的值，所以下面的`this`将会默认为`undefined`。

```javascript
// strict mode
function func2 () {
  'use strict';
  return this;
};
func2 === undefined; // true
```

所以，可以得出结论在严格模式下，如果 `this` 没有被执行环境（execution context）定义，那它将保持为 `undefined`。

**首先，来看下面一个简单的例子：**

**例 1：**

```javascript
var name = 'windowsName';
function foo () {
  var name = 'Br3ad';
  console.log(this.name); // windowsName
  console.log('inner: ' + this); // [Object Window]
}
foo();
console.log('outer: ' + this); // [Object Window]
```

为什么这里`console.log`是 windowsName？

因为**“`this`永远指向最后调用它的那个对象”**，调用`foo`的地方`foo()`，前面没有调用的对象那么就是指向全局对象 `Object window`，相当于`window.foo()`

这里没有使用严格模式，如果使用严格模式的情况下，全局对象就是`undefined`，那么就会报错`Uncaught TypeError: Cannot read property 'name' of undefined`

**请看下面的例子：**

**例 2：**

```javascript
// Use Strict Mode
'use strict'
var name = 'windowsName';
function foo () {
  var name = 'Br3ad';
  console.log('inner: ' + this); // inner: undefined
  console.log(this.name); // Uncaught TypeError: Cannot read property 'name' of undefined
}
foo();
console.log('outer: ' + this); // [Object Window]
```

**再看下面的例子：**

**例 3：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  fn: function () {
    console.log(this.name); // Br3ad
  };
};
bar.fn(); // Br3ad
```

在这个例子中，函数 `fn` 是对象 `bar` 调用的，所以打印的值就是 `bar` 中的 `name` 的值。

**基于上面的例子，再做个改动：**

**例 4：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  fn: function () {
    console.log(this.name); // Br3ad
  }
};
window.bar.fn(); // Br3ad
```

这里`console.log`为`Br3ad`，最后调用它的对象是`bar`,还是因为**“`this` 永远指向最后调用它的那个对象”**

**再来看下面这个例子：**

**例 5：**

```javascript
var name = 'windowName';
var bar = {
  // name: 'Br3ad',
  fn: function () {
    console.log(this.name); // undefined
  }
};
window.bar.fn(); // undefined
```

为什么`console.log`会打印`undefined`呢？

因为，如刚刚所描述的那样，调用`fn`的是`bar`这个对象，也就是说`fn`内部的`this`是对象`bar`，而对象`bar`中并没有对`name`字段进行定义，所以`console.log`的`this.name`的值为`undefined`。

这个例子还是印证了刚才的结论：**this 永远指向最后调用它的那个对象**，因为最后调用`fn`的对象是`bar`，所以就算`bar`中没有`name`这个属性，也不会继续向上一个对象寻找`this.name`，而是直接输出`undefined`。

**再来看一个复杂点的例子：**

**例 6：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  fn: function () {
    console.log(this.name); // windowsName
  }
};
var fun = bar.fn;
fun(); // windowsName
```

为什么这里`console.log`打印出的不是`Br3ad`？因为虽然`bar`对象的`fn`方法赋值给了变量`fun`了，但是没有调用，回到之前我们的结论：**“this 永远指向最后调用它的那个对象”**，由于刚刚的`fun`并没有调用，所以`fn()`最后仍然是被`window`调用的。所以这里`this`指向的也就是`window`。

以上的例子，不难发现`this`的指向并不是在创建的时候就可以确定的，在 `es5` 中，永远是：**`this` 永远指向最后调用它的那个对象**

**再来看一个例子：**

**例 7：**

```javascript
var name = 'windowName';
function fn () {
  var name = 'Br3ad';
  innerFunction();
  function innerFunction() {
    console.log(this.name); // windowsName
  }
};
fn(); // windowsName
```

## 怎么改变 `this` 的指向?

改变this的指向主要有以下几种方法：

- 使用`ES6`的[`箭头函数(Arrow function expressions)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- 在函数内部使用`_this = this`
- 使用`apply()`、`call()`、`bind()`
- `new` 实例化一个对象

**请看下面的例子：**

**例子8：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name);  // this.func1 is not a function
  },
  func2: function () {
    setTimeout(function () {
      this.func1();
    }, 100);
  }
};
bar.func2(); // this.func1 is not a function
```

在不使用箭头函数的情况下，是会报错的，因为最后调用`setTimeout`的对象是`window`，但是在`window`中并没有`func1`函数。

在改变 `this` 指向这一节将把这个例子作为 `Demo` 进行改造

那么，箭头函数是如何实现的？


### 箭头函数（Arrow function expressions）
---

**箭头函数的 `this` 始终指向函数定义时的 `this`，而非执行时。**记住：“箭头函数没有单独的`this`绑定，必须通过查找作用域链来决定其值，如果箭头函数被非箭头函数包含，则 `this` 绑定的是最近一层非箭头函数的 `this`，否则，`this` 为 `undefined`(箭头函数会从自己的作用域链的上一层继承`this`)”。

**请看下面的例子：**

**例9：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name); // Br3ad
  },
  func2: function () {
    setTimeout(() => {
      this.func1(); // 箭头函数没有单独的this绑定，必须通过查找作用域链来决定其值
    }, 100);
  }
};
bar.func2(); // Br3ad
```

### 在函数内部使用`_that = this`
---

如果不使用ES6，那么这种方式应该是最简单的不会出错的方式，先将调用这个函数的对象保存在变量`_this`中，然后在函数中都是用这个`_that`，这样`_that`就不会改变了。

**请看下面的例子：**

**例10：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name); // Br3ad
  },
  func2: function () {
    var _that = this; // 这里把对象bar的作用域保存起来给一个变量_that
    setTimeout( function () {
      _that.func1();
    }, 100);
  };
};
bar.func2(); // Br3ad
```

这个例子中，在`func2`中，首先设置`var _that = this;`，这里的`this`是调用func2的对象`bar`，为了防止在`func2`中的`setTimeout`被`window`调用而导致的在`setTimeout`中的`this`为`window`。将`this(指向变量bar)`赋值给一个变量`_that`，这样，在`func2`中使用`_that`就是指向对象`bar`了。


### 使用 `apply()`、`call()`、`bind()`

使用[`apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)、[`call()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)、[`bind()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)函数也是可以改变`this`的指向，先来看一下是怎么实现的：

#### 使用[*`apply()`*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

来看看MDN对[`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)的用法定义：

> [`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)方法调用一个具有给定`this`值的函数，以及作为一个数组（或类似数组对象）提供的参数

**语法**

```javascript
function.apply(thisArg, [argsArray])
```

**请看下面的例子：**

**例11：**

```javascript
// function.apply()
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name); // Br3ad
  },
  func2: function () {
    setTimeout(function () {
      this.func1(); // Br3ad
    }.apply(bar), 100);
  }
};
bar.func2(); // Br3ad
```

#### 使用[*`call()`*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

来看看MDN对[`call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)的用法定义：

> [`call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数。

**语法**

```javascript
function.call(thisArg, arg1, arg2, arg3, ar4, ...);
```

**请看下面的例子：**

**例子12：**

```javascript
// function.call()
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name); // Br3ad
  },
  func2: function () {
    setTimeout( function (){
      this.func1();
    }.call(bar), 100)
  }
};
bar.func2(); // Br3ad
```

#### 使用[*`bind()`*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

来看看MDN对[`bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)的用法定义：

> [`bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用

**语法**

```javascript
function.bind(thisArg[, arg1[, arg2[, ...]]])
```

**请看下面的例子：**

**例子13**

```javascript
// function.bind()
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name); // Br3ad
  },
  func2: function () {
    setTimeout(function () {
      this.func1();
    }.bind(bar)(), 100);
  }
};
bar.func2(); // Br3ad
```

## JavaScript 中 [`call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)、[`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)、[`bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)的区别？

现在，我们都知道使用`call()`、`apply()`、`bind()`函数都可以改变JavaScript中`this`的指向，但是这三个函数稍有不同。

在[`MDN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)中定义`apply()`如下：

> `apply()` 方法调用一个具有给定`this`值的函数，以及作为一个数组（或类似数组对象）提供的参数

**语法**

```javascript
function.apply(thisArg, [argsArray])
```

**参数：**
> `thisArg`(必须) 在 `func` 函数运行时使用的 `this` 值。请注意，`this`可能不是该方法看到的实际值：如果这个函数处于非严格模式下，则指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。

> `argsArray`(可选) 一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 `func` 函数。如果该参数的值为 `null` 或  `undefined`，则表示不需要传入任何参数。从`ECMAScript 5`开始可以使用类数组对象。

### `apply()` 和 `call()` 的区别

`apply()` 和 `call()` 基本类似，他们的区别只是传入的参数不同

call()的语法为：

```javascript
function.call(thisArg, arg1, arg2, ...)
```

`apply()`和`call()`的区别就是：
> **`call()`方法接受的是若干个参数列表，而`apply()`接收的是一个包含多个参数的数组。**

**请看下面的例子：**

**例子14：**

```javascript
// function.apply()
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  fn: function (a, b) {
    console.log(a + b); // 3
  }
};
var b = bar.fn;
b.apply(bar, [1, 2]); // 3
```

**例子15：**

```javascript
// function.call()
var bar = {
  name: 'Br3ad',
  fn: function (a, b) {
    console.log(a + b); // 3
  }
};
var b = bar.fn;
b.call(bar, 1, 2); // 3
```

### [`bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)和[`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)、[`call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)的区别

现在，将刚刚的例子使用[`bind()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)试一下

```javascript
// function.bind()()
var bar = {
  name: 'Br3ad',
  fn: function (a, b) {
    console.log(a + b);
  }
};
var b = bar.fn;
b.bind(bar, 1, 2); // 到这一步并没有输出，这是因为bind()方法创建了一个新函数，需要进一步调用才能执行
```

会发现并没有输出，这是为什么呢，我们来看一下 [`MDN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) 上的文档说明：

> `bind()` 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 `this` 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

所以我们可以看出，`bind()` 是创建一个新的函数，我们必须要手动去调用：

```javascript
// function
var bar = {
  name: 'Br3ad',
  fn: function (a, b) {
    console.log(a + b); // 3
  }
};
var b = bar.fn; // 到这一步并没有输出，这是因为bind()方法创建了一个新函数，需要进一步调用才能执行
b.bind(bar, 1, 2)(); // 调用bind()方法创建的新函数，并正确输出了结果：3
```

---

## JavaScript 中的函数调用方式

**例7：**

```javascript
var name = 'windowsName';
function fn () {
  var name = 'Br3ad';
  innerFunction();
  function innerFunction () {
    console.log(this.name); // windowsName
  }
};

fn();
```

**例8：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name);
  },
  func2: function () {
    setTimeout(function(){
      this.func1();
    }, 100)
  }
};
bar.func2(); // Uncaught TypeError: this.func1 is not a function
// 这里调用setTimeout的是全局对象，this指向的也是全局对象，而全局对象中并没有`func1()`这个函数，所以这里会报错
```

**函数调用的方法一共有 4 种**
> **作为一个函数调用**
> **函数作为方法调用**
> **使用构造函数调用函数**
> **作为函数方法调用函数（[`call()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)、[`apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)）**

### 作为函数调用

**比如上面的例子1：**

**例1：**
```javascript
// non-strict mode
var name = 'windowsName';
function foo () {
  var name = 'Br3ad';
  console.log(this.name); // windowsName
  console.log('inner:' + this); // inner: [object Window]
};
foo();
console.log('outer:' + this); // outer: [object Window]
```

这是一个简单的函数，在浏览器运行环境中的非严格模式(non-strict mode)默认是属于全局对象 `window` 的，在严格模式(strict mode)，this指向的就是 `undefined`。**这是一个全局的函数，很容易产生命名冲突，不建议这样使用。**

```javascript
// strict mode
'use strict';
var name = 'windowsName';
function foo () {
  var name = 'Br3ad';
  console.log(this.name);
};
foo(); // Uncaught TypeError: Cannot read property 'name' of undefined
// 这里使用的是严格模式，this指向的全局对象，而全局对象没有被定义所以是undefined，所以这里会报错
```

### 函数作为方法调用

将函数作为对象的方法使用。比如：

**例2：**

```javascript
var name = 'windowName';
var foo = {
  name: 'Br3ad',
  fn: function () {
    console.log(this.name); // Br3ad
  }
};
foo.fn(); // Br3ad
```

这里定义一个对象`foo`，对象`foo`有一个属性(`name`)和一个方法(`fn`)。

然后，对象`foo`通过`.`方法调用了其中的`fn`方法

还记得那句话**“this永远指向最后调用它的那个对象”**，所以在`fn`中的`this`就是指向 `foo` 的

### 作为构造函数调用函数

> 构造函数：关键字new建一个对象并调用一个函数（这个函数称作构造函数 Constructor）初始化新对象的属性
> 如果函数调用前使用了new运算符，则是调用了构造函数
> 这看起来就像创建了新的函数，但实际上JavaScript函数是重新创建的对象

```javascript
// 构造函数
function myFunction(arg1, arg2) {
  this.firstName = arg1;
  this.lastName = arg2;
}
var foo = new myFunction('Li', 'Cherry');
foo.lastName; // 'Cherry'
```

new 的过程

```javascript
var foo = new myFunction('Li', 'Cherry');
new myFunction {
  var obj = {};
  obj.__proto__ = myFunction.prototype;
  var result = myFunction.call(obj, 'Li', 'Cherry');
  return typeof result === 'object' ? result : obj;
}
```

1、创建一个空对象obj；
2、将新创建的空对象的隐式原型指向其构造函数的显示原型
3、使用`call`改变`this`的指向
4、如果无返回值或者返回一个非对象值，则将 obj 返回作为新对象；
如果返回值是一个新对象的话那么直接直接返回该对象。

可以看到，在new的过程中，使用`call`改变了this的指向

### 通过它们的`call()`和`apply()`方法间接调用

> JavaScript 中，函数是对象
> JavaScript 函数有它的属性和方法。
> `call()`和`apply()`是预定义的函数方法。两个方法可用于调用函数，两个方法的第一个参数必须是对象本身
> JavaScript 严格模式（strict mode）下，在调用函数时第一个参数会成为`this`的值，即使该参数不是一个对象
> JavaScript 非严格模式（non-strict mode）下，如果第一个参数的值是`null`或`undefined`，它将使用全局对象替代。

**再来看例子6:**

```javascript
var name = 'windowsName';
function fn () {
  var name = 'Br3ad';
  innerFunction();
  function innerFunction() {
    console.log(this.name); // windowsName
  };
};
fn();
```

这里的`innerFunction()`的调用属于第一种调用方式：作为一个函数调用（作为一个函数调用、没有挂载在任何对象上，所以对于没有挂载在任何对象的函数，在非严格模式（non-strict mode）下就是指向window的）

**然后再看一下例7:**

**例7：**

```javascript
var name = 'windowsName';
var bar = {
  name: 'Br3ad',
  func1: function () {
    console.log(this.name);
  },
  func2: function () {
    setTimeout(function (){
      this.func1()
    }, 100)
  }
};

bar.func2(); // this.func1 is not a function
```

得出结论，可以简单理解为：**匿名函数的`this`永远指向`window`**

在这之前，我们得出结论：**`this`永远指向最后调用它的那个对象**，那么去找最后调用匿名函数的对象，
但是因为匿名函数没有名字，所以没有办法被其他对象调用匿名函数的。所以：**匿名函数的 `this` 永远指向 `window`**

那么问题来了，匿名函数是如何被定义的？匿名函数是自执行的，就是在匿名函数后面加`()`让其自执行。其次就是虽然匿名函数不能被其他对象调用，但是可以被其他函数调用，比如**例7**中的`setTimeout`

---

## 严格模式

> 在严格版中的默认的`this`不再是`window`，而是`undefined。`

**几条判断`this`指向的方法：**

1、查看函数在哪被调用
2、点左侧有没有对象？如果有，它就是 “`this`” 的引用。如果没有，继续往下。
3、该函数是不是用 “`call`”、“`apply`” 或者 “`bind`” 调用的？如果是，它会显式地指明 “`this`” 的引用。如果没有，继续往下。
4、该函数是不是用 “`new`” 调用的？如果是，“`this`” 指向的就是 `JavaScript` 解释器新创建的对象。如果没有，继续往下。
5、是否在“严格模式”下？如果是，“`this`” 就是 `undefined`，如果不是
6、JavaScript，“`this`” 会指向 “`window`” 对象
7、匿名函数的执行环境`this`具有全局性，其`this`对象通常指向`window`（听过`call()`或`apply()`改变函数执行环境的情况下，`this`就会指向其他对象）

## 参考链接

> [稀土掘金-this、apply、call、bind](https://juejin.im/post/59bfe84351882531b730bac2)
> [阮一峰-JavaScript 的 this 原理](https://www.ruanyifeng.com/blog/2018/06/javascript-this.html)
> [javascript this指向](https://note.youdao.com/ynoteshare1/index.html?id=b2fab3b044aa90033395df0c8c9ca3a4&type=note)
> [*How to use the apply(), call(), and bind() methods in JavaScript*](https://www.freecodecamp.org/news/how-to-use-the-apply-call-and-bind-methods-in-javascript-80a8e6096a90/)
> [*Understanding This, Bind, Call, and Apply in JavaScript*](https://www.taniarascia.com/this-bind-call-apply-javascript/)
> [*Function.prototype.apply()*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
> [*Function.prototype.call()*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
> [*Function.prototype.bind()*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
> [*理解 JavaScript 中的 this、call、apply 和 bind*](https://juejin.im/post/5b9f176b6fb9a05d3827d03f)
> [*Understanding the "this" keyword, call, apply, and bind in JavaScript*](https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/)
> [*JavaScript 之 this 指南*](https://juejin.im/post/5c876ba96fb9a049ae08bc63)
> [*javascript 基础之 call, apply, bind*](https://zhuanlan.zhihu.com/p/71553017)
> [*JavaScript中的call、apply、bind深入理解*](https://www.jianshu.com/p/00dc4ad9b83f)
> [*彻底弄清 this call apply bind 以及原生实现*](https://juejin.im/post/5c813aa5f265da2dd94cd7c2)
> [*如何在 JavaScript 中使用 apply()，call()，bind()*](https://juejin.im/post/5c8617d86fb9a049e93d8e4a)
> [JavaScript 函数调用](https://www.runoob.com/js/js-function-invocation.html)
