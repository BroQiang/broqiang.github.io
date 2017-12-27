---
layout: post
title: 'Ubuntu 禁用IPv6'
date: '2017-12-27'
header-img: "img/post-bg-unix.jpg"
tags:
     - Linux
author: 'Bro Qiang'
---

# Ubuntu 禁用IPv6

应该 Ubuntu 的附近版本都可以吧，实测的是 Ubuntu 17.10

```shell
sudo vim /etc/default/grub
# 找到下面内容
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
# 讲上面内容替换成
GRUB_CMDLINE_LINUX_DEFAULT="ipv6.disable=1 quiet splash"

# 更新
sudo update-grub

# 重启后生效
reboot
```

这个方法可以真正的禁用 IPv6，不过应该是每次内核升级后都要自己配置一次，不过也还好，内核升级的频率也没有那么高。

