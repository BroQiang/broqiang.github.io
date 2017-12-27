---
layout: post
title: 'Ubuntu 开发环境配置'
date: '2017-12-27'
header-img: "img/post-bg-unix.jpg"
tags:
     - Linux
author: 'Bro Qiang'
---

# Ubuntu 开发环境配置

> 版本 17.10 64 位（ubuntu-17.10-desktop-amd64.iso）

## 安装操作系统

这里不太多的赘述，基本上就是下一步下一步就可以了，每一个地方点击下一步之前注意看一下即可。

系统安装完成后，可以通过 `Ctrl+Alt+T` 打开终端，后面所有的命令都在终端中执行。

## 安装 VMTools

如果是虚拟机安装的操作系统就安装下这个，如果是物理机安装可以跳过这步。

```shell
sudo apt install open-vm-tools-desktop -y
```

安装完成后，就可以随便调整桌面的大小，并且可以和物理机之间复制文件和剪切板，如果不能生效，可以将当前登录的桌面注销或者重启操作系统。

## 更改家目录为英文

```shell
LANG=en_US
xdg-user-dirs-gtk-update
```
然后点击填出界面右下角的 `Update Names`

## 去除不必要的软件

这一步不是必须的，个人觉得这样可以减少一些磁盘空间，并且在更新操作系统的时候可以不更新那些用不到的包，可以节省一些时间。

```shell
sudo apt autoremove libreoffice-* ibus -y
```

## 安装需要的软件包

包括：主题、图标、vim、numix-icon-theme等

```shell
# 添加 Ubuntu Kylin 源，配置了这个源之后可以安装更多的软件，如：搜狗拼音
echo -e "deb http://archive.ubuntukylin.com:10006/ubuntukylin trusty main" | \
sudo tee /etc/apt/sources.list.d/ubuntu-kylin
# 添加公钥，如果失败了可以多尝试几次，因为公钥服务器的网络不稳定
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D259B7555E1D3C58

# 更新源
sudo apt Update

# 安装软件
sudo apt install -y gnome-tweak-tool arc-theme numix-icon-theme vim \
gnome-icon-theme sogoupinyin wps-office git net-tools shutter kazam \
ttf-wqy-microhei
```

## 更新操作系统到最新

```shell
sudo apt upgrade -y
# 更新完成后重启操作系统
reboot
```

重启后登录桌面的时候选择 `Ubuntu on xorg` 启动，不要选择默认，因为现在很多软件不支持 `Wayland`

更新系统后，会出现两个内核，可以通过下面方式删除旧的内核
```shell
# 查询出当前系统中的内核
sudo dpkg -l | grep kernel
# 用眼睛找到版本老的版本，然后将包名复制删除即可
sudo dpkg -l | grep kernel | grep 4.13.0-16.19 | awk '{print $2}' | xargs sudo apt autoremove -y
```

## 配置主题

这个看个人爱好，区别只是美观，我使用的是 arc-theme 和 Numix 的图标，上面安装软件的时候已经安装。

快捷键 `Alt+F2` 在窗口中输入 `gnome-tweak-tool`，然后就按照喜好去配置就可以了。

## 设置快捷键

#### 系统快捷键

打开设置

- 右上角菜单点进设置界面

- 快捷键 `Alt+F2` 输入 `gnome-control-center`

左侧菜单找到`设备`->`键盘` ，在右侧设置快捷键，也可以在最下面点击 `+ 号` ，自定义快捷键。

#### 设置 gnome-terminal （终端）快捷键
因为这个使用频率非常的高，以前使用 xshell 习惯了全屏 Alt+Enter，所以这个也改成这个。

菜单上的`编辑`->`首选项`->`快捷键` ，然后根据需要去配置就可以了。

## 配置搜狗输入法

前面已经安装了，如果没装用下面命令安装即可，不过需要注意，要配置 ubuntukylin 源。

```shell
sudo apt install sogoupinyin
```
打开`设置`界面->`区域和语言`->`Manage Installed Languages`

在弹出界面选择 fcitx，然后通过 `Ctrl+空格` 就可以切换输入法。

## 配置 git

软件已经在前面 apt install 的时候安装，下面进行一些简单的配置

```shell
# 提交数据的时候的用户邮箱和用户名
git config --global user.email "broqiang@qq.com"
git config --global user.name "Bro Qiang"
# 保存密码
git config --global credential.helper store

# 配置 git 别名
echo -e "\nalias gs='git status'\nalias gaa='git add .'\nalias ga='git add '\nalias gp='git push'\nalias gc='git commit -m '\nalias gl='git log'\nalias grao='git remote add origin '\nalias gpo='git push origin '" >> ~/.bash_aliases
```

## 配置vim

```shell
echo -e ":set nu\n:set tabstop=4\n:set expandtab\n:set autoindent\n:set shiftwidth=4\n:set smartindent" > ~/.vimrc
```
# 安装 lantern

```shell
# 下载
wget https://raw.githubusercontent.com/getlantern/lantern-binaries/master/lantern-installer-64-bit.deb

# 安装
sudo dpkg -i lantern-installer-64-bit.deb

# 如果提示需要依赖关系，执行下面命令
sudo apt install -f
```

## 安装 Sublime
下面的是一个已经按照我的习惯配置好了的 Sublime，更多配置参考 ：
[http://broqiang.com](http://broqiang.com)

- [Github仓库](https://github.com/BroQiang/Software_Sublime.git)

- [码云仓库](https://gitee.com/BroQiang/Software_Sublime.git)

```shell
git clone https://github.com/BroQiang/Software_Sublime.git
```

## 安装 Atom

具体步骤：

- [Github仓库](https://github.com/BroQiang/Software_Atom.git)

- [码云仓库](https://gitee.com/BroQiang/Software_Atom.git)

## 安装 chrome 浏览器

直接去官网安装下载安装即可，如果打不开确定下前面的 alntern 是否安装

[chrome浏览器官方下载地址](https://www.google.cn/intl/zh-CN/chrome/browser/desktop)

```shell
# 安装软件包
sudo dpkg -i google-chrome-stable_current_amd64.deb
# 解决依赖关系
sudo apt install -f
```

使用，直接 `Alt+F2` 输入 `google-chrome`

## 安装 Navicat

下载地址： [https://gitee.com/BroQiang/Software_Navicat.git](https://gitee.com/BroQiang/Software_Navicat.git)

里面有详细的安装步骤

安装完成可以配置一个启动脚本，方便快速启动
```shell
echo -e "/opt/navicat112_Premium_cs_x64/start_navicat" > ~/bin/navicat
chmod +x ~/bin/navicat
```

使用，可以直接在终端或者 `Alt+F2` 输入 `navicat` 就可以运行了。

## 配置截图工具

在 Ubuntu 下没有什么太好用的截图工具，尝试了几个之后，确定为 `shutter`，这个工具很强大，说它不好用是因为它太重了，有点不够灵巧，功能有点太多了。

使用方法，可以直接通过 `shutter`命令来截图，并可以通过系统设置，给截图命令配置快捷键，方便快速使用截图。

- `shutter -s` 区域截图

- `shutter -f` 全屏截图

- `shutter -m` 截取菜单（一般工具没法截取右键菜单，这个很强大）

## 配置录屏工具

这里使用的是 `kazam` ，在前面已经安装了，如果没有安装再安装一下

#### 快捷键
- 开始录 - `Supper+Ctrl+R`

- 暂停 - `Supper+Ctrl+P`

- 结束保存 - `Supper+Ctrl+F`


## 配置WPS

前面已经安装了，如果想安装最新版本或者 wps 不能启动，请看 [github](https://github.com/BroQiang/Software_WPS)

## 配置 MySQL PHP Nginx 环境

可以使用 [自动安装脚本](https://github.com/BroQiang/lnmp)，自动安装环境，使用的时候注意下 config 文件中的配置，如：操作系统版本、用户等。

如果想要手动配置，请参考(注意下安装顺序，建议按照下面的顺序安装)：

- [MySQL](http://broqiang.com/2017/04/18/Mysql-Install-5.7.18-Linux-Compile/)

- [PHP](http://broqiang.com/2017/04/18/PHP-Install-7.1.4-Linux-Compile/)

- [Nginx](http://broqiang.com/2017/04/18/Nginx-Install-1.12-Linux/)
