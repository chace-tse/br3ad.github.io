---
title: JavaScript长字符串拆分并换行处理
date: 2020-02-29 01:45:16
tags:
  - 前端
  - JavaScript
category:
- [前端]
- [JavaScript]
---


# JavaScript 如何将一个长段字符串进行拆分并换行？

**如：**

```javascript
let str = '这是一个很长很长的字符串 很长很长的字符串 很长很长的字符串 很长很长的字符串 很长很长的字符串 很长很长的字符串 很长很长的字符串 很长很长的字符串 很长很长的字符串';
```

**解决方案：**

利用 `<br/>` 进行换行
```javascript
var reg = new RegExp(' ', '\g');
    str = str.replace(reg, '<br />');
    console.log(str);
```

**整体思路：**
1、利用`split()`进行切割，占位符( )
2、遍历切割后的数组
3、[splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)将切分后的数组拼接换行符再拼接完整的字符串

## 参考链接

+ [*怎么用JavaScript拆分字符串并换行*](https://segmentfault.com/q/1010000012225245)
+ [*怎么用JavaScript拆分字符串并换行*](http://www.imooc.com/wenda/detail/501889)
+ [*MDN-Array.prototype.splice()*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
