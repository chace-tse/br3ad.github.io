---
title: npm install安装依赖包出现超过最大调用堆栈大小
date: 2020-01-08 19:26:22
tags:
- 前端
- npm
- node
category:
- [前端]
- [npm]
---

## 问题

> **问题描述：**在使用`npm install`安装依赖包超过最大调用堆栈大小的`error `

**错误信息：**

```sh
npm ERR! Maximum call stack size exceeded
npm ERR! A complete log of this run can be found in:
```

## 解决方案

> 思路：删除所有`npm `依赖项的内容，并强制性清除npm依赖的缓存，再重新`npm install`

**强制清除npm依赖包的缓存**

```sh
npm cache clean --force
```

**重新安装所需依赖**

```sh
npm install -g babel-cli
```

Ok, Done. 完美解决.

## 参考链接

> [*Maximum call stack size exceeded on npm install*](https://stackoverflow.com/questions/40566348/maximum-call-stack-size-exceeded-on-npm-install)

