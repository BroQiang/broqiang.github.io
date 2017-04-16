---
layout: post
title: '安装 PHP-CS-Fixer'
date: '2017-02-16'
header-img: "img/post-bg-unix.jpg"
tags:
    - PHP
author: 'Bro Qiang'
---

### 安装 PHP-CS-Fixer

此工具是用来进行代码格式化

参考: [https://github.com/FriendsOfPHP/PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)

**需要有php的环境变量,此工具依赖php-cli,安装此工具前要保证 PHP 已经安装并配置正确**

```
$ wget http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -O php-cs-fixer

$ chmod +x php-cs-fixer

$ sudo mv php-cs-fixer /usr/local/bin
```

