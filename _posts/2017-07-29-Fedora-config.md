---
layout: post
title: 'Fedora 开发环境配置'
date: '2017-07-29'
header-img: "img/post-bg-unix.jpg"
tags:
     - Linux
author: 'Bro Qiang'
---

# Fedora 26 开发环境配置

因为将开发环境从 Ubuntu 换到了 Fedora ，所以在使用的时候将配置过程记录下来，方便自己下次配置，
如果你正好看到此文档，也可以参考下，因为本人是做 PHP 开发，所以此博客中的文档全部是以 Linux 下 PHP 开发为主导写的。

## 更新默认的目录名称

因为默认家目录下的自动的几个目录全都是中文，命令行访问的时候总是要切换输入法，不太方便。
所以把他全部都改成英文的，打开终端，输入下面命令。

```shell
export en_US.UTF-8
xdg-user-dirs-gtk-update
```

在弹出的窗口选择更新


## 安装 vim、numix主题、gnome配置工具

```shell
sudo dnf -y install vim numix-* gnome-tweak-tool
```

## 配置桌面环境
```shell
gnome-tweak-tool
```
可以配置主题、桌面、窗口最大化最小化按钮等，根据实际情况去配置。

Update theme to numix ... 

## 配置快捷键

根据个人喜好去配置，输入下面命令，在设置的界面找到键盘，配置对应的快捷键即可。

```shell
gnome-control-center
```

- `Win+E` - 打开文件管理器

- `Win+D` - 显示/隐藏桌面
  
- `Ctrl+Alt+T` - 打开终端

## 更新系统到最新hanchu1  
```shell
sudo dnf update -y
```

更新后重启，然后将旧的内核删除，看个人喜好，不删除也不影响使用，只是稍微会多占一点磁盘空间。

```shell
# 版本号根据 rpm -qa 去查询旧的内核版本
sudo rpm -qa | grep kernel | grep core-4.11.8 | xargs sudo dnf remove -y
```

## 安装sogou拼音

默认安装完没有中文输入法，个人又喜欢搜狗拼音

原本在 Fedora 25 之前会有中文源，配置上之后直接 `dnf install -y sogoupinyin` 就可以了，不过暂时这个源最高直接到 25 ，
估计 26 发布的时间太短，作者还没来得及更新。

[安装源的配置方法](https://github.com/FZUG/repo/wiki/%E6%B7%BB%E5%8A%A0-FZUG-%E6%BA%90)
（注意：这个需要查看26的源更新了才可以用，否则配置了也没有用）



自己手动下载 sogoupinyin 的 rpm 包（也是上面的源中的，下载的 Fedora25 的 rpm 包，也是可以用的）安装，需要下载两个包。

```shell
wget https://repo.fdzh.org/FZUG/free/25/x86_64/sogsupinyin-2.1.0.0082-2.fc25.x86_64.rpm
wget https://repo.fdzh.org/FZUG/free/25/x86_64/sogoupinyin-selinux-2.1.0.0082-2.fc25.noarch.rpm
# 将上面的两个包安装
sudo dnf install -y sogoupinyin-*
```

不过不知道是什么原因，可能版本不兼容吧（没去研究），偶尔会崩溃，处理方式： 通过 `Ctrl+Alt+F2` 切换到字符界面，输入下面命令

```shell
ps aux | grep sogou-qimpanel | grep -v grep | awk '{print $2}' | xargs kill
ps axu | grep 'fcitx -D' | grep -v grep | awk '{print $2}' | xargs kill
```

懒得去研究到底为什么会出现这个问题了，还好只是偶尔出现，
如果上面命令在字符界面复制不方便，可以在输入法正常的时候将上面内容写成脚本，出问题了切换到字符界面执行一下就可以了。

```shell
mkdir ~/bin
vim ~/bin/restartSogou
```

写入下面内容
```shell
#!/bin/bash
ps aux | grep sogou-qimpanel | grep -v grep | awk '{print $2}' | xargs kill
ps axu | grep 'fcitx -D' | grep -v grep | awk '{print $2}' | xargs kill
```

然后给上 x 权限，下次要用的时候直接用就可以了

```shell
 chmod +x ~/bin/restartSogou
# 直接用就可以了，因为放在 bin 目录下，直接就在 PATH 中了
 restartSogou
```

然后切回到桌面，多按几下 Ctrl+空格就好了

## 安装 Sublime Text

这个看个人喜好，个人比较喜欢使用 Sublime 来写代码，可以通过下面方式安装，关于主题插件等，可以参考前面关于 Sublime 的专门的文档

```shell
# 配置安装源
sudo dnf config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo
# 安装软件
sudo dnf install sublime-text
```


## 安装 chrome 浏览器

看个人喜好，默认的火狐浏览器也很强大，不过个人喜欢用 chrome 浏览器，而且开发测试的时候会用到多个浏览器，所以就安装上了。

直接去官网下载，梯子自己想办法吧，如果不想准备梯子，推荐一个 hosts 的配置方式，到写本文档时仍然好用： [2017 Google hosts](https://laod.cn/hosts/2017-google-hosts.html)

[下载 chrome 浏览器](http://www.google.cn/chrome/browser/desktop/index.html) ，下载好了之后直接 通过 dnf 安装就可以了

```shell
sudo dnf install google-chrome-stable_current_x86_64.rpm 
```

## 解决 chrome 浏览器打开是一个黑框

```shell
sudo vim /etc/gdm/custom.conf
# 将下面的内容
#WaylandEnable=false
# 改成
WaylandEnable=false
```

上面的配置需要重启系统才可以生效。

## 其他配置

可以参考本博客的其他文档，支持搜索，如 输入 Sublime，可以将所有关于 Sublime 的文档全部搜索出来。

如 Nginx PHP Mysql ，搜索指定的关键字就都可以搜索出来了，PHP 的基本开发环境都可以在本博客找到文档 。

## 更新日志

#### 2017-07-29

首次安装 Fedora 26 ，更写下本文档，在日志的使用中遇到问题会再次记录





























