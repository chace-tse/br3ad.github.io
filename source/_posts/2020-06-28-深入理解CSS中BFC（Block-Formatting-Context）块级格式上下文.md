---
title: 深入理解CSS中BFC（Block Formatting Context）块级格式上下文
date: 2020-06-28 00:56:32
tags:
  - 前端开发
  - CSS
  - CSS BFC
  - CSS Layout
  - CSS 布局
  - CSS 块级格式上下文
category:
- [CSS]
- 前端
---

## 常见定位方案

**普通流 (normal flow)**
> 在普通流中，元素按照其在 HTML 中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。

**浮动 (float)**
> 在浮动布局中，元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移，其效果与印刷排版中的文本环绕相似。

**绝对定位 (absolute positioning)**
> 在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定。

## BFC 概念

> BFC 即 Block Formatting Contexts (块级格式化上下文)，它属于上述定位方案的普通流。
**什么是BFC？**
> 块格式化上下文（Block Formatting Context，BFC）是Web页面的可视CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。
> 具有BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的一些特性。

## 触发BFC

**触发条件**
> 根元素`<html>`
> 浮动元素(元素的`float`属性不为`none`)
> 绝对定位元素（元素的`position`为`absolute`或`fixed`）
> 行内块元素 (元素的`display`为`inline-block`)
> 表格单元格(元素的`display`为`table-cell`，`html`表格单元格默认为该值)
> 表格标题(元素的`display`为`table-caption`，`html`表格标题默认为该值)
> 匿名表格单元格元素(元素的`display`为`table`、`table-row`、`table-row-group`、`table-header-group`、`table-footer-group`（分别是`HTML table`、`row`、`tbody`、`thead`、`tfoot`的默认属性）或`inline-block`)
> `overflow`值不为`visible`的快元素
> `display`值为`flow-root`的元素
> `contain` 值为`layout`、`content`或`paint`的元素
> 弹性元素（`display`为`flex`或`inline-flex`元素的直接子元素）
> 网格元素（`display`为`grid`或`inline-grid`元素的直接子元素）
> 多列容器（元素的`column-count`或`column-width`不为`auto`，包括 `column-count`为1）
> `column-span`为`all`的元素始终会创建一个新的*BFC*，即使该元素没有包裹在一个多列容器中

## BFC 特性及应用

**同一个BFC下外边距会发生折叠**

```html
<head>
  <style>
    div {
      width: 100px;
      height: 100px;
      background: lightblue;
      margin: 100px;
    }
  </style>
</head>
<body>
  <div></div>
  <div></div>
</body>
```
**想要避免外边距的重叠，可以将其放在不同的 BFC 容器中。**

**改造一下代码**

```html
<head>
  <style>
    .container {
      overflow: hidden;
    }
    p {
      margin: 100px;
      width: 100px;
      height: 100px;
      background: lightblue;
    }
  </style>
</head>
<body>
  <div class="container">
    <p></p>
  </div>
  <div class="container">
    <p></p>
  </div>
</body>
```

**BFC 可以包含浮动的元素（清除内部浮动）**

> **浮动原理：** 浮动的元素会脱离普通文档流，导致父元素的高度塌陷
> **清楚浮动原理：** 触发父元素的BFC属性，使下面的子元素都处在父元素的同一个BFC区域之内，此时已成功清除浮动

```html
<head>
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    .parent {
      border: 1px solid #000;
      overflow: hidden;
    }
    .child {
      float: left;
      width: 100px;
      height: 100px;
      background: #eee;
    }
  </style>
</head>
<body>
  <div class="parent">
    <div class="child"></div>
  </div>
</body>
```

**BFC 可以阻止元素被float box重叠**

```html
<head>
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    .box1 {
      float: left;
      width: 100px;
      height: 100px;
      background: lightblue;
    }
    .box2 {
      overflow: hidden;
      height: 100px;
      background: #eee;
    }
  </style>
</head>
<body>
  <div class="box1">left float elements</div>
  <div class="box2">没有设置浮动，也没有触发BFC元素，width: 200px; height: 200px; background: #eee;</div>
</body>
```

*PS：用于实现两列自适应布局，左边的宽度固定，右边的内容自适应宽度*

## BFC 与 Layout

在IE浏览器中不支持BFC标准，于是IE中有了Layout，**Layout 和 BFC 基本是等价的**，为了处理IE的兼容性，在需要触发BFC时，除了需要用触发条件中的 CSS 属性来触发 BFC，还需要针对IE浏览器使用`zoom: 1;`来触发IE浏览器的Layout。

```html
<head>
  <style>
    .parent {
      width: 300px;
      margin-top: 3rem;
      border: 5px solid #fcc;
    }
    .child {
      float: left;
      border: 5px solid #f66;
      width: 100px;
      height: 100px;
    }
  </style>
</head>
<body>
  <div class="parent"></div>
  <div class="child"></div>
</body>
```

**BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。**

**文字环绕`float`**

```html
<head>
  <style>
    * {
      margin: 0;
      padding: 0;
    }
    .box1 {
      float: left;
      width: 100px;
      height: 100px;
      background: #000;
    }
    .box2 {
      height: 200px;
      background: #aaa;
    }
    .red-box {
      width: 30px;
      height: 30px;
      background: red;
    }
  </style>
</head>
<body>
<div class="box-1"></div>
<div class="box-2">
  <div class="red-box"></div>
  <p>content</p><p>content</p><p>content</p><p>content</p><p>content</p>
</div>
</body>
```

**`float`的定义和用法：**

> `float` 属性定义元素在哪个方向浮动。以往这个属性总应用于图像，**使文本围绕在图像周围**，不过在CSS中，**任何元素都可以浮动**。浮动元素会生成一个块级框，而不论它本身是何种元素。

可以看到，`box-2`盒子的左上角被`box-1`盒子覆盖了，而文本却没有被`box-1`盒子覆盖。

盒子会被float的盒子所覆盖，但盒子但文本却没有被float的盒子覆盖

是因为，**`float`设计初衷是为了使文本围绕在浮动对象的周围。**

## 参考链接

> [博客园-前端精选文摘：BFC 神奇背后的原理](https://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html)
> [知乎-10分钟理解BFC](https://zhuanlan.zhihu.com/p/25321647)
> [CSS深入理解流体特性和BFC特性下多栏自适应布局](https://www.zhangxinxu.com/wordpress/2015/02/css-deep-understand-flow-bfc-column-two-auto-layout/)
> [MDN-块格式化上下文（Block Formatting Context, BFC）](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
> [stackoverflow-How does the CSS Block Formatting Context work?](https://stackoverflow.com/questions/6196725/how-does-the-css-block-formatting-context-work)
> [w3g-Block-formatting-contexts](https://www.w3.org/TR/CSS2/visuren.html#block-formatting)
