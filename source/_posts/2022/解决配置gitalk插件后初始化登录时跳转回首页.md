---
title: 解决配置gitalk插件后初始化登录时跳转回首页
categories:
  - 开发日记
abbrlink: a7bfe54a
date: 2022-03-14 19:52:51
cover: hub.jpg
---

# 起源

在参考了一些列博文配置了gitalk插件后，一直不能正常登录。具体表现为点击登录后直接跳转到了博客首页，搞的一头雾水，不明所以。

# 分析

在登录时，打开F12跟踪network访问记录，发现有一个是github认证授权的请求，另外有两个是重定向到首页的请求：

一个是跳转到`http://lition.online`的，另一个是跳转到`https://lition.online`的

![](redirect.png)

结合参考文章和以上分析可知，授权请求中的参数`redirect_uri`的域名必须与Github的`OAuth Apps`中配置的`Authorization callback URL`相同，否则就会重定向到这个`Authorization callback URL`，而我这里配置的就是博客首页地址`http://lition.online`，但是跳转后需要https连接，所以又会重定向

回头看一下授权请求中携带的`redirect_uri`参数的域名，竟然是`http://lition.online`！

# 解决

果断将`OAuth Apps`中的`Authorization`callback URL设置为`https://lition.online`，重新打开博客进行登录授权，成功登陆。

如果你仔细观察的时候，你会发现跳向博客首页的时候，地址栏链接变的很复杂，都是些什么东西呢，我们不妨解析一下

```
https://lition.online/?
error=redirect_uri_mismatch&
error_description=The+redirect_uri+MUST+match+the+registered+callback+URL+for+this+application.&
error_uri=https://developer.github.com/apps/managing-oauth-apps/troubleshooting-authorization-request-errors/#redirect-uri-mismatch

//真是贴心啊，错误原因，和参考文档地址全都给了
```


# 参考
 - https://blog.csdn.net/qq_39195042/article/details/86135917