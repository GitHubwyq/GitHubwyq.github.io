---
title: 'CSS reset文件'
date: 2017-11-30 19:22:15
tags: [CSS]
categories: "CSS"
---
#### 不多说，直接上代码
```CSS
*{
    margin: 0;
    padding: 0;
}
html{ 
    overflow-y: scroll; 
}
a{
    text-decoration: none;
}
a:active,a:hover,a:link,a:visited{
    text-decoration: underline;
}
input,button{
    border: none;
    outline: none;
}
textarea{
    outline: none;
}
li,ol{
    list-style: none;
}
i {
    font-style: normal;
}
table {
    border-collapse: collapse;
    border-spacing: 0;
}
/* 多行文本域的控制 */
textarea{
    resize: none;                   /*用户无法调整元素的尺寸*/
    /*resize: vertical;*/           /*用户可调整元素的高度*/
    /*resize: horizontal;*/         /*用户可调整元素的宽度*/
}
/* 文字对齐方式 */
.text_ce{
    text-align: center
}
.text_rt{
    text-align: right
}
.text_lf{
    text-align: left
}
/* 浮动 */
.fl{
    float: left;
}
.fr{
    float: right;
}
/* 清除浮动 */
.clearfix:after{
    content: '';
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
/* 弹性盒子 */
.flex {
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
}
.flex_v{
    -webkit-box-orient: vertical;
    -webkit-flex-direction: column;
    -ms-flex-direction: column;
    flex-direction: column;
}
.flex1{
    -webkit-box-flex: 1;
    -webkit-flex: 1;
    -ms-flex: 1;
    flex: 1;
}
.flex2{
    -webkit-box-flex: 2;
    -webkit-flex: 2;
    -ms-flex: 2;
    flex: 2;
}
.flex3{
    -webkit-box-flex: 3;
    -webkit-flex: 3;
    -ms-flex: 3;
    flex: 3;
}
.flex_hc{
    -webkit-justify-content: center;
    justify-content: center;
}
.flex_hm{
    display: -webkit-box;
     display: -webkit-flex;
     display: flex;
     -webkit-box-align: center;
     -webkit-align-items: center;
     align-items: center;
}
.flex_ld{
    -webkit-justify-content: space-between;
    justify-content: space-between;
}
.flex_k{
    -webkit-justify-content: space-around;
    justify-content: space-around;
}
/* 字体超出省略号 */
/* 一行文字 */
.text_ellipsis{
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
    word-wrap: normal;
    word-wrap: break-word;
    word-break: break-all;
}
/* 多行文字   谷歌才会出现的效果，为确保其他浏览器不出现样式问题，height:xxxpx  */
.moretext_ellipsis{
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
     overflow: hidden;
    word-break: break-all;
    word-wrap: break-word;
}  
```
#### 欢迎补充