---
title: hexo-admin安装使用
author: Lition
abbrlink: 4ffa5bc6
tags:
  - hexo
  - git
categories:
  - 学习笔记
date: 2022-04-14 11:10:00
cover: 2.jpg
---
# 概要

如果自己编辑 MD 文件的话，确实比较麻烦，你可以用一些 MD 的编辑器，但是在管理 MD 文件上还是操作不方便。
这里推荐使用 hexo-admin，而且编辑完之后可以马上看到效果呢。
需要说明的是，hexo-admin 管理是本地用的，就是你需要在本地编辑完之后再上传到 github，而不能直接在线编辑保存，因为 github pages 只支持静态页面的。

# 安装过程

## 前提
基于版本”hexo”: “^3.7.0”，”hexo-admin”: “^2.3.0”。

## 安装 hexo-admin
cd hexo 目录

``` bash
npm install --save hexo-admin
```

启动 hexo
``` bash
hexo s
```
然后打开 http://localhost:4000/admin/ 就可以看到管理页面。

## 在 hexo-admin 你可以

![](1.png)

* Pages - 新加 page；
* Posts - 新加或删除 post；双击一个 post，你可以编辑，预览，新增修改 tags、categories，选择发布或不发布；
* Settings - 一些配置；
* Deploy - 可以直接部署到 github。