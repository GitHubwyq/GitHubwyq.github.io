---
title: elementUi的upload组件-action属性
date: 2019-03-13 13:54:31
tags: [vue]
categories: "vue"
---
#### 最近在适用VUE作为前端框架做自己的项目，在做到需要上传文件到服务器时,考虑到上传服务器的地址以后会变化，于是就想到action属性能不能赋值个变量，以后服务器地址改变后，直接改这个变量就行了
##### 于是查了一些资料，需要把action写成:action，然后后面跟着一个方法名，调用方法，返回你想要的地址，代码示例：
```js
//html部分
<el-upload  :action="UploadUrl()"  :on-success="UploadSuccess" :file-list="fileList">
    <el-button size="small" type="primary" >点击上传</el-button>
    <div slot="tip" class="el-upload__tip"></div>
</el-upload>
//methods中的方法部分
methods:{
    UploadUrl:function(){
        return "返回需要上传的地址";     
    }   
}   
```
##### 你可以把这个公用的url挂载到全局中（写在main.js中）
```js
Vue.prototype.url='服务器地址'
```
##### 使用的时候直接用```this.url```就能访问到
