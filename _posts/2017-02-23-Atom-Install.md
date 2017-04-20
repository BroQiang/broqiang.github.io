---
layout: post
title: 'Linux 安装 Atom 及常用插件'
date: '2017-02-23'
header-img: "img/post-bg-unix.jpg"
tags:
    - Editor
    - Atom
author: 'Bro Qiang'
---

### Atom 及常用插件安装

非常强大的一个文本编辑器，个人觉得比Sublime要强大

不过对PHP，尤其是Laravel支持没有Sublime好，现在我的主力编辑器仍然是Sublime

偶然也会用此工具写一些东西，比如Markdown

[官方网站](https://atom.io)

[中文社区](https://atom-china.org)

如果官方下载打开慢的话可以到我的 [码云仓库](https://git.oschina.net/BroQiang/software) 下载

- Ubuntu 安装

```shell
$ wget https://atom.io/download/deb -O atom-amd64.deb
$ sudo dpkg -i atom-amd64.deb
```

- CentOS/Fedora 安装

```shell
$ wget https://atom.io/download/rpm
$ sudo rpm -ivh atom.x86_64.rpm
# 或者
$ sudo yum install atom.x86_64.rpm
```

PS: 暂时没有找到重新加载的方法,所有安装完主题和插件都要重启软件使其生效,等找到了将次文本换成方法

### 修改源，设置国内镜像

如果速度慢就配置下面这个，如果有VPN，或者不慢，忽略此步

编辑下面的文件，如果没有就创建一个,此文件用来配置和apm相关的配置。

```shell
vim  ~/.atom/.apmrc

# 写入 
registry = https://registry.npm.taobao.org
```

## 安装主题

[查看所有官方主题](https://atom.io/themes)

安装material-ui和material-syntax(个人偏好这个,因为原来用Sublime的时候就是用的这个)

```shell
# 安装主题
$ apm install atom-material-ui

# 安装语法
$ apm install atom-material-syntax
```

### 安装始终插件atom-clock

[官方介绍](https://atom.io/packages/atom-clock)

使用此插件会在下方的状态栏显示一个时钟,算是有用的吧,毕竟全屏写代码时候可以知道什么时间该休息了

```shell
$ apm install atom-clock
```

重启软件后,点击插件下方,可以设置时间格式和地区,可以自定义设置

Date format: `YYYY-MM-DD H:mm`

Locales: `zh-cn`


### 代码格式化插件 atom-beautify

[官方介绍](https://atom.io/packages/atom-beautify)

```shell
$ apm install atom-beautify
```

此插件还需要一些其他的支持,比如PHP,需要提前安装好 `PHP-CS-Fixer`

## linter-php 语法检测插件

这个很有用,至少不用等到提交才发现代码错了...

[官方介绍](https://atom.io/packages/linter-php)

```shell
$ apm install linter-php
```

### autocomplete-php 插件

这个对我来说也挺有用,好多方法记不全,至少不用去翻手册了

[官方介绍](https://atom.io/packages/autocomplete-php)

```shell
$ apm install autocomplete-php
```

### docblockr 自动注释插件

[官方介绍](https://atom.io/packages/docblockr)

```shell
$ apm install docblockr
```

`extra_tags` 配置 `@Another BroQiang<broqiang@qq.com> , Date {{datetime}}`

### markdown-pdf 导出mardown到PDF

安装

```shell
$ apm install markdown-pdf
```

### style 设置

修改工具的 `style.css` 文件

- 隐藏默认带的虚线,根据分辨率,有可能在中间,有可能在右边

    ```css
    atom-text-editor::shadow .wrap-guide {
        visibility: hidden;
    }
    ```

- 设置mardown preview 样式
    
    如下面这个修改默认字体大小

    ```css
    .markdown-preview {
       p {
         font-size: 25px;
       }
     }
    ```


### 更新日志

- 2017-04-20
    
    因为官方的地址用 wget 下载完名字就叫 deb , 不影响安装

    不过看起来有点莫名其妙,更改下载的时候重命名了一下, 保持和 http 方式下载的名称一致

    更改 wget 下载方式 `wget https://atom.io/download/deb` 为 `wget https://atom.io/download/deb -O atom-amd64.deb`
