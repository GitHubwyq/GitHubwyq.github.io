---
title: 'Hello,Hexo'
date: 2017-11-23 16:22:15
tags: [hexo]
categories: "hexo"
---
### 迁移注意问题说明
> 1.执行clone命名
>> git clone -b hexo 路径

> 2.安装依赖
>> 依次执行 npm install hexo(最好全局安装hexo，不然hexo环境变量不主动配置) npm insatll hexo-deployer-git     (*切记不要执行hexo init)


### 迁移后注意事项
1. 新建博客命：hexo new post "博客名"

2. 完成后先提交代码 直接提交到hexo分支上，不用向master分支上推。 提交代码时不用提交package-lock.json文件。只提交写的文件就行，.json后缀的文件都不用提交

3. 执行发布命令 hexo g -d


