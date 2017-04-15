---
layout: post
title: 'Sublime 安装'
date: '2017-02-01'
header-img: "img/post-bg-unix.jpg"
tags:
     - Editor
     - Sublime
author: 'Bro Qiang'
---

# Sublime的安装配置

用过几个编辑器，比如Atom（非常强大，也非常喜欢，尤其是用来写markdown）,不过对不是对PHP不友好，就是对Linux不友好，最后没办法，还是转回了Sublime，在Linux下，他对中文不友好，有个替代方案，凑合用，还好写代码的时候就是表单注释之类的用到中文，不算太多，还能凑合用

### 获取软件

官方下载：　[http://www.sublimetext.com/3](http://www.sublimetext.com/3)


### 安装

- Ubuntu直接下载Deb包
    ```shell
# 可以根据下载的版本去安装，这样就不用管版本了
$sudo dpki -i sublime-text_build*
    ```

- 其他版本，直接解压就可以用了


### 安装包控制器

这个是Sublime的精髓,后面安装的时候都会用到

- 安装

    按快捷键`Ctrl+Shift+p`

    输入 `Install Package Control`

    回车,等待安装成功的提示即可


### 安装字体

推荐Google的`Roboto Mono`字体

- 下载地址: [https://fonts.google.com/specimen/Roboto+Mono](https://fonts.google.com/specimen/Roboto+Mono)

- 下载完直接解压到系统的字体目录即可

    `$ sudo unzip Roboto_Mono.zip -d /usr/share/fonts/Roboto_Mono`

    配置文件中加入`"font_face": "Roboto Mono",`



