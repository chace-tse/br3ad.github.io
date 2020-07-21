---
title: Vue-Router路由的三种模式
date: 2020-07-17 19:09:50
tags:
- Vue
- 前端
- Vue路由模式
category:
- [Vue]
- [前端]
---

## `hash`

> 使用`URL hash`值来做路由。支持所有浏览器，包括不支持 `HTML5 History Api`的浏览器

## `history`

> `history`模式依赖`HTML History Api`和服务器配置。美化后的`hash`模式，这种模式充分利用`history.pushState`API来完成`URL`跳转而无须重新加载页面。

```javascript
const router = new VueRouter({
  mode: 'history',
  router: [...]
})
```

## `abstract`

> `abstract`：支持所有JavaScript运行环境，如`Node.js`服务器端。**如果发现没有浏览器的API，路由会自动强制进入这个模式。**

## 参考链接

> [HTML5 History 模式](https://router.vuejs.org/zh/guide/essentials/history-mode.html#%E5%90%8E%E7%AB%AF%E9%85%8D%E7%BD%AE%E4%BE%8B%E5%AD%90)
> [Vue路由的三种模式](https://router.vuejs.org/zh/api/#routes)
