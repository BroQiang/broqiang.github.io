---
layout: post
title: 'Ubuntu apt 安装Mysql5.7'
date: '2017-02-10'
header-img: "img/post-bg-unix.jpg"
tags:
    - Mysql
author: 'Bro Qiang'
---


### 安装

开发环境,采用 apt 方式快速安装

`$ sudo apt install mysql-server-5.7`

------

### 字符集配置

此处设置utf8mb4，以后没有特殊需求都设置这种默认字符集，因为现在emoji表情，移动端数据兼容等

- 查询当前字符集

`mysql> SHOW VARIABLES WHERE Variable_name LIKE 'character\_set\_%' OR Variable_name LIKE 'collation%';`

- 设置字符集

将下面信息写入mysql配置文件中，根据实际安装去找mysql的配置文件
```
[client]
default-character-set = utf8mb4

[mysql]
default-character-set = utf8mb4

[mysqld]

character-set-server = utf8mb4

collation-server = utf8mb4_general_ci

init_connect='SET NAMES utf8mb4'
```

- 重启数据库

注意： 要stop再start，不要直接restart，否则不一定会生效
```shell
$ sudo systemctl stop mysql

$ sudo systemctl start mysql
```