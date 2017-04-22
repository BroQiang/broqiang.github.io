---
layout: post
title: 'PHP 不常用又非常有用的函数'
date: '2017-04-16'
header-img: "img/post-bg-unix.jpg"
tags:
    - PHP
author: 'Bro Qiang'
---

# PHP 不常用又非常有用的函数

> 标题定义成这个,就是因为此处记录的函数是平时不会经常用到在特定 (比如开发框架) 的时候又非常有用, 需要了解, 至少知道有这个函数
> 
> 下面只是简单列出函数名称,参数,类型,用途,并链接到官方文档
> 
> 下面函数的组成方式是按照官方文档的结构组成
> 
> 此文档更新会比较频繁,遇到觉得有用需要记录的就会记录下来,不在做更新记录

---

### PHP选项/信息

-- [set_include_path](http://php.net/manual/zh/function.set-include-path.php) - 为当前脚本设置 include_path 运行时的配置选项

-- [get_include_path](http://php.net/manual/zh/function.get-include-path.php) - 获取当前 include_path 配置选项的值

-- [get_included_files](http://php.net/manual/zh/function.get-included-files.php) - 返回被 include 和 require 文件名的数组

-- [extension_loaded](http://php.net/manual/zh/function.extension-loaded.php) - 检查一个扩展是否已经加载

-- [get_loaded_extensions](http://php.net/manual/zh/function.get-loaded-extensions.php) - 返回所有编译并加载模块名的数组

-- [ini_get_all](http://php.net/manual/zh/function.ini-get-all.php) - 获取所有配置选项

-- [ini_get](http://php.net/manual/zh/function.ini-get.php) - 获取一个配置选项的值

-- [ini_set](http://php.net/manual/zh/function.ini-set.php) - 为一个配置选项设置值

-- [getenv](http://php.net/manual/zh/function.getenv.php) - 获取一个环境变量的值

-- [getlastmod](http://php.net/manual/zh/function.getlastmod.php) - 获取执行的主脚本的最后修改时间

-- [set_time_limit](http://php.net/manual/zh/function.set-time-limit.php) - 设置脚本最大执行时间

-- [sys_get_temp_dir](http://php.net/manual/zh/function.sys-get-temp-dir.php) - 返回用于临时文件的目录

-- [version_compare](http://php.net/manual/zh/function.version-compare.php) - 对比两个「PHP 规范化」的版本数字字符串


### 输出控制

只列出了最基本的,更多请访问 [官网](http://php.net/manual/zh/ref.outcontrol.php)

-- [ob_start](http://php.net/manual/zh/function.ob-start.php) - 打开输出控制缓冲

-- [ob_end_flush](http://php.net/manual/zh/function.ob-end-flush.php) - 输出缓冲区内容并关闭缓冲


### 杂项

-- [define](http://php.net/manual/zh/function.define.php) - 定义一个常量

-- [defined](http://php.net/manual/zh/function.defined.php) - 检查某个名称的常量是否存在

-- 


### 文件系统

-- [dirname](http://php.net/manual/zh/function.dirname.php) - 给出一个包含有指向一个文件的全路径的字符串

### Session

-- [session_start](http://php.net/manual/zh/function.session-start.php) - 启动新会话或者重用现有会话


### 类/对象

-- [get_declared_classes](http://php.net/manual/zh/function.get-declared-classes.php) - 返回由已定义类的名字所组成的数组



        


