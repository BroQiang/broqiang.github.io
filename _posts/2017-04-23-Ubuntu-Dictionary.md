---
layout: post
title: 'Ubuntu 16.10 下离线词典'
date: '2017-04-23'
header-img: "img/post-bg-unix.jpg"
tags:
     - Ubuntu
author: 'Bro Qiang'
---

## Ubuntu 下离线词典

Linux 下的词典支持的不是很好, 不过一般情况下打开个浏览器就行了, Web 端支持的很好了

不过偶尔会有没有网的情况,就尴尬了(英语不太好啊)

也可以查看文档的时候划词翻译, 也算是方便了

### 安装 goldendict

星际译王不更新了, 这个勉强还能用

```shell
$ sudo apt install goldendict
```

### 添加在线词典

有道 http://dict.youdao.com/search?q=%GDWORD%&ue=utf8


### 添加离线词典

可以去星际译王的词典库下载 [下载地址](http://download.huzheng.org/zh_CN)

可以到我的 [码云仓库](https://git.oschina.net/BroQiang/software) 下载

只保存了 朗道英汉/汉英字典 词库, 够基本功能,  无网的时候应急

