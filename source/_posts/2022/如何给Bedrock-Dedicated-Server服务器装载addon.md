---
title: 如何给Bedrock Dedicated Server服务器装载addon
categories:
  - 开发日记
cover: dir.png
abbrlink: a820ba8e
date: 2022-03-15 10:02:28
---

如何给自己的的Bedrock Dedicated Server服务器装载addon已经成为了每个新人服主的日经问题，这里专门开一帖来详细讲述一下。

# 准备工作

你需要一个[EasyPacks](https://www.minebbs.com/resources/easypacks-addon.2334/)

还有你下载好的`.mcaddon`文件

这里选一个示例的`Dynamic Ligting v4.mcaddon`，移动光源

![](addon.png)

# 解压

先点开你的地图文件夹，我这里用的是默认的`Bedorck level`

把刚才下载的`EasyPacke.exe`和准备好的addon文件放进来

{% note warning simple %}
如果没有`behavior_packs`和`resource_packs`这两个文件夹，需要您自行创建
{% endnote %}

![](dir.png)

把你的addon文件拖到`EasyPacks.exe`上，会自动解压缩

![](unzip.png)

敲一下回车，这个窗口会自动关闭，接着你会发现多了一个解压好的文件夹

![](dir2.png)

里面是这样的

![](dir3.png)

我们运气比较不好，正常情况下会是一个或几个文件夹，这里是作者把单独的文件夹又打包了

重复上面的操作，继续用`EasyPacks.exe`解压

![](dir4.png)

全部解压完就可进行安装了。

# 装载

下面是标准的addon文件根目录样式

```
├── xxxx 
├── xxxx
├── manifest.json
└── pick_icon.png
```

进到我们解压好的文件夹里面，点进去

一直点，直到发现`manifest.json`这个文件，一般来说同级还会有一个`pick_icon.png`

![](dir5.png)

点进`manifest.json`

``` json manifest.json
{
    "format_version": 2,
    "header": {
        "description": "Made By: Dewdimpple/Amon28,Twitter: @dewdimpple,Youtube: Dewdimpple",
        "name": "Dynamic Lighting B v4",
        "uuid": "d9675696-e757-41d2-9918-82aae6803931",
        "version": [ 3, 3, 4 ],
        "min_engine_version": [ 1, 16, 0 ]
    },
    "modules": [
        {
            "description": "Example vanilla behavior pack",
            "type": "data",  // <-- 看这里！！
            "uuid": "fa6e90c8-c925-460f-8155-c8a60b753caa",
            "version": [3, 3, 4]
        }
    ]
}
```
{% note info simple %}
**这里做了一些截取，只留下需要展示的键值对。**
{% endnote %}


查看`modules`项的第一个`type`

如果是`data`或者`script`就把这个文件夹移动到`behavior_packs`，如果是`resoure`就移动到`resource_packs`

对于展示这个文件来说，第13行的`type`为`data`，所以这个文件夹需要移动到`behavior_packs`里面

我们需要的文件夹是点进去就能看到`manifest.json`的文件夹，所以对于上图来说

我们需要移动的是`Dynamic Lighting B`而不是`Dynamic Lighting B.mcpack.unzip`

直接移动到地图文件夹，db同级的`behavior_packs`里

如果`type`是`resoure`则需要移动到`resoure_packs`

![](dir6.png)

# 生成json

把所有文件夹都移动到位之后

运行地图文件夹的`EasyPacks.exe`

![](dir7.png)

可以看到EasyPacks加载了两个包，并生成了`world_behavior_packs.json`和`world_resoure_packs.json`

有时候只有资源包或者只有行为包的话，只会生成一个json文件

# 开服

接下来，启动服务器，连接世界

如果出现`此世界已装载资源包..`等字样，表明装载成功!