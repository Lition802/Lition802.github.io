---
title: 记一次oicq无法扫码登录的解决方案
categories:
  - 开发日记
cover: 1.png
tags:
  - oicq
  - mirai
abbrlink: 93f59e31
date: 2022-04-18 12:32:29
---

这几天突然出现了`oicq`登录时扫码显示环境异常的消息

![](2.jpg)

查了一下，原来是来自tx的愤怒

![](3.jpg)

只能强制`oicq`提交滑块验证码，但是在提交的时候会报`server is busy`然后直接断开连接。

搞了一晚上都没效果。

最后没办法只好上[mirai论坛](https://mirai.mamoe.net)看看

终于找到了[无法登录的临时处理方案](https://mirai.mamoe.net/topic/223/%E6%97%A0%E6%B3%95%E7%99%BB%E5%BD%95%E7%9A%84%E4%B8%B4%E6%97%B6%E5%A4%84%E7%90%86%E6%96%B9%E6%A1%88)

![](4.png)

这才知道滑块助手去年就不能用了，最新版需要`MiraiAndroid`辅助

[MiraiAndroid下载](https://install.appcenter.ms/users/mzdluo123/apps/miraiandroid/distribution_groups/release)

只要我们拿到**device.json**就可以跳过滑块直接登录。

MiraiAndroid提供了过滑块的方法，直接在MiraiAndroid登录后找到侧边栏，选择工具，然后导出device.json

这里放一下`oicq`和`mirai`协议的device.json对比

``` json oicq
  "--begin--": "该设备由账号作为seed固定生成，账号不变则永远相同",
  "product": "MRS4S",
  "device": "HIM188MOE",
  "board": "MIRAI-YYDS",
  "brand": "OICQX",
  "model": "Konata 2020",
  "wifi_ssid": "TP-LINK-a9279e78",
  "bootloader": "U-boot",
  "android_id": "OICQX.46742215.12",
  "boot_id": "b696d701-5aab-9fc2-946c-8d5c4f681a99",
  "proc_version": "Linux version 4.19.71-23211 (konata@takayama.github.com)",
  "mac_address": "00:50:9F:C2:94:6C",
  "ip_address": "10.0.141.92",
  "imei": "354330025964720",
  "incremental": 1332222617,
  "--end--": "修改后可能需要重新验证设备"
```

``` json mirai
{
    "deviceInfoVersion": 2,
    "data": {
        "display": "MIRAI.840537.001",
        "product": "mirai",
        "device": "mirai",
        "board": "mirai",
        "brand": "mamoe",
        "model": "mirai",
        "bootloader": "unknown",
        "fingerprint": "mamoe/mirai/mirai:10/MIRAI.200122.001/1806562:user/release-keys",
        "bootId": "AF4C4739-CE8A-A7BF-2A7D-F14C2E09A76F",
        "procVersion": "Linux version 3.0.31-Cq1qN990 (android-build@xxx.xxx.xxx.xxx.com)",
        "baseBand": "",
        "version": {
            "incremental": "5891938",
            "release": "10",
            "codename": "REL"
        },
        "simInfo": "T-Mobile",
        "osType": "android",
        "macAddress": "02:00:00:00:00:00",
        "wifiBSSID": "02:00:00:00:00:00",
        "wifiSSID": "<unknown ssid>",
        "imsiMd5": "553569922b3df7889344803c6ade19ec",
        "imei": "869455027156715",
        "apn": "wifi"
    }
}
```

基本上`oicq`需要的`mirai`都有生成，下一步就是改一改这个json。然后扔到`oicq`里面。

这里有一个坑，`oicq`的`android_id`是`mirai`的`display`，其他的没有问题。

然后就可以顺利登录了。