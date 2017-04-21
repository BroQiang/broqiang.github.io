---
layout: post
title: 'PHP 中 include,include_once,require,require_once 详解'
date: '2017-04-21'
header-img: "img/post-bg-unix.jpg"
tags:
     - PHP
     - 语法
author: 'Bro Qiang'
---

## PHP 中 include,include_once,require,require_once 详解

这四种都是 PHP 的流程控制语句

### include 和 require 对比

官方的解释

> require 和 include 几乎完全一样，除了处理失败的方式不同之外。
> 
> require 在出错时产生 E_COMPILE_ERROR 级别的错误。
> 
> 换句话说将导致脚本中止而 include 只产生警告（E_WARNING），脚本会继续运行。

一般要求程序及时 包含失败也要继续执行,不能停止时, 用 include, 比如页面模板的引入

一般程序要求严格时,出错会影响后面代码时,要用 require, 一般除了页面模板尽量都用 require

### include,require 和 include_once,require_once

官方解释

> require_once 语句和 require 语句完全相同，唯一区别是 PHP 会检查该文件是否已经被包含过，如果是则不会再次包含。
> 
> include_once 和 include 语句类似，唯一区别是如果该文件中已经被包含过，则不会再次包含。如同此语句名字暗示的那样，只会包含一次。

写两个测试的 PHP 脚本就可以看出效果

新建一个 `test.php` ,里面只写入一句 echo 即可

```php
<?php

echo "我是将要被引用的文件<br>"; 
```

然后在访问 PHP 脚本中执行下面, 如 `index.php`

```shell
<?php 

include 'test.php'; 

require 'test.php';

include_once 'test.php';

require_once 'test.php';

```

可以看到结果, 只打印了两次而不是4次, 因为已经被包含过了, 所以不会再执行

```
我是将要被引用的文件
我是将要被引用的文件
```

### include和require后面是否需要加括号

这个网上的争论很多, 没找到什么有说服力的地方, 后来从官网看到 [Return](http://cn2.php.net/manual/zh/function.return.php) 中这样说明

> Note: 注意既然 return 是语言结构而不是函数，因此其参数没有必要用括号将其括起来。通常都不用括号，实际上也应该不用，这样可以降低 PHP 的负担。

从此处来看, include和require 也是语言结构, 加上会增加PHP 负担, 所以最好也不要加括号

实测,加上和不加上都不会出错, 代码可以正常执行

个人观点: 尽量不加, 不过要和其他语言混编,比如模板中使用,为了增加可读性或者解决其他语言的冲突, 也是可以加上的, 要灵活应用
 






