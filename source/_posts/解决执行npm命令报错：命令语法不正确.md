---
title: 解决执行npm命令报错：命令语法不正确
tags: 技术
abbrlink: 42779
date: 2023-12-30 20:22:09
---


问题：执行npm命令报错：命令语法不正确

分析：由于更改了npm prefix文件中的全局安装路径，导致config混乱

解决办法：删除C盘中的.npmrc文件，路径为`C:\用户名\.npmrc`