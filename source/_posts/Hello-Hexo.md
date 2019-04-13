---
title: 'Hello,Hexo'
date: 2018-08-23 16:22:15
tags: [随笔]
---
### 迁移注意问题说明
> 1.执行clone命名
>> git clone -b hexo 路径

> 2.安装依赖
>> 直接执行 npm install命令（不用执行其他的命令了）

### 迁移后注意事项
1. 新建博客命：hexo new post "博客名"

2. 完成后先提交代码 直接提交到hexo分支上，不用想master分支上推。 提交代码时不用提交package-lock.json文件。只提交写的文件就行，.json后缀的文件都不用提交

3. 执行发布命令 hexo g -d


