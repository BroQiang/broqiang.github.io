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

### 源码编译安装

如果想安装官方最新版本，可以用源码编译安装

下面的方法支持CentOS和Ubuntu，区别只是依赖关系的安装方式不同，其他全部相同

```shell
# CentOS 安装依赖关系 
$ sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel  perl-ExtUtils-MakeMaker

# Ubuntu 安装依赖关系
# sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev

# 下载解压
$ wget https://www.kernel.org/pub/software/scm/git/git-2.9.4.tar.gz

$ sudo tar xzvf git-2.9.4.tar.gz -C /usr/local/src/
$ cd /usr/local/src/git-2.9.4

# 配置及安装
$ sudo ./configure --prefix=/usr/local/git
$ sudo make
$ sudo make install
```


## 配置环境变量

```shell
$ sudo vim /etc/profile.d/git.sh
# 写入
export GIT_HOME=/usr/local/git
export PATH=$GIT_HOME/bin:$PATH

# 生效下
$ source /etc/profile.d/git.sh
```

## 安装完成后测试

```shell
$ git --version
```

全部打印出版本信息，安装完成

## 配置账号

安装完成后最好配置下用户和邮箱，否则commit的时候也无法提交

全局配置

```shell
# 邮箱改成实际的
$ git config --global user.email "broqiang@qq.com"

# 用户名改成实际的
$ git config --global user.name "Bro Qiang"

```

## 配置记住用户名密码

比如提交 github ，如果不记住，每次都要输一次，个人电脑，还是记住比较方便

```shell
# 长期保存, 一般要是个人开发电脑，配置这个就行
$ git config --global credential.helper store

# 临时保存，默认15分钟
$ git config --global credential.helper cache

# 指定临时保存时间
$ git config credential.helper 'cache --timeout=3600'
```



## 更新日志

- 2017-06-11 更正书写错误

- 2017-05-25 更新到当前最新版本 `2.9.4`