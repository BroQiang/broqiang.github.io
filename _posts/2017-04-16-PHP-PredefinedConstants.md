---
layout: post
title: 'PHP 预定义常量'
date: '2017-04-16'
header-img: "img/post-bg-unix.jpg"
tags:
    - PHP
author: 'Bro Qiang'
---

## PHP 预定义常量

此处只记录一些会经常用到的, 更多的常量见 [官方文档](http://php.net/manual/en/reserved.constants.php)

### 核心预定义常量

PHP 核心代码定义的常量

- PHP_VERSION (string) - PHP 版本, 建议只是展示用,不要用来去匹配

- PHP_VERSION_ID (integer) - 整数类型版本,如: `70015` , 推荐用此方法匹配

- PHP_MAXPATHLEN (integer) - 文件名的最大长度,包括路径

- PHP_OS (string) - 当前PHP 环境的操作系统,如: Linux

- PHP_EOL (string) - PHP 的换行符

    Linux 下是 `\n`, Windows 下是 `\r\n`, MAC 下是 `\r`

    推荐需要换行符时用此常量,提高可移植性

- DEFAULT_INCLUDE_PATH - 当时候函数include(),require(),fopen_with_path() 默认寻找的起始位置

- PHP_BINARY - PHP 可执行文件的绝对路径, 一般写命令行的时候会用到

### 标准预定义常量

太多了,这里只记录了最常用的

- DIRECTORY_SEPARATOR - 系统分隔符, Windows 下是 `\` , Linux 下是 `/`

- PATH_SEPARATOR - 环境变量分隔符, Windows 下是 `;` , Linux 下是 `:`



