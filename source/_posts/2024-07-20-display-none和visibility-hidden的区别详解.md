---
title: 'display:none和visibility:hidden的区别详解'
date: 2024-07-20 21:26:01
tags:
  - 前端开发
  - CSS
  - CSS 显示隐藏
  - display
  - visibility
category:
- [CSS]
---

区别：**display: none;不占据文档流空间。visibility: hidden;还占据原来的位置，只是看不见。**

## 「深入理解`display: none;`」

**定义：**将 `display` 设置为 `none` 会将元素从 可访问性树 accessibility tree 中移除。这会导致该元素及其所有子代元素不再被屏幕阅读技术 screen reading technology 访问。

> 当父元素为`display:none`，所有的后代元素也不会再显示。
> 可进行`DOM`操作，不能进行响应任何事件

## 「深入理解`visibility:hidden`」

**定义：**CSS属性 `visibility` 显示或隐藏元素而不更改文档的布局，还占据文档流空间
隐藏元素，但是其他元素的布局不改变，相当于此元素变成透明。要注意若将其子元素设为 `visibility: visible`，则该子元素依然可见。

> [*注：要隐藏并从文档布局中移除元素，将 display 属性设置为 none 来代替 visibility 属性。*](https://developer.mozilla.org/zh-CN/docs/Web/CSS/visibility)

**使用场景：**

- 隐藏表格的行和列
- 不触发布局的情况下隐藏元素 常用值
- `visible`：显示
- `hidden`：不可视，保持位置
- `collaose`：用于表格元素
- `inherit`：继承父元素的`visibility`值

## 「对比」

- 设置为`visibility：hidden`的元素其子元素设置为`visibility: visible`还可以显示
- 两者都无法获得焦点
- 不会妨碍表单的提交
- `transition`的影响对表单的改变有效
- `visibility`不会触发reflow回流。只会重绘

## 参考内容

> + [*https://developer.mozilla.org/zh-CN/docs/Web/CSS/visibility*](https://developer.mozilla.org/zh-CN/docs/Web/CSS/visibility)
> + [*https://developer.mozilla.org/zh-CN/docs/Web/CSS/display*](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display)
> + [*display:none和visibility:hidden区别详解*](https://juejin.cn/post/6976447436701040647)
