---
title: css实现三角形原理！
date: 2017-12-10 20:56:51
tags: [CSS]
categories: "CSS"
---
> 对于一个块级元素，但我们分别将元素的上下左右四个border设置成一个比较大的像素（如10px），样式设置成solid ,分别设置成不同的颜色的时候，同时将元素的width,height设置为0.这时我们将会看到四条边均呈现为三角形的形状。如图：

{% asset_img 20160709112257058.png 如图 %}

其css样式为：

```
        .element{
            width: 0px;
            height: 0px;
            border-top: 20px solid aqua;
            border-right: 20px solid #760000;
            border-bottom: 20px solid blue;
            border-left: 20px solid darkkhaki;
        }

```
