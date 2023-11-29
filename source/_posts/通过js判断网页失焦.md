---
title: 通过js判断网页失焦
abbrlink: 17908
date: 2023-11-30 00:40:44
tags: 技术
---

考试的时候看到考试软件有检测失焦的功能，切屏到一定次数会判定为不及格，好奇的了解了一下原理。

以下摘自W3school。
> `onblur`是一个JavaScript事件，用于在元素失去焦点时触发特定的操作或函数。`onblur` 事件与 `onfocus` 事件相反。

通过js监听`onfous`和`onblur`事件，自己尝试实现了一下。

```js
let blurtime = null;
let focustime = null;
let isFirst = true;
window.onfocus = function() {
	focustime = new Date().valueOf();
	let second = (focustime - blurtime) / 1000;
	second = Math.round((second + Number.EPSILON) * 10) / 10;
	if (!isFirst) {
		console.log(`请注意，你失去焦点了！总共离开${second}秒`);
	}
};
window.onblur = function() {
	if (isFirst) {
		isFirst = false;
	}
	blurtime = new Date().valueOf();
};
```

同时本页面也嵌入了这个代码，按下`F12`进入控制台即可看到输出。

<script>console.log('加载成功，开始监听网页失焦');let blurtime=null;let focustime=null;let isFirst=true;window.onfocus=function(){focustime=new Date().valueOf();let second=(focustime-blurtime)/1000;second=Math.round((second+Number.EPSILON)*10)/10;if(!isFirst){console.log(`请注意，你失去焦点了！总共离开${second}秒`)}};window.onblur=function(){if(isFirst){isFirst=false}blurtime=new Date().valueOf()};</script>