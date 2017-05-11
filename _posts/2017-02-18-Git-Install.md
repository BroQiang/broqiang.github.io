---
layout: post
title: 'Git 安装'
date: '2017-02-18'
header-img: "img/post-bg-unix.jpg"
tags:
    - Git
author: 'Bro Qiang'
---

### 获取最新安装包

git是工具，个人觉得不必过分追求稳定，推荐用最新版本，可以获得最好的体验

[官方下载](https://www.kernel.org/pub/software/scm/git/)

如果下载速度慢的话可以到[我的git仓库 ](https://git.oschina.net/BroQiang/software.git) 下载，不一定是最新的，一般是我正在使用的版本

没有选择具体版本，找到最新版本下载即可，下面示例以当前最新版本进行说明

### Ubuntu安装

Ubuntu比较简单，直接一条命令安装即可

```shell
$ sudo apt install git -y
```

### CentOS安装

因为CentOS是跟随RHEL的版本，为了追求稳定，不会频繁更新内核几软件，一般版本比较低，推荐直接官方下载安装

```shell
# 安装依赖关系
$ sudo yum install zlib-devel perl-ExtUtils-MakeMaker asciidoc xmlto openssl-devel

# 下载解压
$ wget https://www.kernel.org/pub/software/scm/git/git-2.9.3.tar.gz

$ sudo tar xzvf git-2.9.3.tar.gz -C /usr/local/src/
$ cd /usr/local/src/git-2.9.3

# 配置及安装
$ sudo ./configure --prefix=/usr/local/git
$ sudo make
$ sudo make install
```


## 配置环境变量

```shell
$ vim /etc/profile.d/git.sh
# 写入
export GIT_HOME=/usr/local/git
export PATH=$PATH:$GIT_HOME/bin
```

## 安装完成后测试

```shell
$ git --verion
$ npm --version
```

全部打印出版本信息，安装完成
