---
title: 单独更改elementuUi的表格样式
date: 2019-03-09 23:41:14
tags: [vue]
categories: "vue"
---
#### element更改表格表头、行、指定单元格样式
#### 更改表格的样式
##### 使用header-cell-style属性，可为函数或对象
##### 1、函数写法
```html
<!-- html -->
<el-table :header-cell-style="rowClass"></el-table>
```
```js
//在method里面写上方法
rowClass({ row, rowIndex}) {
    console.log(rowIndex) //表头行标号为0
    return 'background:red'
}
```
##### 2、对象写法
```html
<!-- html -->
<el-table :header-cell-style="{background:'red'}"></el-table>
```
#### 更改表格中某个单元格的样式
##### 1、函数写法
```html
<!-- html -->
<el-table :header-cell-style="cellStyle"></el-table>
```
```js

//在method里面写上方法
cellStyle({row, column, rowIndex, columnIndex}){
    if(rowIndex === 1 && columnIndex === 2){ //指定坐标
        return 'background:pink'
    }else{
        return ''
    }
}
```
##### 2、对象写法
```html
<!-- html -->
<el-table :cell-style="{background:'pink'}"></el-table>
```

