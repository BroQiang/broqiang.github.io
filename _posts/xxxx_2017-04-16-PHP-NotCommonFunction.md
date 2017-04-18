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

---

### [set_include_path](http://php.net/manual/zh/function.set-include-path.php) - 为当前脚本设置 include_path 运行时的配置选项

- 语法 - string set_include_path ( string $new_include_path )

- 参数 - include_path 新的值, 一般 `get_include_path() . PATH_SEPARATOR . $new_include_path` 这样用

- 返回值 - 成功时返回旧的 include_path 或者在失败时返回 FALSE

---

### [get_include_path](http://php.net/manual/zh/function.get-include-path.php) - 获取当前 include_path 配置选项的值

- 语法 - string get_include_path ()

- 返回值 - 返回路径的字符串

---

### [define](http://php.net/manual/zh/function.define.php) - 定义一个常量

- 语法 - bool define ( string $name , mixed $value [, bool $case_insensitive = false ] )

- 参数
    - name - 常量名    
    - value - 常量的值
    - case_insensitive - 如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的,大小写不敏感的常量以小写的方式储存
    
- 返回值 - 成功时返回 TRUE， 或者在失败时返回 FALSE

---

### [defined](http://php.net/manual/zh/function.defined.php) - 检查某个名称的常量是否存在

- 语法 - bool defined ( string $name )

- 参数 - name 常量的名称

- 返回值 - 如果名称 name 的常量已定义,返回 TRUE,未定义则返回 FALSE

---

### [dirname](http://php.net/manual/zh/function.dirname.php) - 给出一个包含有指向一个文件的全路径的字符串

给出一个包含有指向一个文件的全路径的字符串，本函数返回去掉文件名后的目录名

- 语法 - string dirname ( string $path )

- 参数 - path 一个路径

- 返回值 - 返回 path 的父目录。 如果在 path 中没有斜线，则返回一个点（'.'），表示当前目录

---

### [session_start](http://php.net/manual/zh/function.session-start.php) - 启动新会话或者重用现有会话

session_start() 会创建新会话或者重用现有会话。 如果通过 GET 或者 POST 方式，或者使用 cookie 提交了会话 ID， 则会重用现有会话。

- 语法 - bool session_start ([ array $options = [] ] )

- 参数 - path 一个路径

- 返回值 - 返回 path 的父目录。 如果在 path 中没有斜线，则返回一个点（'.'），表示当前目录

---


        


