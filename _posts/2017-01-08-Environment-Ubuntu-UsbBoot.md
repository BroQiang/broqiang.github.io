---
layout: post
title: 'Ubuntu 16.10 USB 引导盘制作'
date: '2017-01-08'
header-img: "img/post-bg-unix.jpg"
tags:
    - Environment
    - Ubuntu
    - Linux
author: 'Bro Qiang'
---

## 获取 Linux 镜像文件

要想制作 启动盘，需要现有操作系统的安装镜像文件
#### Fedora

可以直接去官方网站下载，如果速度慢的话可以采用国内的镜像，比如 163开源、阿里云等。

- [Fedora 官方下载地址](https://getfedora.org/zh_CN/workstation/download)

- [163 开源镜像下载](http://mirrors.163.com/fedora/releases/27/Workstation/x86_64/iso/Fedora-Workstation-Live-x86_64-27-1.6.iso)

#### Ubuntu

- [Ubuntu 官网下载](http://cn.ubuntu.com/download/)

- [163 开源镜像下载](http://mirrors.163.com/ubuntu-releases/17.10.1/ubuntu-17.10.1-desktop-amd64.iso)

#### CentOS

- [CentOS 官方镜像列表](https://centos.org/download/mirrors) 可以从里面找到一个喜欢的下载，注意选择 `China`

- [清华大学开源镜像下载](https://mirrors.tuna.tsinghua.edu.cn/centos/7.4.1708/isos/x86_64/CentOS-7-x86_64-DVD-1708.iso)


## 通用工具

可以使用 [unetbootin](http://unetbootin.github.io/) ,这个软件直接 `Linux` `Windows` `macOS` 客户端，详细使用方法见 [官方文档](https://unetbootin.github.io/)

- [下载ubuntu-16.10（64位）](http://releases.ubuntu.com/16.10/ubuntu-16.10-desktop-amd64.iso)


## Fedora 安装工具

Fedora 官方提供了 [Fedora Media Writer](https://github.com/MartinBriza/MediaWriter) 安装工具，可以下载安装工具，直接安装就可以了。工具是图形界面的，很容易就可以看明白怎么使用，也可以查看 [官方文档](https://docs.fedoraproject.org/f27/install-guide/install/Preparing_for_Installation.html) 查看使用方法

#### Windows 系统中制作启动盘

下载 [FedoraMediaWriter Windows 版本](https://github.com/MartinBriza/MediaWriter/releases/download/4.1.1/FedoraMediaWriter-win32-4.1.1.exe) 直接安装使用即可。

#### Fedora 中制作启动盘

```bash
# 安装
sudo dnf install mediawriter
# 使用
mediawriter
```
然后在图形界面中去操作启动盘制作即可。


## Ubuntu 安装工具

#### 

官方推荐 `rufus` ，当然这个工具也可以用来安装其他发行版本的 Linux，直接 [下载](https://rufus.akeo.ie/downloads/rufus-2.18.exe) 安装使用就可以，图形界面工具，可以很容易就看明白怎么使用，如果看不明白的话，可以查看 [官方文档](https://rufus.akeo.ie/?locale=zh_CN)

#### Ubuntu 中制作启动盘

在 Ubuntu 系统中制作启动盘很容易，可以直接找到 `usb-creator-gtk` 即可，这个是系统自带的。

**打开方式：**

- 快捷键 `Alt+F2` 输入 `usb-creator-gtk` 可以打开工具

- 菜单中直接搜索 `usb-creator-gtk` 或者找到 `启动盘创建器` 也可以打开工具