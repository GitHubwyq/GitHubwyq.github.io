---
title: vue打包后路径报错问题
date: 2019-06-10 23:17:55
tags: [vue]
categories: "vue"
---
#### vue文件打包后的问题
#### 打包后，打开index.html文件报错（net::ERR_CONNECTION_REFUSED）
如图

![Image text](https://github.com/GitHubwyq/photos/blob/master/imgs/1001313-20181121180313427-1187140394.png?raw=true)

> 报错原因是index.html文件的资源引入路径有错误  

#### 解决方案  
> 步骤①、打开config/index.js文件，将build->assetsPublicPath改为“./”，即可，就是前面加个点。代码如下
```js
build: {
    // Template for index.html
    index: path.resolve(__dirname, "../dist/index.html"),


    //新增打包后配置文件
    // Paths
    assetsRoot: path.resolve(__dirname, "../dist"),
    assetsSubDirectory: "static",
    assetsPublicPath: "./",

```

> 步骤②、找到 build->utils.js,在里面加入一句publicPath:'../../',
```js
if (options.extract) {
    return ExtractTextPlugin.extract({
    use: loaders,
    publicPath:'../../',
    fallback: 'vue-style-loader'
    })
} else {
    return ['vue-style-loader'].concat(loaders)
}
```

