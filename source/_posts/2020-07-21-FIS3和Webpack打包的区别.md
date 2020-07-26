---
title: FIS3和Webpack打包的区别
date: 2020-07-21 20:09:19
tags:
- 前端
- 前端基础
- 前端工程化
- FIS3
- Webpack
category:
- [前端]
- [前端工程化]
---

## [*FIS3*](http://fis.baidu.com/)

> `FIS3`是**面向前端的构建工具**，主要解决了前端性能优化、资源加载（异步、同步、按需、预加载、依赖管理、合并、内嵌）
> **`FIS3`的构建不会修改源码，而是通过用户设置，将构建结果输出到指定的目录**

### FIS的工作原理

整个`FIS3`的构建流程：

- 扫描项目目录拿到文件并初始化出一个文件对象列表
- 对文件对象中每一个文件进行单文件编译
- 获取用户设置的`package`插件，进行打包处理

## [*Webpack*](https://www.webpackjs.com/)

**webpack核心概念**

> `entry`一个可执行模块或库的入口文件
> `chunk`多个文件组成的一个代码块
> `loader`文件转换器，比如把`ES6`转换为`ES5`，`SCSS`转换为`CSS`
> `plugin`插件，勇于扩展`Webpack`的功能，在`Webpack`构建

## FIS和Webpack的区别

> `FIS`是一个前端解决方案，基于静态资源标记+动态资源解析表，可以说fis真正做到了静态资源动态按需加载。
> `Webpack`是静态打包，生成`chunk`需要手动配置`entry`，可以依赖npm社区，`plugin`扩展，相比`FIS`，`Webpack`前端模块化生态更完善，代码本身的质量和可靠性比`FIS`更强
> `Webpack`是以`JavaScript`为中心，针对`JavaScript`去分析各个依赖，控制构建过程。`FIS`是以`HTML`为中心，分析各个`HTML`的依赖控制构建过程

## 参考链接

> [FIS3和Webpack有什么区别？](https://www.zhihu.com/question/50829160)
> [fex-team/fis3](https://github.com/fex-team/fis3)
> [FIS3 VS Webpack](http://liveipool.com/blog/2016/09/15/FIS3-VS-Webpack/)
