---
title: 获取B站视频下载链接
tags: 日常
abbrlink: 45317
date: 2022-04-11 09:45:01
---

<!-- https://api.bilibili.com/x/player/playurl?avid=797486918&cid=245068432&qn=1&type=&otype=json&platform=html5&high_quality=1 -->

这个方法是目前市面上最常规和高清的解析方法。获取到的也直接是MP4。使用本文的方法可以从此远离所有的解析程序。当然操作步骤有点麻烦。

B站的视频解析需要两个参数，aid和cid。它对标的就是视频和分段。

那怎么拿到这两个参数呢，需要下面这个接口

```
[GET] http://api.bilibili.com/x/web-interface/view?bvid={BVID}
```

把上面的`{BVID}`换成你需要查询的BVID即可

我们拿`BV1jy4y1r74k`来举例子

访问`http://api.bilibili.com/x/web-interface/view?bvid=BV1jy4y1r74k`

![](https://s11.ax1x.com/2023/12/25/piHwaQJ.png)

这里我们取`data`部分来看

``` json
{
    "bvid": "BV1jy4y1r74k",
    "aid": 797486918,  //  <- aid
    "videos": 1,
    "tid": 86,
    "tname": "特摄",
    "copyright": 2,
    "pic": "http://i1.hdslb.com/bfs/archive/259550d2fb9cc0c5e380e7e8d8fe382512cb75a3.jpg",
    "title": "【KRL字幕组】不破使用日本狼变身和必杀片段",
    "desc": "视频素材来自KRL字幕组",
    "duration": 107,
    "owner": {
      "mid": 44918570,
      "name": "一只布瑞",
      "face": "http://i2.hdslb.com/bfs/face/591b17c4005e071a84fe8e4480a0bd52f6307d71.jpg"
    },
    "cid": 245068432,  // <- cid
}
```

接着我们访问

``` 
[GET] https://api.bilibili.com/x/player/playurl?avid={AID}&cid={CID}&qn=1&type=&otype=json&platform=html5&high_quality=1 
```

`{AID}`换成上面获取的aid，`{CID}`换成上面获取的cid

我们的结果这就出来了

![](https://s11.ax1x.com/2023/12/25/piHwNz4.png)

`durl.url`和`durl.backup_url`都是可以播放的MP4

然后各位就可以拿去下载工具里下载，或在浏览器里访问，然后右击下载了。