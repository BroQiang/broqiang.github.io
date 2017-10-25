---
layout: post
title: 'CentOS 7 禁用 IPv6'
date: '2017-10-25'
header-img: "img/post-bg-unix.jpg"
tags:
     - Linux
author: 'Bro Qiang'
---

# CentOS 7 禁用 IPv6

IPv6现在一般只在高校中推行，一般用来资源共享与下载。所以一般情况下不会用到，如果确定用不到，就可以将其禁用，可以提高一下网络的速度。

## 修改配置文件

编辑 `/etc/default/grub` ，在 `GRUB_CMDLINE_LINUX` 加上的后面句首加上 `ipv6.disable=1` 。

```shell
# 打开配置文件
sudo vim /etc/default/grub
# 将下面内容
GRUB_CMDLINE_LINUX="rd.lvm.lv=centos_fullstack/root rd.lvm.lv=centos_fullstack/swap rhgb quiet"
# 修改成
GRUB_CMDLINE_LINUX="ipv6.disable=1 rd.lvm.lv=centos_fullstack/root rd.lvm.lv=centos_fullstack/swap rhgb quiet"
```

## 重新生成grub.cfg文件

```shell
grub2-mkconfig -o /boot/grub2/grub.cfg
```

配置完成之后重启服务器

```shell
sudo reboot
```

## 查看

```shell
# 查看监听的地质，是不是已经没有了 和 IPv6 相关的都消失了
sudo netstat -tnlp

# 查看 IPv6 模块是否已经没有在内核中加载
sudo lsmod | grep ipv6
```
