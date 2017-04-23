---
layout: post
title: 'PHP 函数索引'
date: '2017-04-16'
header-img: "img/post-bg-unix.jpg"
tags:
    - PHP
author: 'Bro Qiang'
---

# PHP 函数索引
 
> 下面只是简单列出函数名称,用途,并链接到官方文档
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

- [array_change_key_case](http://php.net/manual/zh/function.array-change-key-case.php) - 将数组中的所有键名修改为全大写或小写

- [array_chunk](http://php.net/manual/zh/function.array-chunk.php) - 将一个数组分割成多个(分割后变成二维数组)

- [array_column](http://php.net/manual/zh/function.array-column.php) - 返回数组中指定的一列(将二维数组变成一维数组)

- [array_combine](http://php.net/manual/zh/function.array-combine.php) - 创建一个数组，用一个数组的值作为其键名，另一个数组的值作为其值

- [array_count_values](http://php.net/manual/zh/function.array-count-values.php) - 统计数组中所有的值出现的次数

- [array_diff_assoc](http://php.net/manual/zh/function.array-diff-assoc.php) - 比较数组的`差集`,键和值都会比较(包括隐性的0,1,2等)

- [array_intersect_assoc](http://php.net/manual/zh/function.array-intersect-assoc.php) - 比较数组的`交集`,键和值都会比较(包括隐性的0,1,2等)

- [array_diff](http://php.net/manual/zh/function.array-diff.php) - 比较数组的值,计算数组的`差集`

- [array_intersect](http://php.net/manual/zh/function.array-intersect.php) - 通过数组的键比较数组的`交集`

- [array_diff_key](http://php.net/manual/zh/function.array-diff-key.php) - 通过数组的键比较数组的`差集`

- [array_intersect_key](http://php.net/manual/zh/function.array-intersect-key.php) - 通过数组的键比较数组的`交集`

- [array_fill_keys](http://php.net/manual/zh/function.array-fill-keys.php) - 使用指定的键和值填充数组

- [array_filter](http://php.net/manual/zh/function.array-filter.php) - 用回调函数过滤数组中的单元

- [array_flip](http://php.net/manual/zh/function.array-flip.php) - 交换数组中的键和值

- [array_key_exists](http://php.net/manual/zh/function.array-key-exists.php) - 检查数组里是否有指定的键名或索引

- [array_keys](http://php.net/manual/zh/function.array-keys.php) - 返回数组中部分的或所有的键名

- [array_map](http://php.net/manual/zh/function.array-map.php) - 为数组的每个元素应用回调函数

- [array_merge](http://php.net/manual/zh/function.array-merge.php) - 合并一个或多个数组

- [array_pad](http://php.net/manual/zh/function.array-pad.php) - 以指定长度将一个值填充进数组

- [array_pop](http://php.net/manual/zh/function.array-pop.php) - 去除数组最后一个值(出栈), 并且将数组长度减1, 返回的是去除的值

- [array_shift](http://php.net/manual/zh/function.array-shift.php) - 将数组开头的单元移出数组, 并且将数组长度减1, 返回的是去除的值

- [array_sum](http://php.net/manual/zh/function.array-sum.php) - 对数组中所有值求和

- [array_product](http://php.net/manual/zh/function.array-product.php) - 计算数组中所有值的乘积

- [array_unshift](http://php.net/manual/zh/function.array-unshift.php) - 在数组开头插入一个或多个单元

- [array_push](http://php.net/manual/zh/function.array-push.php) - 将一个或多个单元压入数组的末尾（入栈）

- [array_rand](http://php.net/manual/zh/function.array-rand.php) - 从数组中随机取出一个或多个单元,取出的是 key

- [array_reduce](http://php.net/manual/zh/function.array-reduce.php) - 用回调函数迭代地将数组简化为单一的值

- [array_replace_recursive](http://php.net/manual/zh/function.array-replace-recursive.php) - 使用传递的数组`递归`替换第一个数组的元素

- [array_replace](http://php.net/manual/zh/function.array-replace.php) - 使用传递的数组替换第一个数组的元素(`非递归`)

- [array_search](http://php.net/manual/zh/function.array-search.php) - 在数组中搜索给定的值，如果成功则返回首个相应的键名

- [array_slice](http://php.net/manual/zh/function.array-slice.php) - 从数组中指定位置取出指定数量的元素

- [array_splice](http://php.net/manual/zh/function.array-splice.php) - 去掉数组中的某一部分并用其它值取代

- [array_unique](http://php.net/manual/zh/function.array-unique.php) - 移除数组中重复的值

- [array_values](http://php.net/manual/zh/function.array-values.php) - 返回数组中所有的值,并给其建立数字索引

- [array_walk_recursive](http://php.net/manual/zh/function.array-walk-recursive.php) - 对数组中的每个成员递归地应用用户函数

- [array_walk](http://php.net/manual/zh/function.array-walk.php) - 使用用户自定义函数对数组中的每个元素做回调处理

- [array_reverse](http://php.net/manual/zh/function.array-reverse.php) - 将原本的数组倒序排序

- [asort](http://php.net/manual/zh/function.asort.php) - 对数组的值进行正向排序并保持索引关系

- [arsort](http://php.net/manual/zh/function.arsort.php) - 对数组的值进行逆向排序并保持索引关系

- [ksort](http://php.net/manual/zh/function.ksort.php) - 对数组按照键名正向排序

- [sort](http://php.net/manual/zh/function.sort.php) - 对数组正向排序,会重新生产索引

- [rsort](http://php.net/manual/zh/function.rsort.php) - 对数组逆向排序,会重新生产索引

- [krsort](http://php.net/manual/zh/function.krsort.php) - 对数组按照键名逆向排序

- [array_multisort](http://php.net/manual/zh/function.array-multisort.php) - 对多个数组或多维数组进行排序

- [shuffle](http://php.net/manual/zh/function.shuffle.php) - 打乱（随机排列单元的顺序）一个数组

- [compact](http://php.net/manual/zh/function.compact.php) - 建立一个数组，包括变量名和它们的值

- [extract](http://php.net/manual/zh/function.extract.php) - 从数组中将变量导入到当前的符号表

- [list](http://php.net/manual/zh/function.list.php) - 把数组中的值赋给一组变量

- [range](http://php.net/manual/zh/function.range.php) - 根据范围创建数组，包含指定的元素



### 杂项

- [define](http://php.net/manual/zh/function.define.php) - 定义一个常量

- [defined](http://php.net/manual/zh/function.defined.php) - 检查某个名称的常量是否存在

- 


### 文件系统

- [dirname](http://php.net/manual/zh/function.dirname.php) - 给出一个包含有指向一个文件的全路径的字符串


### Session

- [session_start](http://php.net/manual/zh/function.session-start.php) - 启动新会话或者重用现有会话



        


