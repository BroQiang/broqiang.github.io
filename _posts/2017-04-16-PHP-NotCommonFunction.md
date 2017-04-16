---
layout: post
title: 'PHP 不常用又非常有用的函数'
date: '2017-04-16'
header-img: "img/post-bg-unix.jpg"
tags:
    - PHP
author: 'Bro Qiang'
---

## PHP 不常用又非常有用的函数

标题定义成这个,就是因为此处记录的函数是平时不会经常用到
在特定 (比如开发框架) 的时候又非常有用, 需要了解, 至少知道有这个函数

#### [string set_include_path ( string $new_include_path )](http://php.net/manual/zh/function.set-include-path.php) 

为当前脚本设置 include_path 运行时的配置选项

- 参数 - include_path 新的值, 一般 `get_include_path() . PATH_SEPARATOR . $new_include_path` 这样用

- 返回值 - 成功时返回旧的 include_path 或者在失败时返回 FALSE


#### [string get_include_path ()](http://php.net/manual/zh/function.get-include-path.php)

获取当前 include_path 配置选项的值

- 返回值 - 返回路径的字符串

