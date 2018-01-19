---
layout: post
title: 'Linux 关机时自动提交 git'
date: '2017-10-25'
header-img: "img/post-bg-unix.jpg"
tags:
     - PHP
author: 'Bro Qiang'
---

# Linux 关机时自动提交 git

有这个想法，是因为个人比较马虎，经常忘记提交代码，就导致在家中写完的代码第二天回到公司没法继续，导致晚上的工作就白费了，于是就冒出了这个自动提交git的想法。

原理很简单，自己写一个可以自动提交的脚本，在关机之前手动提交一次，最好的办法就是利用 Systemd，在关机的时候自动执行。

## 自动提交git的脚本

