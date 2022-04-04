---
title: SVIP2的使用教程
categories:
  - 开发日记
cover: 1.png
tags:
  - minecarft
  - bds
abbrlink: 806a4d2d
date: 2022-04-03 22:01:59
---

![](2.jpg)

先来看配置文件

``` json config.json
{
	"up_level_minute": 10, //升级所需的在线累计时间，玩家当前等级*这个值是玩家升到下一级所需的
	"buy": 10000,  //买一个月VIP所需的金币
	"tips_level": 3,  //可以自定义进服提示的等级
	"particle_level": 5  //可以自定义粒子效果的等级
}
```

有几点要注意的（其实是客户要求的）
1. op和普通玩家可以用的粒子效果不一样，具体查看`SVIP2/particle`文件夹，想自定义就改里面的内容就可以
2. VIP等级和在线时间挂钩
3. VIP不同等级有不同的权限，比如粒子效果和进服提示
4. 命令是/vip gui，真命令
5. 续费只能按月加，设计问题，但是不影响使用

![](3.jpg)
然后就没啥了，[下载链接](SVIP2.zip)