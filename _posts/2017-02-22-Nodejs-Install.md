---
layout: post
title: 'Linux 安装 Node.js'
date: '2017-02-22'
header-img: "img/post-bg-unix.jpg"
tags:
    - Nodejs
author: 'Bro Qiang'
---


### 获取软件

下载地址：　[https://nodejs.org/dist/v7.7.1/node-v7.7.1-linux-x64.tar.xz](https://nodejs.org/dist/v7.7.1/node-v7.7.1-linux-x64.tar.xz)

`$ wget https://nodejs.org/dist/v7.7.1/node-v7.7.1-linux-x64.tar.xz`

### 安装

```shell
$ sudo tar xvf node-v7.7.1-linux-x64.tar.xz
$ sudo mv node-v7.7.1-linux-x64 /usr/local/node
```

### 配置环境变量

`$ sudo vim /etc/profile.d/node.sh`

写入

```shell
#!/bin/bash
export NODE_PATH=/usr/local/node
export PATH=$PATH:$NODE_PATH/bin
```

### 配置支持淘宝镜像

写入别名
```shell
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
```
