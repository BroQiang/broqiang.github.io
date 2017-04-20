---
layout: post
title: 'Ubuntu 下最好用的截图工具'
date: '2017-04-20'
header-img: "img/post-bg-unix.jpg"
tags:
     - Ubuntu
author: 'Bro Qiang'
---

## Ubuntu 下最好用的截图工具

Ubuntu 系统自带的截图工具就不推荐了, 功能有点弱,不过用起来也算方便

推荐使用下面两款截图工具


### Shutter 安装

这个是最强大的, 不过用起来有点笨重, 操作步骤较多

Ubuntu 的软件源中就包含了, 直接安装就可以了

```shell
$ sudo apt install shutter
```


### Deepin-scrot

这个是深度出品的,用起来和QQ截图很像,比较方便

安装

```shell
# 下载 Deb 包
$ wget http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-scrot/deepin-scrot_2.0-0deepin_all.deb

# 安装
$ sudo dpki -i install deepin-scrot_2.0-0deepin_all.deb

# 安装依赖, 一般会提示安装失败,缺少依赖关系, 需要 python-xlib ,直接用下面命令即可
$ sudo apt install -f

# 安装完依赖再安装一次 
$ sudo dpki -i install deepin-scrot_2.0-0deepin_all.deb

# 试用, 会弹出截图界面,和 QQ截图那种工具很像, 使用方式也基本相同, 后面有快捷键配置方法
$ deepin-scrot
```

其他版本 Linux 可以查看 [Github 源码](https://github.com/linuxdeepin-packages/deepin-scrot.git) 进行尝试, 未测试


### 快捷键配置

- 打开设置界面

    - 方法1 - 快捷键 `Alt+F2` 输入 `gnome-control-center`

    - 方法2 - 点击右上角的菜单, 在里面找到设置的选项

- 选择键盘

- 选中左侧的自定义快捷键,点击右侧的 `+` 号按钮

- 输入名称 Screenshot (随意,只是名字)

- 输入命令

    - Shutter - `shutter -f` 全屏 或 `shutter -s` 鼠标选择区域

    - 深度截图 - `deepin-scrot`

- 设置快捷键 - 默认新建的是没有快捷键的, 鼠标点中命令右侧的禁用, 输入快捷键即可, 如: `Ctrl+Alt+A`

如果两种方式都要使用的话,就自定义两个快捷键即可

