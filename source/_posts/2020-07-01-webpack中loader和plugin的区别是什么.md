---
title: webpack中loader和plugin 的区别是什么
date: 2020-07-01 17:44:32
tags:
category:
- [Webpack]
---

## [`Loader`](https://webpack.docschina.org/concepts/loaders/)

> `loader` 用于对模块的源代码进行转换。`loader` 可以使你在 import 或 "load(加载)" 模块时预处理文件。因此，`loader`类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的得力方式。loader可以将文件从不同的语言（如TypeScript）转换为 JavaScript 或将内联图像转换为 data URL。`loader`甚至允许你直接在 JavaScript 模块中 import CSS文件！

## Webpack中`loader`和`plugin`的区别？

**loader**

> `loader`，转换指定类型的模块功能，它是一个转换器，将A文件进行编译成B文件。
将`A.less`转换为`A.css`，单纯的文件转换过程。

> `plugin`，是一个扩展器，它丰富了Webpack本身，针对是loader结束后，webpack打包的整个过程，它并不直接操作文件，而是基于事件机制工作，会监听webpack打包过程中的某些节点，执行广泛的任务，比如：打包优化、文件管理、环境注入等

## 参考链接

> [Webpack-Loader](https://webpack.docschina.org/concepts/loaders/)
> [Webpack-Plugin](https://webpack.docschina.org/concepts/plugins/)
> [Webpack loaders vs plugins; what's the difference?](https://stackoverflow.com/questions/37452402/webpack-loaders-vs-plugins-whats-the-difference)
> [Github-webpack中loader和plugin的区别是什么](https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/308)
