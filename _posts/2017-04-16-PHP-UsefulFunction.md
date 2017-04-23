---
layout: post
title: 'PHP 非常有用的函数'
date: '2017-04-16'
header-img: "img/post-bg-unix.jpg"
tags:
    - PHP
author: 'Bro Qiang'
---

# PHP 非常有用的函数
 
> 下面只是简单列出函数名称,参数,类型,用途,并链接到官方文档
> 
> 下面函数的组成分类是按照官方文档的结构分类组成
> 
> 此文档会持续更新一段时间,不在做更新记录

---

### PHP选项/信息

- [set_include_path](http://php.net/manual/zh/function.set-include-path.php) - 为当前脚本设置 include_path 运行时的配置选项

- [get_include_path](http://php.net/manual/zh/function.get-include-path.php) - 获取当前 include_path 配置选项的值

- [get_included_files](http://php.net/manual/zh/function.get-included-files.php) - 返回被 include 和 require 文件名的数组

- [extension_loaded](http://php.net/manual/zh/function.extension-loaded.php) - 检查一个扩展是否已经加载

- [get_loaded_extensions](http://php.net/manual/zh/function.get-loaded-extensions.php) - 返回所有编译并加载模块名的数组

- [ini_get_all](http://php.net/manual/zh/function.ini-get-all.php) - 获取所有配置选项

- [ini_get](http://php.net/manual/zh/function.ini-get.php) - 获取一个配置选项的值

- [ini_set](http://php.net/manual/zh/function.ini-set.php) - 为一个配置选项设置值

- [getenv](http://php.net/manual/zh/function.getenv.php) - 获取一个环境变量的值

- [getlastmod](http://php.net/manual/zh/function.getlastmod.php) - 获取执行的主脚本的最后修改时间

- [set_time_limit](http://php.net/manual/zh/function.set-time-limit.php) - 设置脚本最大执行时间

- [sys_get_temp_dir](http://php.net/manual/zh/function.sys-get-temp-dir.php) - 返回用于临时文件的目录

- [version_compare](http://php.net/manual/zh/function.version-compare.php) - 对比两个「PHP 规范化」的版本数字字符串


### 输出控制

只列出了最基本的,更多请访问 [官网](http://php.net/manual/zh/ref.outcontrol.php)

- [ob_start](http://php.net/manual/zh/function.ob-start.php) - 打开输出控制缓冲

- [ob_end_flush](http://php.net/manual/zh/function.ob-end-flush.php) - 输出缓冲区内容并关闭缓冲


### 类/对象

- [get_declared_classes](http://php.net/manual/zh/function.get-declared-classes.php) - 返回由已定义类的名字所组成的数组

- [get_declared_interfaces](http://php.net/manual/zh/function.get-declared-interfaces.php) - 返回包含所有已声明的接口的数组

- [get_declared_traits](http://php.net/manual/zh/function.get-declared-traits.php) - 返回所有已定义的 traits 的数组

- [get_object_vars](http://php.net/manual/zh/function.get-object-vars.php) - 返回由对象属性组成的关联数组

- [get_class_methods](http://php.net/manual/zh/function.get-class-methods.php) - 返回由类的方法组成的数组

- [get_class_vars](http://php.net/manual/zh/function.get-class-vars.php) - 返回由类的默认属性组成的数组

- [get_class](http://php.net/manual/zh/function.get-class.p) - 返回对象的类名

- [class_exists](http://php.net/manual/zh/function.class-exists.php) - 检查类是否已定义

- [interface_exists](http://php.net/manual/zh/function.interface-exists.php) - 检查接口是否已被定义

- [trait_exists](http://php.net/manual/zh/function.trait-exists.php) - 检查指定的 trait 是否存在

- [method_exists](http://php.net/manual/zh/function.method-exists.php) - 检查类的方法是否存在

- [is_subclass_of](http://php.net/manual/zh/function.is-subclass-of.php) - 对象是否是一个类的子类

- [property_exists](http://php.net/manual/zh/function.property-exists.php) - 检查对象或类是否具有该属性


### 函数处理

- [call_user_func](http://php.net/manual/zh/function.call-user-func.php) - 调用函数或对象中的方法

- [call_user_func_array](http://php.net/manual/zh/function.call-user-func-array.php) - 调用函数或对象中的方法,和 `call_user_func` 的类似,传递参数更友善

- [func_get_args](http://php.net/manual/zh/function.func-get-args.php) - 返回一个包含函数参数列表的数组

- [func_get_arg](http://php.net/manual/zh/function.func-get-arg.php) - 返回参数列表的某一项

- [func_num_args](http://php.net/manual/zh/function.func-num-args.php) - 返回传递给函数参数的数量

- [function_exists](http://php.net/manual/zh/function.function-exists.php) - 判断指定的函数是否存在

- [get_defined_functions](http://php.net/manual/zh/function.get-defined-functions.php) - 返回所有已经定义的函数名称的数组(二维数组,按照 internal 和 user 组合)

- [register_shutdown_function](http://php.net/manual/zh/function.register-shutdown-function.php) - 注册一个会在php中止时执行的函数



### 数组

- [array_pop](http://php.net/manual/zh/function.array-pop.php) - 去除数组最后一个值(出栈), 并且将数组长度减1, 返回的是去除的值


### 杂项

- [define](http://php.net/manual/zh/function.define.php) - 定义一个常量

- [defined](http://php.net/manual/zh/function.defined.php) - 检查某个名称的常量是否存在

- 


### 文件系统

- [dirname](http://php.net/manual/zh/function.dirname.php) - 给出一个包含有指向一个文件的全路径的字符串


### Session

- [session_start](http://php.net/manual/zh/function.session-start.php) - 启动新会话或者重用现有会话



        


