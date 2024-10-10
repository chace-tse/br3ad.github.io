---
title: javascript中隐式转换
date: 2019-12-17 13:59:30
tags:
- 前端开发
- JavaScript
- JavaScript 隐式转换
- JavaScript 基础知识
category:
- [前端]
- [JavaScript]
---

**请看如下代码：**

```javascript
var x = 'The answer is ' + 42;
consolo.log(x); // 'The answer is 42'

var y = 42 + 'is the answer';
console.log(y); // '42 is the answer'

var num = '37';
num = num - 0; // 37
num = num + 7; // 377

```

## 巧用+/-规则转换类型

* 如果想把一个string转换为number类型，可以通过减去0，比如：

```javascript
var str = "43434";
str = str - 0; 
console.log(str) // 43434
typeof str // 'number'
```

**如果想把一个变量转换为字符串类型，只需要把这个变量加上一个空字符，比如：**
```javascript
var num = 6353355;
num = num + '';
console.log(num); // '6353355'
typeof num; // 'string'
```

## `==` 非严格相等比较

> 类型相同：比较两边的内容和长度必须是完全一样时才会返回true，否则为false
> 类型不同：尝试(隐式)类型转换然后再做比较

```javascript
number == string // 转number 1 == ‘1.0’ true
boolean == ? // 转number 1 == true // true
object == number | string // 尝试对象转为基本类型
0 == undefined; // false
[] == []; // false
[] == {}; // false
new Object() == new Object(); // false
[1,2] == [1,2]; // false

'1.23' == 1.23; // true 会尝试把string转换为number再进行比较
null == undefined; // true 
O == false; // true
0 == []; // true
[] == ![]; // true
[] == false; // true
'' == []; // true
'' == 0; // true
'' == false; // true
Function == Function; // true
Function == function (){}; // false
new String('hi') == 'hi'; // true
```
* 如果是字符串和数字比较，会把字符串转为数字


## `===` 严格相等比较

```javascript
Array.prototype.indexOf // 返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1
Array.prototype.lastIndexOf // 返回指定元素（有效的 JavaScript 值或变量）在数组中的最后一个的索引，如果不存在则返回 -1。从数组的后面向前查找，从 fromIndex 处开始
case-matching
```

* 类型不同：先判断两边的类型，如果类型不同，直接返回false，

* 类型相同：比较两边的内容和长度必须是完全一样时才会返回true，否则为false
但是需要考虑如下情况：

```javascript
null === null; // true
undefined === undefined; // true

null === undefined; // false
[] === []; // false
[] !== []; // true
NaN !== NaN; // true
Function === Function; // true
Function === function (){}; // false
NaN === NaN; // false NaN不等于自身 
new Object() === new Object(); // false 对象是用引用去比较，而不是用值去比较
```
