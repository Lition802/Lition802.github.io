---
title: 基于nodejs的微博系统
date: 2021-11-13 13:57:14
categories:
  - 开发日记
---

今天早上尝试着做了一个基于Node的微博系统

用到了`express`库，去[html5up](http://html5up.net)找了一个模板

结果发现写起来巨困难555...

遇到好多困难，例如`url.parse`被Node弃用了等等

不过今天新学到了`ejs`模块，可以实时渲染html

``` js
res.render('single/main',{
    name : '小华'
});
```

这个会把`single/main.html`内的`<%= name%>`替换为小华

# 特性

  - <% %> 用于控制流

  - <%= %> 用于转义的输出

  - <%- %> 用于非转义的输出

  - -%> 结束标签用于换行移除模式

  - 带有<%_ _%>的控制流使用空白字符移除模式

  - 自定义分隔符 (例如，使用 '<? ?>' 代替 '<% %>')

  - 客户端支持

  - 中介JavaScript的静态缓存

  - 模板的静态缓存

  - 与 Express 视图系统兼容

项目已在GitHub开源：https://github.com/Lition802/MCWeibo