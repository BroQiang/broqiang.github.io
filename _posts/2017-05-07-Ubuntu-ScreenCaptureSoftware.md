---
layout: post
title: 'Ubuntu 下的录屏软件 kazam'
date: '2017-05-07'
header-img: "img/post-bg-unix.jpg"
tags:
     - Ubuntu
author: 'Bro Qiang'
---

# Ubuntu 下的录屏软件

软件有很多，不过个人觉得 kazam 用起来最顺手

## 软件安装

```shell
sudo apt-get install kazam
```

## 使用

快捷键 `Alt+F2` 输入 `kazam` 即可打开软件

## 快捷键

-- 开始录 - `Win+R`

-- 暂停 - `Win+P`

-- 结束保存 - `Win+F`

## 麦克风杂音很大处理

使用 alsamixer 工具

```shell
$ sudo alsamixer
```

将里面的配置，红色的全都改成绿色即可，不过我的改完之后麦克声音特别小，不清楚是Ubuntu支持的不好，还是麦克太差了……