---
title: JavaScript IIFE(Immediately Invoked Funtion Expression)立即执行函数表达式
date: 2020-01-12 22:32:22
tags:
  - 前端
  - JavaScript
  - Function
  - IIFE
  - 立即执行函数
  - JavaScript 函数作用域
category:
- [前端]
- [JavaScript]
---

## IIFE (Immediately-Invoked Function Expression) 立即执行函数表达式

**请看下面的例子：**

```javascript
var a = 2;
(function foo(c) {
  var a = 3;
  console.log(c); // 1
  console.log(a); // 3
})(b = 1)
console.log(a); // 2
```

```javascript
(function () {/* Code */}()); 
// 或者
(function () {/* Code */})();
```

函数被包含在一对`()`内部，成为了一个表达式，再通过在末尾加上另一个`()`可以立即执行这个函数，比如：`(function foo(){ .. })()`。第一个`()`将函数变成表达式，第二个`()`执行了这个函数。

这种函数表达式被社区成为：[**IIFE(Immediately Invoked Function Expresstion)，立即执行函数表达式**](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

**IIFE**的函数名不是必须的，**IIFE**最常见的用法是使用一个匿名函数表达式**。

```javascript
var a = 2;
(function IIFE() {
  // IIFE
  var a = 3;
  console.log(a); // 3
})();
console.log(a); // 2
```

**IIFE**也可以用箭头函数：

```javascript
var a = 2;
(() => {
  /* Code */
  let a = 3;
  console.log(a); // 3
})();
console.log(a); // 2
```

另一个改进的形式：`(function(){ /* Code */ }())`

仔细观察下面两个的区别：
```javascript
// IIFE 写法一
var a = 2;
(function IIFE(){
  var a = 3;
  console.log(a); // 3
})();
console.log(a); // 2

// IIFE写法二
var a = 2;
(function IIFE(){
  var a = 3;
  console.log(a); // 3
}());
console.log(a); // 2
```
第一种形式中的函数表达式被包含在`()`中，然后在后面用另一个`()`括号来调用。
第二种形式中用来调用的`()`括号被移进了用来包装的`()`的括号中。
这两种形式在功能上是一致的

IIFE的另一种用法：**把它们当作函数调用并传递参数进去**

**例如：**

```javascript
var a = 2;
(function IIFE(global){
  var a = 3;
  console.log(a); // 3
  console.log(global.a); // 2
})(window);
console.log(a); // 2
```

解决`undefined`标识符的默认值被错误覆盖导致的异常（并不常见）。
将一个参数名为`undefined`，但是在对应的位置不传入任何值，这样就可以保证在代码中`undefined`标识符的值真的是`undefined`

**请看下面的例子：**

```javascript
undefined = true;
(function IIFE(){
  var a; // undefined
  if(a === undefined) {
    console.log('Undefined is safe here!'); // Undefined is safe here!
  }
})();
```
**IIFE**还有一种变化的用途是倒置代码的运行顺序，将需要运行的函数放在第二位，当作`IIFE`执行之后的参数传递进去

**请看下面的代码：**

```javascript
var a = 2;
(function (def){
  def(window);
})(function def(gobal){
  var a = 3;
  console.log(a); // 3
  console.log(global.a); // 2 
});
```
这里将函数表达式`def`定义在片段的第二部分，然后当作参数（这个参数也叫做`def`）被传递进`IIFE`函数定义的第一部分中，参数`def`（也就是传递进去的函数）被调用，并将`window`传入当作`global`参数的值。

除了用`()`还有很多方法可以达到同样的目的

```javascript
// IIFE
var i = function () { return 10; }();

true && function () { /* code */}();

0, function () { /* code */ }();

// IIFE
~ (function (){ /* Code*/ })();
// IIFE
;(function (){ /* Code*/})();
// IIFE
+ (function (){ /* CodeE*/ })();
// IIFEE
! (function (){ /* Code */ })();
// IIFEE
- (function (){ /* Code */ })();
void function () { /* Code */}();
// new 关键字也能达到这个效果
new function () { /* Code */ };
new function () { /* Code */ }();
```

**为什么要使用`IIFE`，它解决了什么问题？**

> 不必为函数命名，避免了污染全局变量；(封装一些外部无法读取的私有变量)
> `IIFE` 内部形成了一个单独的作用域；(隔离作用域，在`ES6`之前`JavaScript`只有函数作用域，没有块级作用域)
> 可以利用`IIFE`写`function`惰性载入

```javascript
// 写法一
var tmp = newData;
processData(tmp);
storeData(tmp);

// 写法二
(function (){
  var tmp = newData;
  processData(tmp);
  storeData(tmp);
}());
```

上面代码中，写法二比写法一更好，因为完全避免了污染全局变量。

**请看下面的例子：**

```javascript
// 使用IIFE 获取时间，以年/月/日 时: 分: 秒的格式来赋给某个变量
var currTime = (function (){
  var time = new Date();
  var year = time.getFullYear();
  var month = time.getMonth();
  var date = time.getDate();
  var hour = time.getHours();
  var minute = time.getMinutes();
  var sec = time.getSeconds();
  return year + '/' + month + '/' + date + ' ' + hour + ':' + minute + ':' + sec;
})();
console.log(currTime);
```

## 参考链接

> [Medium What is an IIFE in JavaScript?](https://medium.com/javascript-in-plain-english/https-medium-com-javascript-in-plain-english-stop-feeling-iffy-about-using-an-iife-7b0292aba174)
> [JavaScript Immediately-invoked Function Expressions (IIFE)](https://flaviocopes.com/javascript-iife/)
> [Mozilla Developer Network - IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)
> [阮一峰-《JavaScript 标准参考教程（alpha）》](https://javascript.ruanyifeng.com/grammar/function.html#toc23)
> [合理使用IIFE优化JS引擎的性能](https://zhuanlan.zhihu.com/p/23629542)
