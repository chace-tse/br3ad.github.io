---
title: JavaScript阶乘 (Factoral) 函数实现
date: 2019-12-17 17:49:03
  - 前端开发
  - 前端算法
  - 前端面试题
  - 前端算法面试题
  - JavaScript 算法
  - JavaScript 阶乘实现
category:
- [前端]
- [JavaScript]
---

## 什么是阶乘(Factoral)
> **一个正整数的阶乘是所有小于及等于该数的正整数的积，并且有0的阶乘为1。自然数n的阶乘写作n!**

阶乘函数是**递归(Recursion)**典型示例，在JavaScript中可能运用到**递归(Recursion)**函数

## 什么是**递归(Recursion)**
> 在函数内部，可以调用其他函数。如果一个函数在内部调用自身本身，这个函数就是递归函数。[*(来自wikipedia)*](https://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92)

在函数的定义中使用函数自身的方法。简单理解就是：自我复制的过程。

## 如何实现阶乘(Factoral)函数

数学上的**阶乘(Factoral)**函数定义，阶乘函数的参数是一个自然数，它返回`1`与此数之间所有数的乘积。比如，`6`的阶乘是`1 x 2 x 3 x 4 x 5 x 6 = 720`，这样的方式可以用一种递归函数来表示，如果`n`是 `6`，模式为：

```javascript
0! = 1 // 1
1! = 1 // 1
2! = 2 * 1 // 2
3! = 3 * 2 * 1 // 6
4! = 4 * 3 * 2 * 1 // 24
5! = 5 * 4 * 3 * 2 * 1 // 120
6! = 6 * 5 * 4 * 3 * 2 * 1 // 720
7! = 7 * 6 * 5 * 4 * 3 * 2 * 1 // 5040
...
```

因此，阶乘可以简单的定义为：
> + `0`的阶乘是1
> + 任何数的阶乘都是此数与比此数小一的数的阶乘

定义一个`factoral()`函数来表示：
```javascript
factoral(0) = 1;
factoral(n) = n * factoral (n - 1);
```
第一行`0`的阶乘为`1`，第二行表示任意别的数`n`的阶乘等于`n`乘以`n-1`的阶乘。
*注意那个把`n-1`括起来的括弧：没有这个括弧代码就会被解析称为`(factorial n) - 1;`函数行为的优先级是很高的，会最先执行。*

## 阶乘(Factorial)实现算法

阶乘函数在JavaScript中也是一种典型的算法：

> + `factoral()`函数返回的是一个整数的阶乘
> + 如何整数用字母`n`表示，所有正整数的阶乘是小于或等于`n`
> + 阶乘通常用的表示符号是`n!`

## 阶乘(Factoral)测试用例

+ `factoral(0)返回1`
+ `factoral(1)返回1`
+ `factoral(5)返回120`
+ `factoral(10)返回3628800`
+ `factoral(20)返回2432902008176640000`

## 几种实现阶乘(Factoral)的方法
> + [*递归(Recursion)法*](#递归(Recursion)法)
> + [*ES6数组迭代法*](#ES6数组迭代法)


### 递归(Recursion)法

```javascript
/**
  * @param: {n}
  *
*/
function factoral (n) {
  if (n < 0) {
    // 如果n是一个小于0的整数，返回false
    return false;
  } else if (n === 0 || n === 1) {
    // 如果n是一个0或者1，返回阶乘结果为1
    return 1;
  } else {
    // 调用递归
    return n * factoral (n - 1);
  }
}

factoral (0); // 1
factoral (1); // 1
factoral (5); // 120
factoral (6); // 720
factoral (10); // 3628800
factoral (20); // 2432902008176640000
```

使用函数**arguments.callee**属性解耦

```javascript
function factoral (n) {
  return !(n > 1) ? 1 : arguments.callee(n - 1) * n;
}

factoral (0); // 1
factoral (1); // 1
factoral (5); // 120
factoral (6); // 720
factoral (10); // 3628800
factoral (20); // 2432902008176640000
```

### `while loop`(while 循环)法

```javascript
function factoral (num) {
  var
}
```


### `for loop`(for 循环)法



### ES6数组迭代法

```javascript
function factoral (num) {
  return num < 0 ? 1 : ( // 如果num小于0则返回1，否则执行后面的语句
    new Array(num) // 实例了一个length为num长度的数组对象
      .fill(undefined) // 初始化填充数组的每一项为undefined
      .reduce((product, val, index) => product * (index + 1), 1) // reduce对num的每一项进行累加迭代计算，最终返回计算出的结果
  );
}
factoral(5); // 调用函数，最终结果为120
```

## 参考链接

+ [*维基百科: 阶乘(Factoral)*](https://zh.wikipedia.org/wiki/%E9%9A%8E%E4%B9%98)
+ [*维基百科: 递归(Recursion)*](https://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92)
+ [*w3cplus: JavaScript算法练习：阶乘(Factorial)*](https://www.w3cplus.com/javascript/factorial-function-in-javascript.html?expire=1576575926&code=6UzePxl_rKQ&sign=0337255c0a21b8e38123efa0cb40c62c#paywall)
+ [*FreeCodeCamp Challenge Guide: Factorialize a Number*](https://www.freecodecamp.org/forum/t/freecodecamp-challenge-guide-factorialize-a-number/16013)
+ [*MDN:JavaScript Functions arguments.callee*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments/callee)
+ [*MDN:Array.prototype.fill()*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)
+ [*MDN:Array.prototype.reduce()*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)