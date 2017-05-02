---
layout: post
title: 'PHP 自动加载'
date: '2017-05-02'
header-img: "img/post-bg-unix.jpg"
tags:
     - PHP
author: 'Bro Qiang'
---


# PHP 自动加载的实现

> 本项目定位是为了学习, 并不是最终使用版本, 并且非常基础
> 
> 真是项目推荐使用 Composer, 太强大了,太方便了
> 
> 为什么还要自己写呢 ? 学习, 不了解清楚了, 即使通过 Composer 可以使项目正常运行, 但是要是不明白 . . . . .
> 
> 此代码模仿的 Composer 实现,把本代码搞明白了, 再去学习 Composer 会轻松很多


## 源代码

我的 github 中 [auto-load-demo](https://github.com/BroQiang/auto-load-demo)

详细的使用可以看代码，代码中有详细的中文注释


## 开始之前需要掌握的知识点

需要提前掌握的因为在本框架中会用到, 同时也是可以学习到的知识点

- PHP环境搭建 - 可以参考[我的博客](http://broqiang.com), 里面有安装配置文档

- [类与对象](http://php.net/manual/zh/language.oop5.php) , 
    重点是 [类的自动加载](http://php.net/manual/zh/language.oop5.autoload.php) 及 
    [SPL 函数(自动加载函数)](http://php.net/manual/zh/function.spl-autoload-register.php)




## 目录结构

此结构借鉴的 Laravel, 用过几个框架,觉得这种方式最优雅, 当然因为此框架没有那么完善,还是会有不一样的地方

-- app - 项目代码根目录

-- bootstrap - 引导文件保存目录
 
-- public - 对外展示的目录,包括 `index.php` 入口文件, css,js等静态内容

-- src - 框架目录,此处也只有个助手函数和两个空类，用来测试


## 开始

在web服务器中, 将项目根目录配置到 '保存位置/auto-load-demo/public'

如果没有 Web 服务器的话也没关系,只要有 PHP 环境就可以了, 直接用 PHP 启动服务即可

示例: 

```shell
# 路径根据实际环境,这个是我的环境
$ cd /home/bro/www/localServer/auto-load-demo/public

# 通过 PHP 内置的web服务启动
$ php -S localhost:8888
```

浏览器直接输入 http://localhost:8888 即可访问

代码中从 public 下的入口文件 index.php 开始,我在代码中进行了非常详细的注释





