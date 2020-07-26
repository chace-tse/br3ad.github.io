---
title: JavaScript中==和===以及Object.is()方法的区别
date: 2020-07-26 15:58:07
tag:
- 前端
- 前端基础
- ES6
- JavaScript
category:
- [前端]
- [ES6]
- [JavaScript]
---

## [`==`相等运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)

> `==`相等运算符比较两个值是否相等，在比较前将两个被比较的值转换为相同类型。在转换后（等式的一边或两边都可能被转换），然后再做比较 ——（来自[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness)）

```javascript
console.log(1 == true); // true
console.log('1' == true); // true
console.log(1 == '1'); // true
console.log(-0 == +0); // true
console.log(NaN == NaN); // false
console.log('3' == 3); // true
console.log(1 == {}); // false
console.log(1 == []); // false
console.log(0 == {}); // false
console.log(0 == []); // true
console.log(0 == false); // true，布尔类型转换为number类型，false为0，true为1
console.log('0' == false); // true，将等式前的字符串'0'转换为number类型，然后将等式后的布尔类型转换为number类型，false为0，true为1，再进行比较
console.log(0 == ''); // true，空字符串转换为number类型的0，即空字符串等于false
console.log('0' == ''); // false
```

## [`===`严格比较运算](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness)

> `===`全等（严格比较运算）操作符，用于比较两个值是否相等，两个被比较的值在比较前都不进行隐式转换。如果两个被比较的值具有不同的类型，这两个值是不全等的。换句话说，在比较两个值是否相等时，同时也进行了两个值的类型比较。
> 如果两个被比较的值类型相同，值也相同，并且都不是 `number` 类型时，两个值全等。如果两个值都是 `number` 类型，当两个都不是 NaN，并且数值相同，或是两个值分别为 +0 和 -0 时，两个值被认为是全等的。——（来自[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness)）

```javascript
console.log(+0 === -0); // true
console.log([] === []); // false
console.log({} === {}); // false
console.log(NaN === NaN); // false
console.log('11' === '11'); // true
console.log(null === null); // true
console.log(undefined === null); //false
console.log(1 === '1'); // false
console.log(1 === 1); // true
console.log(1 === true); // false
```

**缺点：**

使用`===`全等（严格比较）运算符来比较两个值不能有效地处理`NaN`(非数字的`number`类型)和`NaN`(非数字的`number`类型)以及处理负零`-0`，这个时候就需要用到`Object.is()`方法来进行比较


## [`Object.is()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

> `Object.is()`方法判断两个值是否为同一个值 ——（来自[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is)）

如果满足以下条件则两个值相等：

- 都是`undefined`
- 都是`null`
- 都是`true`或`false`
- 都是相同长度的字符串且相同字符相同顺序排列
- 都是相同对象（意味着每个对象有同一个引用）
- 都是数字且
  - 都是`+0`
  - 都是`-0`
  - 都是`NaN`
  - 或都是非零而且非`NaN`且为同一个值

```javascript
console.log(Object.is(NaN, NaN)); // true
console.log(Object.is({}, {})); // false
console.log(Object.is([], [])); // false
console.log(Object.is(+0, -0)); // false
console.log(Object.is('1', 1)); // false
console.log(Object.is('1', '1'); // true
console.log(Object.is(1, true)); // false
```

## `==`相等运算符、`===`全等（严格比较）运算符、`Object.is()`的区别

1、`==`相等运算符，两边值类型不同的时候，会先进行值的类型隐式转换，再比较；
2、`===`全等，严格比较运算符，不做类型转换，类型不同就是`false`，对于`NaN`、正零`+0`与负零`-0`的比较时不能有效地判断
3、`Object.is()`是ES6新增的用来比较两个值是否为同一个值，与`===`严格比较运算符基本相似，不同的地方在于对于`NaN`、正零`+0`与负零`-0`的比较时也能有效地处理

## 参考链接

- [*MDN-JavaScript中的相等性判断*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness)
- [*MDN-`Object.is()`*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/is)
