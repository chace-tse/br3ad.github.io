---
title: 深入理解JavaScript执行环境与作用域和作用域链
date: 2020-07-21 18:58:19
tags:
- 前端
- 前端基础
- JavaScript执行环境
- JavaScript作用域
- JavaScript作用域链
category:
- [前端]
- [JavaScript]
---

通常将JavaScript归类为“动态”或“解释执行”语言，JavaScript引擎进行编译的步骤和传统的编译语言非常相似，在某些环节可能比预想的要复杂些。

在传统编译语言的流程中，程序中的一段源代码在执行之前会经历三个步骤，统称为“编译”

- 分词 / 词法分析（Tokenizing / Lexing）
- 解析 / 语法分析（Parsing）
- 代码生成（AST）

## JS执行环境及作用域（execution context And Scope）

### 执行环境**

> 每个执行环境都有一个与之关联的变量对象（variable object）


### 作用域（Scope）

**什么是作用域？**

所有的Window对象的属性拥有全局作用域

**全局作用域和函数作用域**

**JavaScript中作用域链和执行上下文有什么区别？**

> 执行上下文在运行时确定，随时可能改变；作用域在定义时就确定，并且不会改变。

**快级作用域**

### 作用域链（Scope chain）

**什么是自由变量？**

**什么是作用域链？（Scope chain）**

**关于自由变量的取值**

## 作用域与执行上下文

## 参考文章和书籍

> [深入理解javascript原型和闭包系列](https://www.cnblogs.com/wangfupeng1988/p/4001284.html)
> [Web 前端面试指南与高频考题解析](https://juejin.im/book/5a8f9ddcf265da4e9f6fb959/section/5a8f9ed96fb9a0633229bddf)
> [JavaScript 开发进阶：理解 JavaScript 作用域和作用域链](https://www.cnblogs.com/lhb25/archive/2011/09/06/javascript-scope-chain.html)
> [JavaScript 作用域和作用域链](https://gaohaoyang.github.io/2015/05/20/scope/#top)
> [深入理解ES6](https://book.douban.com/subject/27072230/)
