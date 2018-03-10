---
layout: post
title: 'Linux 下 Mysql GUI 客户端'
date: '2017-02-11'
header-img: "img/post-bg-unix.jpg"
tags:
    - Mysql
author: 'Bro Qiang'
---

## MySQL Workbench

[https://www.mysql.com/products/workbench/](https://www.mysql.com/products/workbench)

这个是mysql官方的,功能比较全,不过设计的有点反人类,反正我不习惯使用

## Navicat (推荐)

这个软件比较好用,个人推荐,不过他的linux版本是基于wine的,还能凑合用吧

下载地址: [https://www.navicat.com.cn](https://www.navicat.com.cn)

下载下来直接解压缩即可用,推荐mysql_cs_x64版本,否则中文的支持有点头疼

解压后要将 `start_navicat` 中的默认语言修改一下

```shell
export LANG="en_US.UTF-8"
# 修改成
export LANG="zh_CN.UTF-8"
```

*安装完成后如果有方块,登录进去之后选择一下系统中存在的字体即可,如* `Roboto Mono Regular`

官方的只能免费使用 14 天，更多的使用方法可以参考： [自动安装脚本](https://gitee.com/BroQiang/Software_Navicat)