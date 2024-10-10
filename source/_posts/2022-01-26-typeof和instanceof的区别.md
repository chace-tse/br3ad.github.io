---
title: typeof和instanceof的区别
date: 2022-01-26 22:11:54
tags:
- 前端
- 前端基础
- 数据类型检测
category:
- [前端]
- [JavaScript]
---

## `typeof`

**`typeof`操作符返回一个字符串，表示未经计算的操作数的类型**

```javascript
typeof operand
typeof (operand)
```

`operand` 表示对象或原始值的表达式，其类型将被返回

```javascript
typeof 1 // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
typeof null // 'object'
typeof [] // 'object'
typeof {} // 'object'
typeof console // 'object'
typeof console.log // 'function'
```

`typeof` 可能的返回值。有关类型和原始值

```javascript

Undefined // 'undefined'
Null // 'object'
Boolean // 'boolean'
Number // 'number'
Bigint // 'bigint'
String // 'string'
Symbol // 'symbol'
宿主对象 // 取决于具体实现
Funtion 对象 // 'function'
其他任何对象 // 'object'

```

示例

```javascript
// 数值
typeof 37 === 'number' // true
typeof 3.14 === 'number' // true
typeof (42) === 'number' // true
typeof Math.LN2 === 'number' // true
typeof infinity === 'number' // true
typeof NaN === 'number' // true
typeof Number(1) === 'number'

```

## `instanceof`

## 参考链接

- [*typeof与instanceof的区别*](https://github.com/febobo/web-interview/issues/65)
- [*developer.mozilla.org：typeof*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)
- [*developer.mozilla.org：instanceof*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)
- [*typeof 和 instanceOf的区别*](https://segmentfault.com/a/1190000000730982)
