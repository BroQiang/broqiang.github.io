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
export LANG=en_US.UTF-8
xdg-user-dirs-gtk-update
```

在弹出的窗口选择更新

## 先将系统更新到最新

更新系统，更新完成后将系统重启

```shell
sudo dnf -y update

sudo reboot
```

更新后重启，然后将旧的内核删除，看个人喜好，不删除也不影响使用，只是稍微会多占一点磁盘空间。

```shell
# 版本号根据 rpm -qa 去查询旧的内核版本
sudo rpm -qa | grep kernel | grep core-4.11.8 | xargs sudo dnf remove -y
```

## 关闭 SELinux

```shell
sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
```

## 安装 vim、numix主题、gnome配置工具

```shell
sudo dnf -y install vim numix-* gnome-tweak-tool
```

vim 环境变量

```shell
:set nu
:set tabstop=4
:set expandtab
:set autoindent
:set shiftwidth=4
:set smartindent
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
- `Win+D` - 显示/隐藏桌面（默认是禁用的，启用配置快捷键即可）

- `Win+E` - 打开文件管理器（自定义快捷键）

- `Ctrl+Alt+T` - 打开终端（自定义快捷键）


## 配置中文输入法

默认是没有中文输入法，可以选择 `设置` -> `区域和语言` -> `添加输入源` -> `中文拼音`

~~因为fedora下搜狗拼音各种崩溃，又没有好的办法解决，所以就不再使用，现在的默认中文也可以凑合使用，下面内容废弃，个人已经不在使用，有兴趣的可以参考，这个是以前版本的配置。~~

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
ps aux | grep sogou-qimpanel | grep -v grep | awk '{print $2}' | xargs kill -9
ps axu | grep 'fcitx -D' | grep -v grep | awk '{print $2}' | xargs kill -9
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

## 安装开源字体

安装几个 wqy 的字体，留着备用。

```shell
sudo dnf install -y wqy-*
```

## 安装 lantern

[下载地址](https://github.com/getlantern/lantern/releases)

可以找出最新版本下载，如现在最新的是 3.7.4 就下载 `update_linux_amd64.bz2`

安装及使用

```shell
# 安装以来关系
sudo dnf install -y libappindicator-gtk3

# 解压安装包
bzip -d update_linux_amd64.bz2

# 创建家目录下的 bin 目录，并将软件复制过去
mkdir ~/bin && mv update_linux_amd64 ~/bin/lantern
```

使用，直接快捷键 `Alt+F2` 输入 `lantern`


## 安装 chrome 浏览器

看个人喜好，默认的火狐浏览器也很强大，不过个人喜欢用 chrome 浏览器，而且开发测试的时候会用到多个浏览器，所以就安装上了。

[下载 chrome 浏览器](https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm) ，下载好了之后直接 通过 dnf 安装就可以了

```shell
cd ~/Downloads
sudo dnf install google-chrome-stable_current_x86_64.rpm
```

## 解决 chrome 浏览器打开是一个黑框

```shell
# 将 #WaylandEnable=false 的注释取消
sudo sed -i 's/#WaylandEnable=false/WaylandEnable=false/' /etc/gdm/custom.conf
```

上面的配置需要重启系统才可以生效。


## 安装 Sublime Text

这个看个人喜好，个人比较喜欢使用 Sublime 来写代码，可以通过下面方式安装，关于主题插件等，可以参考前面关于 Sublime 的专门的文档

```shell
# 配置安装源
sudo dnf config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo
# 安装软件
sudo dnf install -y sublime-text
```

## 配置常用别名

这个根据个人喜好

```shell
vim .bash_profile
# 写入下面内容，最好在上一个 fi 后面写
if [ -f ~/.bash_alias ]; then

        . ~/.bash_alias
fi

# 然后将别名内容写入
cat > .bash_alias << EOF

#在提示符下，写入下面内容
# git
alias gs='git status'
alias gaa='git add .'
alias ga='git add '
alias gp='git push'
alias gc='git commit -m '
alias gl='git log'
alias grao='git remote add origin '
alias gpo='git push origin '
EOF
```

## 其他配置

可以参考本博客的其他文档，支持搜索，如 输入 Sublime，可以将所有关于 Sublime 的文档全部搜索出来。

如 Nginx PHP Mysql Git，搜索指定的关键字就都可以搜索出来了，PHP 的基本开发环境都可以在本博客找到文档 。

## 更新日志

#### 2017-09-13

更新了一些配置，使得配置更加详细。

#### 2017-07-29

首次安装 Fedora 26 ，更写下本文档，在日志的使用中遇到问题会再次记录





























