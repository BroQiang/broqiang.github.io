---
layout: post
title: 'Linux 安装 Composer'
date: '2017-02-21'
header-img: "img/post-bg-unix.jpg"
tags:
    - Composer
    - PHP
author: 'Bro Qiang'
---

## PHP包管理工具

中文官方: [http://www.phpcomposer.com/](http://www.phpcomposer.com/)

网不是很好,下载完最好保留一份

[官网下载地址](https://getcomposer.org/download)

如果下载速度慢的话可以到[我的git仓库 ](https://git.oschina.net/BroQiang/software.git) 下载，不一定是最新的，一般是我正在使用的版本


## 安装

```shell
# 官方下载
$ wget https://getcomposer.org/download/1.5.2/composer.phar -O composer

# 我的码云仓库下载
# $ wget https://git.oschina.net/BroQiang/software/raw/master/composer.phar -O composer

$ chmod +x composer

$ sudo mv composer /usr/local/bin

```

## 配置国内全镜像

因为网络和墙的原因，官方的镜像经常访问不到，导致安装不成功或者很慢，所以配置国内源

现在有两个镜像，随意配置哪个都可以，看个人喜好，一个是 bootcss 组织搞的，
一个是 laravel-china 搞的，都算是比较靠谱的社区

#### packagist.phpcomposer.com 镜像

- 全局（推荐）

    `composer config -g repo.packagist composer https://packagist.phpcomposer.com`

- 修改当前项目

    **进入到项目根目录**

    `composer config repo.packagist composer https://packagist.phpcomposer.com`

#### packagist.laravel-china.org 镜像

[官网](https://laravel-china.org/composer)

- 全局（推荐）

    `composer config -g repo.packagist composer packagist.laravel-china.org`

- 修改当前项目

    **进入到项目根目录**

    `composer config repo.packagist composer packagist.laravel-china.org`

## 更新日志

#### 2017-09-16

添加 laravel-china 国内镜像

#### 2017-05-25 

Composer 从 1.4.2 更新到 1.5.2