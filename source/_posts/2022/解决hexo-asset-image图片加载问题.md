---
title: 解决hexo-asset-image图片加载问题
categories:
  - 学习笔记
cover: 1.png
abbrlink: 2663107d
date: 2022-03-14 21:51:44
tags:
 - hexo
---

# 起因

换了新主题之后，图片加载出了点问题。

原图片写法是这样的

``` markdown
![](xxx.jpg)
```

但是hexo渲染之后变成了
``` html
<img src=/.io/img/xxx.jpg/>
```

去网上搜索了一下发现是`hexo-asset-image`的问题

![](2.png)

原来是截取字符串的问题，但是这个仓库已经archived了，npm那边下载过来也只是旧版本

# 解决方法

打开`hexo-asset-image/index.js`

修改第24行

``` js
  else {
   var endPos = link.length-1;
  }
```

