---
layout: post
title: 'Fedora 开发环境配置'
date: '2017-07-29'
header-img: "img/post-bg-unix.jpg"
tags:
     - Linux
author: 'Bro Qiang'
---

因为将开发环境从 Ubuntu 换到了 Fedora ，所以在使用的时候将配置过程记录下来，方便自己下次配置，如果你正好看到此文档，也可以参考下，因为本人是做 PHP 开发，所以此博客中的文档全部是以 Linux 下 PHP 开发为主导写的。

## 更新默认的目录名称

因为默认家目录下的自动的几个目录全都是中文，命令行访问的时候总是要切换输入法，不太方便。
所以把他全部都改成英文的，打开终端，输入下面命令。

```bash
export LANG=en_US.UTF-8
xdg-user-dirs-gtk-update
```

在弹出的窗口选择更新

## 先将系统更新到最新

更新系统，更新完成后将系统重启

```bash
sudo dnf -y update
sudo reboot
```

更新后重启，然后将旧的内核删除，看个人喜好，不删除也不影响使用，只是稍微会多占一点磁盘空间。

```bash
# 版本号根据 rpm -qa 去查询旧的内核版本
sudo rpm -qa | grep kernel | grep core-4.11.8 | xargs sudo dnf remove -y
```

## 关闭 SELinux

```bash
sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
```

## 安装 vim、numix主题、gnome配置工具

```bash
sudo dnf -y install vim numix-* gnome-tweak-tool
```

vim 环境变量

```bash
:set nu
:set tabstop=4
:set expandtab
:set autoindent
:set shiftwidth=4
:set smartindent
```

## 配置桌面环境
```bash
gnome-tweak-tool
```
可以配置主题、桌面、窗口最大化最小化按钮等，根据实际情况去配置。

Update theme to numix ...

## 配置快捷键

根据个人喜好去配置，输入下面命令，在设置的界面找到键盘，配置对应的快捷键即可。

```bash
gnome-control-center
```
- `Win+D` - 显示/隐藏桌面（默认是禁用的，启用配置快捷键即可）

- `Win+E` - 打开文件管理器（自定义快捷键）

- `Ctrl+Alt+T` - 打开终端（自定义快捷键）


## 配置中文输入法

自己手动下载 sogoupinyin 的 rpm 包（也是上面的源中的，下载的 Fedora27 的 rpm 包，也是可以用的）安装，需要下载两个包。

如果是其他版本，可以去 [仓库列表](https://repo.fdzh.org/FZUG/free) 中查看

```bash
wget https://repo.fdzh.org/FZUG/free/27/x86_64/sogoupinyin-2.1.0.0086-2.fc27.x86_64.rpm
wget https://repo.fdzh.org/FZUG/free/27/x86_64/noarch/sogoupinyin-selinux-2.1.0.0086-2.fc27.noarch.rpm
# 将上面的两个包安装
sudo dnf install -y sogoupinyin-*
```


## 安装开源字体

安装几个 wqy 的字体，留着备用。

```bash
sudo dnf install -y wqy-*
```

## 安装 lantern

[下载地址](https://github.com/getlantern/lantern/releases)

可以找出最新版本下载，如现在最新的是 4.4.1 就下载 `update_linux_amd64.bz2`

安装及使用

```bash
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

```bash
cd ~/Downloads
sudo dnf install google-chrome-stable_current_x86_64.rpm
```

## 解决 chrome 浏览器打开是一个黑框

```bash
# 将 #WaylandEnable=false 的注释取消
sudo sed -i 's/#WaylandEnable=false/WaylandEnable=false/' /etc/gdm/custom.conf
```

上面的配置需要重启系统才可以生效。


## 安装 Sublime Text

这个看个人喜好，个人比较喜欢使用 Sublime 来写代码，可以通过下面方式安装，关于主题插件等，可以参考本博客中的关于 Sublime 的专门的文档

```bash
# 配置安装源
sudo dnf config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo
# 安装软件
sudo dnf install -y sublime-text
```

## 配置常用别名

这个根据个人喜好

```bash
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





























