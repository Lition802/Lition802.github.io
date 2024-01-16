---
title: 'Git使用出现git@github.com: Permission denied (publickey). 处理'
tags: 技术
abbrlink: 16394
date: 2024-01-15 02:05:05
---

如果你的电脑只有一个git环境，那么极大多数情况是由于 GitHub 账号没有设置 ssh 公钥信息所致。


# 检查邮箱与用户名
git config --global --list 验证邮箱与GitHub注册时输入的是否一致
```
$ git config --global --list
user.name=xxxxxx
user.email=xxxxxxx@xxx.com
```

# 修改邮箱与用户名

通过git config --global user.name "yourname"，git config --global user.email "email@email.com"（这里得名字和邮箱都是注册github时用的）设置全局用户名和邮箱

# 生成公钥

ssh-keygen -t rsa -C "这里换上你的邮箱"，一路回车，在出现选择时输入Y，再一路回车直到生成密钥。会在/Users/***/路径下生成一个.ssh文件夹，密钥就存储在其中。

[![pFidQN6.md.png](https://s11.ax1x.com/2024/01/15/pFidQN6.md.png)](https://imgse.com/i/pFidQN6)

# 添加公钥

到git仓库，添加秘钥

[![pFidtud.png](https://s11.ax1x.com/2024/01/15/pFidtud.png)](https://imgse.com/i/pFidtud)

[![pFidNDA.md.png](https://s11.ax1x.com/2024/01/15/pFidNDA.md.png)](https://imgse.com/i/pFidNDA)

[![pFidUHI.md.png](https://s11.ax1x.com/2024/01/15/pFidUHI.md.png)](https://imgse.com/i/pFidUHI)

[![pFiddEt.md.png](https://s11.ax1x.com/2024/01/15/pFiddEt.md.png)](https://imgse.com/i/pFiddEt)

# 测试是否添加成功

```
$ ssh -T git@github.com
Hi XXXX! You've successfully authenticated, but GitHub does not provide shell access.
```

即可正常使用。