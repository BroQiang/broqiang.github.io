---
layout: post
title: 'Linux 编译安装 PHP 7 '
date: '2017-04-18'
header-img: "img/post-bg-unix.jpg"
tags:
     - PHP
author: 'Bro Qiang'
---

## Linux 编译安装 PHP 7.1.6

- 此文档是在 Ubuntu 16.10 环境下测试编写, 理论上也支持 CentOS 7, 除了依赖关系,其他步骤相同即可

- 如参考此文档遇到问题,可以留言

- 编译的时候编译了 Mysql 支持,安装前要保证 Mysql 安装正确, 可以参考此博客中的 Mysql 安装

### 准备安装包

```shell
# 下载安装包
$ wget http://cn2.php.net/distributions/php-7.1.6.tar.gz
$ wget http://cn2.php.net/distributions/php-7.1.6.tar.gz

# 解压到src目录
$ sudo tar xzvf php-7.1.6.tar.gz -C /usr/local/src/
$ sudo tar xzvf php-7.1.6.tar.gz -C /usr/local/src/
```

### 解决依赖关系

```shell

# Ubuntu 16.10 执行下面命令
$ sudo apt install -y libxml2-dev libssl-dev libcurl4-gnutls-dev libjpeg-dev libpng-dev \
    libfreetype6-dev libmcrypt-dev



# CentOS 7 执行下面 命令
$ sudo yum install libxml2 libxml2-devel libcurl libcurl-devel libwebp libwebp-devel \
        libjpeg* libpng libpng-devel openldap-devel openldap libmcrypt libmcrypt-devel freetype-devel

```


### 创建守护进程用户

```shell
$ sudo useradd -M -s /sbin/nologin www
```

### 编译安装

此处只是常用的扩展, 如果需要什么扩展后期再安装也可以

```shell
# 进入到源码存放目录
$ cd /usr/local/src/php-7.1.6/
$ cd /usr/local/src/php-7.1.6/

# 配置 makefile
# 需要注意,此处将 mysql 编译进来了,需要保证 Mysql 已经安装配置好
$ sudo ./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc \
    --with-mysqli=/usr/local/mysql/bin/mysql_config --with-pdo-mysql=/usr/local/mysql \
    --with-mysql-sock=/tmp/mysql.sock --enable-sockets --enable-zip \
    --with-fpm-user=www --with-fpm-group=www --enable-fpm --enable-gd-native-ttf --enable-gd-jis-conv \
    --with-jpeg-dir --with-freetype-dir --with-gd --with-curl --with-mcrypt --with-openssl --with-mhash \
    --with-xmlrpc --enable-ftp --enable-bcmath --enable-shmop --enable-sysvsem --enable-soap \
    --enable-inline-optimization --enable-mbregex --enable-mbstring --enable-pcntl --with-zlib

$ sudo make
$ sudo make install
```


### 初始化配置

[详细参数配置参考](http://php.net/manual/zh/install.fpm.configuration.php)

```shell
# 复制默认配置文件
$ sudo cp php.ini-production /usr/local/php/etc/php.ini
$ sudo cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
$ sudo cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf
$ sudo cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf

# 为启动脚本增加权限
$ sudo chmod +x /etc/init.d/php-fpm

# 配置开机自动启动
# Ubuntu 用下面命令
$ sudo systemctl enable php-fpm

# CentOS7 用下面命令
# sudo chkconfig php-fpm on

```

### 配置时区

> 这个还是很有必要的, 如果 php.ini 中没有配置, 程序也没有初始化, 就会出现莫名其妙的问题了
> 
> 养成习惯,安装完了就给他配置上即可
 
根据项目实际去配置, 一般都是中国时区 `Asia/Shanghai`, [可以配置的时区](http://php.net/manual/zh/timezones.php)

```shell
$ sudo vim /usr/local/php/etc/php.ini

# 将下面的
;date.timezone = 
# 改成
date.timezone = Asia/Shanghai

```


### 配置环境变量

```shell
$ sudo vim /etc/profile.d/php.sh

# 写入下面内容
export PHP_PATH=/usr/local/php
export PATH=$PATH:$PHP_PATH/bin

# 生效, 桌面环境最好注销再登录
$ source /etc/profile.d/php.sh

# 测试, 输入下面内容,显示版本信息
$ php --version
```

### 测试 phpinfo

创建 test 目录

```shell
$ mkdir ~/test
```

在目录下创建 `index.php` 文件,写入下面内容

```php
<?php

    phpinfo();

```

在 `test` 目录中执行下面命令

因为此时还没有配置 web 服务, 可以用php 内置的先测试一下

```shell

# -S 参数就是运行内置的web服务, 后面跟的是 地址:端口号
# 如果想用80端口就要加上sudo,用root权限执行
$ php -S localhost:8888
```

此时可以在浏览器地址栏输入 `http://localhost:8888/` , 查看结果

看一下常用的PHP扩展是否安装成功, 比如 pdo_mysql,mysqli,gd(同时要看里面包含的图片格式),libxml,mbstring,curl,openssl等

太多了,直接去看phpinfo输出结果查看

### 额外的配置

- readline 扩展

    `--with-readline` 可以在终端使用 -a(--interactive) 模式，一般只有开发的时候才用得到
    
    安装 `libreadline-dev` (Ubuntu)/`readline-devel` (CentOS) 扩展
    编译PHP的时候加上 --with-readline 参数


## 更新记录

- 2017-06-11 更新到当前最新的 PHP 7.1.6

- 2017-05-25 更新到当前最新的 PHP 7.1.5
