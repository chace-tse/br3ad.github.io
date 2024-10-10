---
title: JavaScript Palindrome String(字符串回文)Function
date: 2019-12-01 23:07:26
tags:
  - 前端开发
  - 前端算法
  - 前端面试题
  - 前端算法面试题
  - JavaScript 字符串回文
  - JavaScript 算法
category:
- [前端]
- [JavaScript]
---

## 什么是回文？

Palindromes称之为**回文**，在中文当中简单来说是指倒着念和顺着念都是相同的，前后对称那么就属于**回文**；例如：「**上海自来水来自海上**」。

在英文文当中是指正着看和反着看都相同的单词，例如：「**madam**」。对于数字，又称为回文数，是指一个像“**16461**”这样的对称的数。

综上所述，我们得出回文的规则：
> + 单个和零个字符都是回文，例如：**「1」**、**「2」**、**「3」**...等等
> + 如果字符串的第一个字符和最后一个字符相同，并且除了两个字符以外剩余的其他字符也是一个回文的话，字符串是一个回文，例如：**「16461」**、**「level」**、**「noon」**、**「nonon」**...等等

**如何用`JavaScript`来实现回文？**

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

[*`Array.prototype.reverse()`*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)实现

**`reverse()`是什么？**

在**MDN**中的介绍：

> [*`Array.prototype.reverse()`*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) 方法将数组中元素的位置颠倒，并返回该数组。数组的第一个元素会变成最后一个，数组的最后一个元素变成第一个。该方法**会改变原数组**。

简单来说就是可以将数组的元素位置顺序颠倒，并重新返回新的数组

**具体实现思路：**
> + 利用正则`/[\W_]/g`(或者`/[^A-Za-z0-9_]/g`)删除不必要的字符
> + 通过`toLowerCase()`将传入的字符串转换为小写字母
> + 利用`split()`方法将`string`对象分割成字符串数组，然后用`reverse()`方法将数组中的元素进行倒序，并返回该数组（会改变原来的数组），最后`join()`方法将这个数组的所有元素连接成一个字符串
> + 将返回的这个字符串再与原字符串进行比较是否完全相等

解释一下这里的正则表达式规则：
+ `\W`：匹配一个非单字字符
+ 等价于 `[^A-Za-z0-9_]`

那么`\W`的意思就是：
+ `[^A-Z]`匹配非26个大写字母中的任意一个
+ `[^a-z]`匹配非26个小写中的任意一个
+ `[^0-9]`匹配非**0**到**9**中的任意一个数字
+ `[^_]`匹配非下划线

主要会用到的正则表达式规则有：
```javascript
/[^A-Za-z0–9_]/g 
// 或 
/[\W_]/g
```

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

也可以写成：
```javascript
function checkPalindrome(str) {
  return str.replace(/[\W_]/g, '').toLowerCase() === str.replace(/[\W_]/g, '').toLowerCase().split('').reverse().join('');
}
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
