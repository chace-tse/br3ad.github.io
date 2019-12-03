---
title: JavaScript Palindrome String(字符串回文)Function
date: 2019-12-01 23:07:26
tags:
  - 前端开发
  - 前端算法
  - 前端面试题
  - 前端算法面试题
  - JavaScript
  - JavaScript 算法
category:
- [JavaScript]
---

## 什么是回文？

Palindromes称之为**回文**，在中文当中简单来说是指倒着念和顺着念都是相同的，前后对称那么就属于**回文**；例如：「上海自来水来自海上」。

在英文文当中是指正着看和反着看都相同的单词，例如：「madan」。对于数字，又称为回文数，是指一个像“16461”这样的对称的数。

综上所述，我们得出回文的规则：
> + 单个和零个字符都是回文，例如：**「1」**、**「2」**、**「3」**...等等
> + 如果字符串的第一个字符和最后一个字符相同，并且除了两个字符以外剩余的其他字符也是一个回文的话，字符串是一个回文，例如：**「16461」**、**「level」**、**「noon」**、**「nonon」**...等等

**如何用JavaScript来实现回文？**

**现给出测试用例：**
> + `checkPalindrome('race car')`返回`true`
> + `checkPalindrome('not a palindrome')`返回`false`
> + `checkPalindrome('A man, a plan, a canal. Panama')`返回`true`
> + `checkPalindrome('never odd or even')`返回`true`
> + `checkPalindrome('nope')`返回`false`
> + `checkPalindrome('almostomla')`返回`false`
> + `checkPalindrome('My age is 0, 0 si ega ym.')`返回`true`
> + `checkPalindrome('1 eye for of 1 eye.')`返回`false`
> + `checkPalindrome('0_0 (: /-\ :) 0–0')`返回`true`
> + `checkPalindrome('我爱妈妈，妈妈爱我')`返回`true`

---

## 方法一 

`reverse()`实现

**实现思路：**
> + 利用正则`/[\W_]/g`(或者`/[^A-Za-z0-9]/g`)删除不必要的字符
> + 通过`toLowerCase()`将传入的字符串转换为小写字母
> + 利用`split()`方法将`string`对象分割成字符串数组，然后用`reverse()`方法将数组中的元素进行倒序，并返回该数组（会改变原来的数组），最后`join()`方法将这个数组的所有元素连接成一个字符串
> + 将返回的这个字符串再与原字符串进行比较是否完全相等

**具体代码如下：**

```javascript
  function checkPalindrome (str) {
    var removeChar = str.replace(/[\W_]/g, '').toLowerCase();
    var checkPalindrome = removeChar.split('').reverse().join('');
    return removeChar === checkPalindrome;
  };

  checkPalindrome('race car'); // true
  checkPalindrome('not a palindrome'); // false
  checkPalindrome('A man, a plan, a canal. Panama'); // true
  checkPalindrome('never odd or even'); // true
  checkPalindrome('nope'); // false
  checkPalindrome('almostomla'); // false
  checkPalindrome('My age is 0, 0 si ega ym.') // true
  checkPalindrome('1 eye for of 1 eye.'); // false
  checkPalindrome('0_0 (: /-\ :) 0–0'); // true
  checkPalindrome('我爱妈妈，妈妈爱我'); // true
  checkPalindrome('16461'); // true
  checkPalindrome('javascript'); // false
  checkPalindrome('Hello world'); // false
```

## 方法二

使用`for`循环来处理

```javascript


```



## 递归实现

```javascript
 function checkPalindrome(text) {
  if (text.length <= 1) return true;
  if (text.charAt(0) != text.charAt(text.length - 1)) return false;
  return checkPalindrome(text.substr(1, text.length - 2));
 }

 checkPalindrome('level'); // true
 checkPalindrome('l'); // true
 checkPalindrome(null); // error
 checkPalindrome(undefined); // erro
// 需要注意的是这种方法，没有考虑，null和undefined的情况
```
