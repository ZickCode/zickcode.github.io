---
title: css3计算属性calc()
date: 2017-04-08 19:39:16
tags: css
---

calc是css3的新属性，可以使用四则运算动态计算样式的值，例如border、margin、pading、font-size和width等属性设置动态值。表达式中有加/减时必须在两边加上空格，否则会报错。
例如
```
width:calc(50% + 2px);
```
例：子元素有padding和border时，width:100%;
```
.box{width:300px;}
//父元素的100%宽度减去两边的border和padding
.box p{border:1px solid #000;padding:20px;height:100px;width:cale(100% - (1 + 20) * 2);}
```
注意：calc()会触发重绘，所以会影响页面性能。