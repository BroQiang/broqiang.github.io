---
layout: post
title: 'Sublime 支持中文输入'
date: '2017-02-05'
header-img: "img/post-bg-unix.jpg"
tags:
     - Editor
     - Sublime
author: 'Bro Qiang'
---

> Sublime 天生不支持中文输入, 没办法, 用了很久, 太习惯了, 想办法解决这个问题吧

## 方法一, 对Sublime 做 hack

这个比较复杂, 不过用起来方便,就有偶尔会崩溃

[Github地址](https://github.com/lyfeyaj/sublime-text-imfix)

## 方法二, 安装 Inputer3 插件

此方法也不太优雅,会弹出一个输入框,将中文输入在这个框里面，全屏时有时会失去焦点

[Github地址](https://github.com/lanky228/Inputer3)

## 方法三，安装 InputHelper 插件

也不优雅，需要弹出个输入框，不过别的问题没有，我现在用的就是这个

#### 安装插件

通过包控制器找到 `InputHelper` 直接安装即可

#### 修改源代码

默认看不到源代码，可以通过 `PackageResourceViewer` 插件生成

- 安装 `PackageResourceViewer`

- 通过 `PackageResourceViewer` 生成模板配置文件

    输入 `PackageResourceVIewer: Extract Package`

    输入 `InputHelper`

    现在就可以看到源码了，接着我们去直接修改就可以了

- 修改快捷键

    它默认的快捷键是 `Ctrl+Shift+z` ，我不习惯，我将他修改成了 Ctrl+空格，使用的时候连续输入两次空格就可以输入中文了

    `vim ~/.config/sublime-text-3/Packages/InputHelper/Default\ \(Linux\).sublime-keymap`

    将 `{ "keys": ["ctrl+shift+z"], "command": "input_helper" }`

    替换成 `{ "keys": ["ctrl+space"], "command": "input_helper" }`

- 修改填出框的长度，默认的有点短，字输入的多了就看不全了

    `vim ~/.config/sublime-text-3/Packages/InputHelper/lib/linux_text_input_gui.py`

    找到 `window.set_default_size(300, 60)`

    改成 `window.set_default_size(600, 60)` 这个长度就看个人喜好了

- 给 `linux_text_input_gui.py` 添加可以执行权限

    如果不添加权限输入框也不会弹出，如果是git clone 的安装包就不需要了，默认就有权限了

    `chmod +x ~/.config/sublime-text-3/Packages/InputHelper/lib/linux_text_input_gui.py`

#### 安装 python gtk2  包

这个插件依赖这个包，如果系统中没有就要安装，否则也是不能使用

```shell
# Ubuntu 
$ sudo apt install -y python-gtk2-dev

# Fedora 
# $ sudo dnf install -y pygtk2
```


好了，现在将Sublime 重启下，看看是不是就可以用了




    


