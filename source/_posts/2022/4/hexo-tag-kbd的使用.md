---
title: hexo-tag-kbd的使用
categories:
  - 学习笔记
abbrlink: e6630a51
date: 2022-04-18 08:35:01
tags:
 - hexo
cover: kbd-all.png
---


显示帖子/页面中的键帽。
用法很简单，如下。

![](kbd-all.png)

```
{% kbd Ctrl %}
{% kbd A %}
```

如果要使用快捷方式，如下。

![](kbd2.png)

```
{% kbd Ctrl %} + {% kbd A %}
{% kbd Ctrl %} + {% kbd ALT %} + {% kbd DELETE %}
```

键符号显示如下。
* Enter
* Shift
* Command
* Option

## For Examples

#### HHKB

I LOVE HHKB.

![](kbd1.png)


#### Enter
![](kbd3.png)

#### Shift
![](kbd4.png)

#### Command
![](kbd5.png)

#### Option
![](kbd6.png)

## Install

```
npm install hexo-tag-kbd@latest --save
```