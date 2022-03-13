---
title: LXLEssential
date: 2022-01-28 21:04:32
categories:
  - 开发日记
---

![](logo.png)

LXLEssential是一个综合性的多功能[LiteXLoader](https://lxl.litebds.com/)插件，为服务器提供多种实用的命令。

# 🆗简介

LXLEssential提供超过数十个有用的命令给几乎所有装载了[LiteXLoader](https://lxl.litebds.com/)的服务器

![](https://img.shields.io/badge/licence-AGPLv3-blue)


# 💾安装

下载方法有三种：
 - [从更新源下载](https://liteldev-lxl.coding.net/p/lxlessential/d/LXLEssential/git/raw/main/LXLEssential.js?download=true)
 - [从Github下载](https://github.com/LiteLDev-LXL/LXLEssential)
 - [从Minebbs下载](https://www.minebbs.com/resources/lxlessential.2836/)

1. 关闭服务器
2. 打开plugins文件夹
3. 放入LXLEssentials核心
4. 启动服务器
5. 安装完成！

# 🔨配置文件

LXLEssential是由多个组件组成的，你一般不需要/想要所有的组件，如果你不知道每个组件是干什么的，那么查看如下配置文件
``` json
{
	"home": {  //家园系统
		"enable": true,  //是否启用
		"cost": {
			"enable": false, //是否花费经济
			"money": 100  //花费的金额
		},
		"max": 15  //最大家的数量
	},
	"tpa": {
		"enable": true,
		"cost": {
			"enable": false,
			"money": 100
		},
		"timeout": 15  //tpa超时时间
	},
	"warp": {
		"enable": true,
		"cost": {
			"enable": false,
			"money": 100
		}
	},
	"back": {
		"enable": true,
		"auto":false, //重生时是否自动弹窗，开启立即重生的服务器可以尝试关闭此选项
		"cost": {
			"enable": false,
			"money": 100
		}
	},
	"tpr": {
		"enable": false,
		"cost": {
			"enable": true,
			"money": 100
		}
	},
	"economy": {
		"enable": true,
		"type": 1,  //经济模式，0为计分板，1为LLMoney
		"rate": 0.1,  //转载汇率，例如0.1为收取10%的手续费，0为全额转账
		"boardname": "money"  //如果是计分板的经济模式，需要填写计分板名称
	},
	"tool": {  //工具模块
		"getpos": {  //获取玩家坐标
			"enable": true, 
			"level": 0  //命令等级，0全体，1管理员
		},
		"kickall": {  //使服务器进入维护模式
			"enable": true
		},
		"suicide": {  //自杀
			"enable": true,
			"cost": {
				"enable": true,
				"money": 100 
			}
		},
		"notice": {  //公告系统
			"enable": true
		},
		"shop": {  //服务器商店
			"sell": {  //回收商店
				"enable": true
			},
			"buy": {  //出售商店
				"enable": true
			}
		}
	},
	"version": "3789",  //配置文件版本，随版本变更
	"lang": "zh_CN"  //语言文件模式，可选zh_CN,en_US
}
```

# 🎯命令

LXLEssential有众多命令，前提是你从配置文件中开启这些功能

🏨家园系统
[/sethome - 添加一个家](#sethome)
[/delhome - 删除一个家](#delhome)
[/gohome - 前往一个家](#gohome)

🔀传送系统
[/tpa - 打开玩家传送面板](#tpa)
[/tptoggle - 更改传送状态](#tptoggle)
[/tpr - 随机传送](#tpr)
[/back - 返回上一个死亡点](#back)

💱经济系统
[/balance - 查看经济余额](#balance)
[/balancetop - 查看服务器经济排行榜](#balancetop)
[/pay - 转账给在线玩家](#pay)
[/payoff - 转账给离线玩家](#payoff)

💰商店系统
[/buy - 查看服务器购买商店](#buy)
[/sell - 查看服务器回收商店](#sell)
[/setbuy - 管理员设置购买商店](#setbuy)
[/setsell - 设置回收商店](#setsell)

🔊公告系统
[/notice - 查看服务器公告](#notice)
[/setnotice - 管理员设置服务器公告](#setnotice)

🧪快捷工具
[/console - 执行控制台命令](#console)
[/suicide - 自杀](#suicide)

## tpa
传统的tpa功能，支持玩家之间互相传送
![](tpa.jpg)

## tptoggle
修改传送模式
关闭
![](tptoggle_refuse.png)
开启
![](tptoggle_open.png)
## back
回到你上一个死亡点

## gohome
传送到你设置的家
![](gohome.jpg)

## sethome
设置一个家
![](sethome.jpg)

## delhome
删除一个家
![](gohome.jpg)
*这里表单样式和gohome是一样的，因为都是选择一个家*

## gowarp
去往一个地标
![](gowarp.jpg)

## setwarp
设置一个地标
![](setwarp.jpg)

## delwarp
删除一个地标
![](gowarp.jpg)

## tpr
随机传送，传送距离限制为3000格内

## pay
转账给在线玩家
![](pay.jpg)

## payoff
转账给离线玩家
![](payoff.jpg)

## balance
查询玩家经济余额

## balancetop 
显示服务器经济排行榜
![](balancetop.jpg)

## getpos
获取一个玩家的坐标
![](getpos.jpg)
反馈
![](getpos_feedback.png)

## suicide
传说中的自杀

## notice
查看服务器公告
![](notice.jpg)

## setnotice
设置服务器公告
![](setnotice.jpg)

## sell
回收身上所有可回收的物品
![](sell_ask.jpg)
![](sell.jpg)

## setsell
当你手中没有物品时使用这个命令，会列出所有回收物品表，可以修改或者删除
![](setsell_all.jpg)
当你手中有物品时，会设置手中物品类型的回收价格
**注意：物品的耐久也被记录，所以损失耐久的工具和未损失耐久的工具并不是同一类物品**
![](setsell_hand.jpg)

## price
查询手中物品的回收价格
![](price.png)

## setbuy
设置出售商店
![](setbuy.jpg)
注意：**设置的是你手中物品的出售价格**
![](setbuy2.jpg)

## buy
购买商品
![](buy.jpg)

## console
快捷执行控制台命令
可以用@s代替自己
![](console.jpg)

# ❓常见问题及其解答

## 1.为什么经济不能用？加钱没有反应？

查看你配置文件中的经济模式是否填写正确

## 2.我不需要某某某功能，如何关闭？

在配置文件中把`enable`项设置为`false`即可

## 3.插件初始化失败了

检查一下你的config.json填写是否正确

如果生成了错误报告，加入售后群反馈给开发者即可。

