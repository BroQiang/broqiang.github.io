---
layout: post
title: 'Ubuntu 16.10 安装后的设置'
date: '2017-04-15'
header-img: "img/post-bg-unix.jpg"
tags:
     - OS
     - Ubuntu
     - Linux
author: 'Bro Qiang'
---

## 安装后的系统设置

## 基本操作

- 打开终端

    终端是用来执行命令，`Ctrl+Alt+t`（快捷键）可以快速打开

    后面的所有命令都是在此工具下输入，就不再单独说明

- 系统操作

    点击右上角的齿轮，，此处也可以进行注销，重启，关机，设置等系统设置


## 修改家目录下的中文目录为英文目录

这个设置个人觉得有点……，用Linux基本上都会用终端命令行进行操作，目录为中文有点麻烦，要不停的切换输入法

如果不进行此步设置，后面的操作要对应修改为中文目录

- 打开终端 `Ctrl+Alt+t` （快捷键）

- 输入下面命令

    ```shell
    # 设置当前终端shell的语言为英文
    $ export LANG=en_US
    # 开发更新语音的工具
    $ xdg-user-dirs-gtk-update
    ```

- 在弹出的工具中选择`Update Names`

- 注销

- 注销后再登录，还会出现更新工具，选择保留旧的名称，如果不想下次登录还会出现，选中下方的`下次不要再询问我`


## 安装Vmware Tools

如果是物理机安装，忽略此步

如果是虚拟机安装，你会发现窗口很小，安装此工具，可以进行分辨率的设置，文件和宿主机之间复制等

- 点击菜单栏的VM，选择`安装 VMWare Tools`，桌面会提示，点击安装

- 稍等，会弹出安装光盘内容，复制 `VMWareTools-*.tar.gz`（星处换成实际的版本号） 到桌面,可以安装`Super(Win键)+Ctrl+d`，显示桌面

- `Ctrl+Alt+t`,打开终端，输入下面命令

    ```shell
    # 如果需要输入密码，输入当前登录用户密码即可，此步是为了防止系统自动安装了VMWareTools开源版本，先进行删除
    $ sudo autoremove open-vm-*
    # 进入到桌面目录
    $ cd ~/Desktop
    # 解压缩安装包,星处换成实际的版本号，下面不再单独说明
    $ tar xzvf VMWareTools-*.tar.gz
    $ cd vmware-tools-distrib
    $ sudo ./vmware-install.pl
    # 在提示框输入yes，然后就一路回车，直到安装完成
    $ yes
    # 安装完成后重启系统，VMWareTools生效
    $ sudo reboot
    ```

- 重启后，发现登录系统后窗口变大，安装成功，此时就可以全屏显示了

## 安装Vim

此步骤非必须，推荐安装，vim比默认的vi多了语法高亮等高级功能

`$ sudo apt install -y vim`

## 禁用访客用户

此步骤非必须，只是登录界面的时候有个guest用，个人不喜欢

物理机安装推荐去掉，防止别人没有用户名密码登录系统

- **16.04** 中修改

    `Ctrl+Alt+t`,打开终端，输入下面命令

    `$ sudo vim /usr/share/lightdm/lightdm.conf.d/50-no-guest.conf`

    写入

    ```shell
    [SeatDefaults]
    allow-guest=false
    ```

**16.10** 中修改

`$ sudo vim /usr/share/lightdm/lightdm.conf.d/50-guest-wrapper.conf`

修改

```shell
[Seat:*]
allow-guest=false
```

*修改完重复系统后生效*

## 安装Gnome桌面

此步骤非必须，如果喜欢Ubuntu的默认桌面可以忽略此步骤

- 安装

    ```shell
    $ sudo apt install -y ubuntu-gnome-desktop
    ```

- 会弹出选择桌面的管理服务，选择lightdm（默认）即可

- 安装完成后注销系统重新登录，登录的时候选择用户名右侧的按钮，选择Gnome即可切换到Gnome桌面


## 安装numix主题

- 安装主题

    `$ sudo apt install numix-*`

    此命令可以装numix主题和numix蓝色主题还有numix图标

- 配置主题

    `$ gnome-tweak-tool`

    通过此工具选择numix主题和图标，还可以用此工具进行一些其他的桌面优化，不再详细说明

## 安装google浏览器

做开发调试个人比较喜欢chrome浏览器，而且有的时候也需要开启多个浏览器做测试，一个Firefox也不够

- 开源版的chromium

    `$ sudo apt install chromium-browser -y`

- chrome

    直接到官网下载Deb包安装即可,如果因为墙打不开，可以配置个hosts文件， [方法](https://laod.cn/hosts/2017-google-hosts.html)

    或者到我的git仓库中下载 [地址](https://git.oschina.net/BroQiang/software)

    下载完成后可以找到安装包直接双击安装，也可以命令行安装(比较快)

    ```shell
    $ cd ~/Downloads
    $ sudo dpkg -i google-chrome-stable_current_amd64.deb
    # 会提示错误，因为缺少依赖关系，执行下面命令安装依赖
    $ sudo apt install -f -y
    # 然后再次安装
    $ sudo dpkg -i google-chrome-stable_current_amd64.deb
    ```

    快捷键`Alt+F2`,输入`google-chrome`,就可以打开chrome浏览器了


## 安装Roboto Mono(google)字体

此步骤非必须，建议安装，后面的配置都会基于此字体，当然如果喜欢其他字体可以根据个人喜好去安装

下载地址: [https://fonts.google.com/specimen/Roboto+Mono](https://fonts.google.com/specimen/Roboto+Mono)

下载完成后,将字体包解压到系统字体目录

```shell
sudo unzip Roboto_Mono.zip -d /usr/share/fonts/
```

## 安装搜狗输入法

- 到官网下载Deb包 [下载](http://pinyin.sogou.com/linux/)

- 安装
    ```shell
    $ cd ~/Downloads
    $ sudo dpkg -i sogoupinyin_2.1.0.0082_amd64.deb
    # 会提示错误，因为缺少依赖关系，执行下面命令安装依赖
    $ sudo apt install -f -y
    # 然后再次安装
    $ sudo dpkg -i sogoupinyin_2.1.0.0082_amd64.deb
    ```

- Gnome要重启生效，Ubuntu桌面应该不用吧（没测试过，不生效也重启下)

- 左下角有个箭头，点开就可以进行配置了



## 设置快捷键

可以根据个人需要设置多个快捷键，此处简单说明下怎么设置

- 打开设置界面，可以右上角进行，也可以`Super(Win键)`，在列表中找到

- 选择键盘

- 设置显示桌面快捷键

    - 导航

    - 找到隐藏所有正常桌面

    - 将默认的`Ctrl+Super+D`->改成`Super+D(和Windows相同，用习惯了)`

- 自定义显示主文件夹（类似windows的我的电脑）

    - 自定义快捷键，右侧的+号添加

    - 名称，随意，如：文件

    - 命令，填入 `nautilus`

    - 添加

    - 此时还是禁用的，还需要将禁用修改成指定的快捷键，如`Super+E` （和Windows一样)

介绍两种方式，剩下的可以根据需要自行设置了



## 修改默认sh 将dash改为bash

此步骤非必须，只是个人习惯了bash shell的脚本语法，不修改自己写的脚本有可能会出错

```shell
$ sudo dpkg-reconfigure dash
```

选择否

## 禁用一般用户，如mysql/www等

此步骤非必须，在有需要的时候再配置，一般情况下忽略即可

在 `/var/lib/AccountsService/users` 目录下,创建和用户名相容的文件,如

`$ sudo vim /var/lib/AccountsService/users/mysql`

写入
```shell
[User]
SystemAccount=true
```

*配置完重启系统后生效*
