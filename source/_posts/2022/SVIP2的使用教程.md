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
`particle.json`里面的东西格式都一样，我单拿一个出来讲
``` json particle.json
{
  "小型黑色药水气泡": {  //按钮上显示的名字
    "particle": "minecraft:arrow_spell_emitter",  //粒子名称，来自minecarft wiki
    "level": 5,  //到多少级之后才可以使用这个粒子
    "opOnly": false  //是不是op专属
  }
}
```

有几点要注意的
1. op和普通玩家可以用的粒子效果不一样，具体查看`SVIP2/particle.json`，想自定义就改里面的内容就可以
2. VIP等级和在线时间挂钩
3. VIP不同等级有不同的权限，比如粒子效果和进服提示
4. 命令是/vip
5. 续费只能按月加

![](3.jpg)
