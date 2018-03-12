---
layout: post
title: 'Linux 安装 Node.js'
date: '2017-04-19'
header-img: "img/post-bg-unix.jpg"
tags:
    - Nodejs
author: 'Bro Qiang'
---

## 获取软件

[官方下载地址](https://nodejs.org/dist/v8.10.0/node-v8.10.0-linux-x64.tar.xz)

### 安装

```bash
# 下载官方当前最新二进制安装包
wget https://nodejs.org/dist/v8.10.0/node-v8.10.0-linux-x64.tar.xz

# 创建 Node.js 安装目录
sudo mkdir -p /usr/local/node

# 解压到 /usr/local/node
sudo tar xvf node-v8.10.0-linux-x64.tar.xz -C /usr/local/node --strip-components=1
```

### 配置环境变量

```bash
sudo vim /etc/profile.d/node.sh

# 写入下面内容

export NODE_PATH=/usr/local/node
export PATH=$PATH:$NODE_PATH/bin
```

### 配置支持淘宝镜像

写入别名
```bash
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
```