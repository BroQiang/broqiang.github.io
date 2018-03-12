---
layout: post
title: 'Composer 常用命令及参数'
date: '2017-04-29'
header-img: "img/post-bg-unix.jpg"
tags:
     - PHP
     - Composer
author: 'Bro Qiang'
---

Composer 是 PHP 的一个依赖管理工具, 它需要依赖 PHP

使用前要保证正确安装了PHP,并配置了环境变量

此处只是列出了比较常用的,更多请看官方文章

如果还没有安装 Composer, 请在本博客中超照 Composer 安装文档

[官网](https://getcomposer.org/)

[中文官网](http://www.phpcomposer.com/)

[packagist](https://packagist.org/)


## 全局参数

- `--verbose` - 反馈信息, 就是使用过程中在终端上显示的内容

    - `-v` - 正常输出
    - `-vv` - 更详细的输出
    - `-vvv` - Debug输出,非常详细的输出

## 命令

#### 初始化 init

使用方法:

```bash
$ composer init
```

参数: (下面的所有参数都不是必须的, 可以通过修改 `composer.json` 来改变)

- `--name` - 包的名称
- `--description` - 包的描述
- `--author` - 包的作者
- `--homepage` - 包的主页
- `--require` - 需要依赖的其它包,必须要有一个版本约束,并且应该遵循 foo/bar:1.0.0 这样的格式
- `--require-dev` - 开发版的依赖包,内容格式与 - equire 相同
- `--stability (-s)` - minimum-stability 字段的值


#### 安装 install

install 命令从当前目录读取 composer.json 文件,处理了依赖关系,并把其安装到 vendor 目录下

如果当前目录下存在 composer.lock 文件,它会从此文件读取依赖版本,而不是根据 composer.json 文件去获取依赖。这确保了该库的每个使用者都能得到相同的依赖版本。

如果没有 composer.lock 文件,composer 将在处理完依赖关系后创建它

**使用方法:**

```bash
$ composer install
```

**参数:**

- `--dry-run` - 只是想演示而并非实际安装,模拟安装并显示将会发生什么

- `--no-dev` - 跳过 require-dev 字段中列出的包

- `--no-scripts` - 跳过 composer.json 文件中定义的脚本


#### 更新 update

为了获取依赖的最新版本,并且升级 composer.lock 文件

**使用方法:**

```bash
$ composer install
```

**参数:**

同 install

#### 申明依赖 require

require 命令增加新的依赖包到当前目录的 composer.json 文件中

**使用方法:**

```bash
$ composer require "引入的包"
```

**包的说明:**

包的名称是由 `供应商名称/项目名称:版本号` 组成

如果不指定版本会安装最新版本, 建议指定, 因为有可能会安装开发版(还不稳定)

版本说明:

|     名称     |                 实例                 |                                                                                         描述                                                                                        |
|--------------|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 确切的版本号 | 1.0.2                                | 你可以指定包的确切版本                                                                                                                                                              |
| 范围         | >=1.0 >=1.0,<2.0 >=1.0,<1.1 &#124; >=1.2 | 通过使用比较操作符可以指定有效的版本范围,有效的运算符：>、>=、<、<=、!=,你可以定义多个范围,用逗号隔开,这将被视为一个逻辑AND处理,一个管道符号,将作为逻辑OR处理,AND 的优先级高于 OR |
| 通配符       | 1.0.*                                | 你可以使用通配符*来指定一种模式。1.0.*与>=1.0,<1.1是等效的 |
| 赋值运算符   | ~1.2                                 | 这对于遵循语义化版本号的项目非常有用, ~1.2相当于>=1.2,<2.0 |


#### 搜索 search

在 packagist 中搜索包

使用方法:

```bash
$ composer search "包名"
```

可以通过传递多个参数来进行多条件搜索, 如果只显示包名,加上 `--only-name` 参数,需要完全匹配包名


#### 依赖性检测 depends

可以查出已安装在你项目中的某个包,是否正在被其它的包所依赖,并列出他们

**使用方法:**

```bash
$ composer depends "包名"
```

此处的包名要是全名 `供应商/项目名`


#### Composer 本身更新 self-update

**使用方法:**

```bash
$ composer self-update
```

#### 更改配置 config

**使用方法:**

```bash
# 查询所有的配置
$ composer config "参数"
```

**参数:**

`--global` - 操作位于 $COMPOSER_HOME/config.json 的全局配置文件。如果不指定该参数，此命令将影响当前项目的 composer.json 文件
还有其他参数,这里只写了常用的

配置 Composer 全局国内镜像

```bash
$ composer config -g repo.packagist composer https://packagist.phpcomposer.com
```


#### 创建项目 create-project

相当于 `git clone` 项目, 并安装依赖关系

**使用方法:**

```bash
$ composer create-project "供应商名字/项目名" "保存的路径及名称" "指定版本"
# 安装 Laravle 示例
composer create-project --prefer-dist laravel/laravel myLaravel
```

**参数:**

- `--repository-url` - 提供一个自定义的储存库来搜索包，这将被用来代替 packagist.org, 和上面全局国内镜像意义相同,只是当前项目生效

- `--stability` - 资源包的最低稳定版本，默认为 stable

- `--prefer-source` -  当有可用的包时,从 source 安装

- `--prefer-dist` - 当有可用的包时，从 dist 安装

- `--dev` - 安装 require-dev 字段中列出的包

- `--no-install` - 禁止安装包的依赖

- `--no-plugins` - 禁用 plugins

- `--no-scripts` - 禁止在根资源包中定义的脚本执行


#### 打印自动加载索引 dump-autoload

**使用方法:**

```bash
$ composer dump-autoload
```

一般自己新建了个类,提示找不到的时候,执行下这个就对了


#### 执行脚本 run-script

只有在根包的 composer.json 中定义的脚本才会被执行

关于脚本, 请查看 [脚本](http://docs.phpcomposer.com/articles/scripts.html) 文档

**使用方法:**

```bash
$ composer run-script
```