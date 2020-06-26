---
title: JavaScript实现斐波那契数列的几种方式
date: 2020-06-26 13:47:58
tags:
- 前端
- 前端基础
- ES6
- JavaScript 算法
- JavaScript 基础
category:
- [前端]
- [前端算法]
- [JavaScript]
---

## 什么是斐波那契？

### 斐波那契数列

> 斐波那契数列（Fibonacci sequence），又称黄金分割数列、因数学家列昂纳多·斐波那契（Leonardoda Fibonacci）以兔子繁殖为例子而引入，故又称为“兔子数列”，指的是这样一个数列：1、1、2、3、5、8、13、21、34、……在数学上，斐波那契数列以如下被以递推的方法定义：`F(1)=1，F(2)=1, F(n)=F(n-1)+F(n-2)（n≥3，n ∈ N*）`(来自——[百度百科](https://baike.baidu.com/item/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97/99145?fr=aladdin))
>
> 在数学上，斐波那契数列是以递归的方式来定义,斐波那契數列由0和1開始，之後的斐波那契數就是由之前的兩數相加而得出。首幾個斐波那契數是：`0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233……`（来自——[WikiPedia维基百科](https://zh.wikipedia.org/wiki/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97)）

```javascript
// 数学计算等式如下
F0 = 0;
F1 = 1;
Fn = (Fn-1) + (Fn-2) // (n>= 2)
```

**类似于以下的数列：**
> 1, 1, 2, 3, 5, 8, 13, ....

伪代码表示，第n个数由数列的前两个相加而来：`f(n) = f(n - 1) + f(n -2)`

## 斐波那契数列的实现

### 递归实现

```javascript
// 递归实现
let fibonacciNum = (n) {
  if (n < = 2) {
    return 1;
  }
  return fibonacciNum(n-1) + fibonacciNum(n-2);
};
// 递归层数越来越深容易递归爆栈=
```
- 优点：代码量少，容易理解
- 缺点：当n较大时很快产生栈溢出，引发原因是“调用帧”过多

### 空间换时间的处理方式

**利用闭包实现缓存**
```javascript
// 闭包 + 缓存数组
const fibonacci2 = (function() {
  const f = [0];
  return function(n) {
    if(f[n] !== undefined) return f[n];
    return f[n] = ( n === 1 || n === 2 ? 1 : fibonacci2(n-1) + fibonacci2(n-2))
  }
})()
```
- 优点：
- 缺点：会增加额外的消耗，比如直接计算 `fibonacci(1000)` ,这个时候数组中会先初始化中间的其他数组项为 `undefined` 这里会小一些时间，但是计算完毕之后`1-1000`之间的斐波那契数列都填充完毕了。

**用对象替换数组来进行缓存**

```javascript
// 闭包 + 缓存对象
// 减少了填充 undefined 的时间
const fibonacci = (function (){
  const f = {};
  return function (n) {
    if ( n === 0 || n === 1) {
      return n;
    }
    if (f[n-2] === undefined) {
      f[n-2] = fibonacci(n-2);
    }
    if (f[n-1] === undefined) {
      f[n-1] = fibonacci(n-1);
    }
    return f[n] = f[n-1] + f[n-2];
  }
})()
```

**函数属性实现**
> 将缓存作为函数的属性，减少闭包的使用；缓存逻辑和业务逻辑不混合使用，添加函数属性的方式会让程序的理解变为复杂。

```javascript
const fibonacci = (n) => {
  // 创建缓存
  if (!fibonacci.f) {fibonacci.f = {}};
  // 计算
  if (n === 0 || n === 1) {
    return n;
  }
  if (fibonacci.f[n-2] === undefined) {
    fibnoacci.f[n-2] = fibonacci(n-2);
  }
  if (fibonacci.f[n-1] === undefined) {
    fibnoacci.f[n-1] = fibonacci(n-1);
  }
  return fibonacci.f[n] = fibonacci.f[n-1] + fibonacci.f[n-2];
}
```
总结：使用空间换时间的好处能够复用之前的计算结果，提升性能，减少计算代价；但是这种方式难以做负载测试和算法复杂度评估，因为输出结果依赖之前的输入。

### 尾递归优化

> 尾调用（Tail Call）是函数式编程的一个重要概念，本身非常简单，就是指某个函数的最后一步是调用另一个函数。

当计算的数值较大时会出现递归爆栈的现象，有一种解决办法就是尾递归。但这种方法需改写函数的参数，将结算结果作为参数传递下去，在实际使用的使用的时候没什么问题修改接口就行。尾递归优化可参考：[ruanyifeng-尾调用优化](https://ruanyifeng.com/blog/2015/04/tail-call.html)

```javascript
function fibonacci(n, n1, n2) {
  if (n <= 1) {
    return n2;
  }
  return fibonacci(n-1, n2, n1 + n2);
}
```

### 递推

递归算法中我们获取某一项的值时是从后一步步往前推，现在我们换成从前往后推，即递推。既然三项中的前两项相加等于第三项，写成表达式就是`res[i-2] + res[i-1] = res[i]`

**for循环**

```javascript
let fib = function(n) {
  if(n <= 2) {
    return 1
  }
  let sum = 0
  let prev = 1
  let next = 1
  for(let i = 3; i <= n; i++) {
    sum = prev + next;
    prev = next;
    next = sum;
  }
  return sum;
}
```

**while循环**
```javascript
let fib = function(n) {
  let i = 2
  let res = [0,1,1]
  while(i <= n) {
      res[i] = res[i - 1] + res[i - 2]
      i++
  }
  return res[n]
}
```

### 其他方法收集

**采用解构赋值**
```javascript
const fibonacci = (n) => {
  let a = 0;
  let b = 1;
  let i = 1;
  while (i++ <=n) {
    [a, b] = [b, a+b]
  }
  return a;
}
```

**闭包实现**
```javascript
const fibonacci=((s) => (f=(i) => s[i] || (s[i]=f(i-1)+f(i-2))))([0,1,1])
```

**ES6 `reduce()`实现**
```javascript
const fibonacci = n => [...Array(n)].reduce(
  (acc, val, i) => acc.concat(
    i > 1 ? acc[i - 1] + acc[i - 2] : i
  ), []
)
```

## 参考链接

> [记忆化斐波那契函数的思考（JavaScript）](https://juejin.im/post/5df1b02d51882512561b6c63)
> [斐波那契数列的js实现](https://juejin.im/post/5eec2840f265da02b80e0373)
> [Fibonacci series in JavaScript](https://stackoverflow.com/questions/51111870/fibonacci-series-in-javascript/51111896)
> [ruanyifeng-尾调用优化](https://ruanyifeng.com/blog/2015/04/tail-call.html)
> [leetcode-斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/solution/xun-huan-fa-bei-wang-lu-javascriptda-shu-shi-xian-/)
