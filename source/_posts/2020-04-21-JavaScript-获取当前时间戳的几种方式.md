---
title: JavaScript 获取当前时间戳的几种方式
date: 2020-04-21 15:43:33
tags:
category:
---

## [`Date.parse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse)

```javascript
let timestamp = Date.parse(new Date());

Console.log(timestamp);
// 1587452848000 获取的时间戳是把毫秒改成000显示，因为这种方式只精确到秒
```

## [`Date.prototype.valueOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

```javascript
let timestamp = (new Date()).valueOf();

console.log(timestamp);
// 1587452987750 获取当前毫秒的时间戳
```

## [`Date.prototype.getTime()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getTime)

```javascript
let timestamp = new Date().getTime();

console.log(timestamp);
// 1587453889920 获取当前毫秒的时间戳
```
