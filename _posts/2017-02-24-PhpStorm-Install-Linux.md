---
layout: post
title: 'Linux 安装配置 PHPStorm'
date: '2017-02-24'
header-img: "img/post-bg-unix.jpg"
tags:
    - Editor
    - PhpStorm
author: 'Bro Qiang'
---

## Linux 安装配置 PHPStorm

虽然个人喜欢Sublime,但是他只是一个功能强大的文本编辑器

PhpStorm 因为太占资源还有速度,不是很喜欢,但是它仍然是 PHP 最强大的 IDE

### 获取软件

[官方下载](https://www.jetbrains.com/phpstorm/download)

可以选择对应的平台的版本, Windows , macOS , Linux 他都支持,跨平台支持很好

此处讲解的是 Linux 下的安装及使用

## 安装

```shell
# 可以去官方找到最新版本下载,此版本是写此文档时的最新版本
$ wget https://download.jetbrains.8686c.com/webide/PhpStorm-2017.1.1.tar.gz
# 解压缩
$ tar xzvf PhpStorm-2017.1.1.tar.gz
# 名字太长,该个名字(非必须)
$ mv PhpStorm-171.4163.3/ PhpStorm
# 配置个启动文件,也可以直接放到 /usr/local/bin 中
$ vim ~/bin/phpstorm

# 写入下面内容
#!/bin/bash
#
/home/bro/Program/PhpStorm/bin/phpstorm.sh

# wq 保存

# 增加执行权限
$ chmod +x ~/bin/phpstorm

```

上面步骤执行完成后,用快捷键 `Alt+F2` 输入 `phpstorm` 就可以打开了

## 首次启动

首次启动会有个简单的配置

- 导入配置文件

    如果之前保存了配置文件,直接导入即可,省去了配置的时间,配置好了之后也可以导出一份配置文件

    此处是第一次安装,选择 `Do not import settings`

- 激活

    此处可以选择激活或适用,适用可以适用30天

    选择 `Active` ,然后选择下面的 `Activation code`,输入

    ```
    CNEKJPQZEX-eyJsaWNlbnNlSWQiOiJDTkVLSlBRWkVYIiwibGljZW5zZWVOYW1lIjoibGFuIHl1IiwiYXNzaWduZWVOYW1lIjoiIiwiYXNzaWduZWVFbWFpbCI6IiIsImxpY2Vuc2VSZXN0cmljdGlvbiI6IkZvciBlZHVjYXRpb25hbCB1c2Ugb25seSIsImNoZWNrQ29uY3VycmVudFVzZSI6ZmFsc2UsInByb2R1Y3RzIjpbeyJjb2RlIjoiQUMiLCJwYWlkVXBUbyI6IjIwMTgtMDEtMzAifSx7ImNvZGUiOiJETSIsInBhaWRVcFRvIjoiMjAxOC0wMS0zMCJ9LHsiY29kZSI6IklJIiwicGFpZFVwVG8iOiIyMDE4LTAxLTMwIn0seyJjb2RlIjoiUlMwIiwicGFpZFVwVG8iOiIyMDE4LTAxLTMwIn0seyJjb2RlIjoiV1MiLCJwYWlkVXBUbyI6IjIwMTgtMDEtMzAifSx7ImNvZGUiOiJEUE4iLCJwYWlkVXBUbyI6IjIwMTgtMDEtMzAifSx7ImNvZGUiOiJSQyIsInBhaWRVcFRvIjoiMjAxOC0wMS0zMCJ9LHsiY29kZSI6IlBTIiwicGFpZFVwVG8iOiIyMDE4LTAxLTMwIn0seyJjb2RlIjoiREMiLCJwYWlkVXBUbyI6IjIwMTgtMDEtMzAifSx7ImNvZGUiOiJEQiIsInBhaWRVcFRvIjoiMjAxOC0wMS0zMCJ9LHsiY29kZSI6IlJNIiwicGFpZFVwVG8iOiIyMDE4LTAxLTMwIn0seyJjb2RlIjoiUEMiLCJwYWlkVXBUbyI6IjIwMTgtMDEtMzAifSx7ImNvZGUiOiJDTCIsInBhaWRVcFRvIjoiMjAxOC0wMS0zMCJ9XSwiaGFzaCI6IjUxOTU1OTMvMCIsImdyYWNlUGVyaW9kRGF5cyI6MCwiYXV0b1Byb2xvbmdhdGVkIjpmYWxzZSwiaXNBdXRvUHJvbG9uZ2F0ZWQiOmZhbHNlfQ==-QOxwjWvRwJz6vo6J6adC3CJ4ukQHosbPYZ94URUVFna/Rbew8xK/M5gP3kAaPh6ZDveFdtMR1UBoumq3eCwXtXM3U3ls5noB4LIr+QplVlCj2pK5uNq7g/feyNyQcHpSXtvhIOnXDBLOecB05DOsxzm0p7ulGGJoAInmHeb9mc0eYjqc4RPpUQfh6HSYBnvEnKMlLF5bz4KEtzmsvvgA55CwzwQ3gRitm5Q/wUT7AQCBdjmBfNUjKVQL6TSjSDPp56FUdEs4Aab8LqstA2DIMbxocO64rvytmcUeIwu8Mi5uq87KQP5AQMSMYb59Inbd+dmVfx5cJo3fRS4/5s3/Hg==-MIIEPjCCAiagAwIBAgIBBTANBgkqhkiG9w0BAQsFADAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBMB4XDTE1MTEwMjA4MjE0OFoXDTE4MTEwMTA4MjE0OFowETEPMA0GA1UEAwwGcHJvZDN5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxcQkq+zdxlR2mmRYBPzGbUNdMN6OaXiXzxIWtMEkrJMO/5oUfQJbLLuMSMK0QHFmaI37WShyxZcfRCidwXjot4zmNBKnlyHodDij/78TmVqFl8nOeD5+07B8VEaIu7c3E1N+e1doC6wht4I4+IEmtsPAdoaj5WCQVQbrI8KeT8M9VcBIWX7fD0fhexfg3ZRt0xqwMcXGNp3DdJHiO0rCdU+Itv7EmtnSVq9jBG1usMSFvMowR25mju2JcPFp1+I4ZI+FqgR8gyG8oiNDyNEoAbsR3lOpI7grUYSvkB/xVy/VoklPCK2h0f0GJxFjnye8NT1PAywoyl7RmiAVRE/EKwIDAQABo4GZMIGWMAkGA1UdEwQCMAAwHQYDVR0OBBYEFGEpG9oZGcfLMGNBkY7SgHiMGgTcMEgGA1UdIwRBMD+AFKOetkhnQhI2Qb1t4Lm0oFKLl/GzoRykGjAYMRYwFAYDVQQDDA1KZXRQcm9maWxlIENBggkA0myxg7KDeeEwEwYDVR0lBAwwCgYIKwYBBQUHAwEwCwYDVR0PBAQDAgWgMA0GCSqGSIb3DQEBCwUAA4ICAQC9WZuYgQedSuOc5TOUSrRigMw4/+wuC5EtZBfvdl4HT/8vzMW/oUlIP4YCvA0XKyBaCJ2iX+ZCDKoPfiYXiaSiH+HxAPV6J79vvouxKrWg2XV6ShFtPLP+0gPdGq3x9R3+kJbmAm8w+FOdlWqAfJrLvpzMGNeDU14YGXiZ9bVzmIQbwrBA+c/F4tlK/DV07dsNExihqFoibnqDiVNTGombaU2dDup2gwKdL81ua8EIcGNExHe82kjF4zwfadHk3bQVvbfdAwxcDy4xBjs3L4raPLU3yenSzr/OEur1+jfOxnQSmEcMXKXgrAQ9U55gwjcOFKrgOxEdek/Sk1VfOjvS+nuM4eyEruFMfaZHzoQiuw4IqgGc45ohFH0UUyjYcuFxxDSU9lMCv8qdHKm+wnPRb0l9l5vXsCBDuhAGYD6ss+Ga+aDY6f/qXZuUCEUOH3QUNbbCUlviSz6+GiRnt1kA9N2Qachl+2yBfaqUqr8h7Z2gsx5LcIf5kYNsqJ0GavXTVyWh7PYiKX4bs354ZQLUwwa/cG++2+wNWP+HtBhVxMRNTdVhSm38AknZlD+PTAsWGu9GyLmhti2EnVwGybSD2Dxmhxk3IPCkhKAK+pl0eWYGZWG3tJ9mZ7SowcXLWDFAk0lRJnKGFMTggrWjV8GYpw5bq23VmIqqDLgkNzuoog==
    ```

    此注册码来自 [http://idea.qinxi1992.cn/](http://idea.qinxi1992.cn/)  仅供学习使用,请自行购买正版

- 简单的初始化配置

    - 快捷键方案

        可以支持 Eclipse 等 IDE 的快捷键方案(如果你以前用过,可以选择一个习惯的)

        此处选择的是 `Default for GNOME`

    - IDE 主题

        默认的 IntelliJ 是白色主题

        Darcula 是暗色主题 (我选择的此主题)

        这个看个人喜好去选择了

    - 编辑器的颜色和字体,

        也有好几种方案供选择,可以点击下面的预览看看效果,按照个人喜好去选择

        此处选择的也是 Darcula

- 然后就可以 创建一个新的项目或者打开一个项目开始使用了

### 常用快捷键

可以在菜单 Navigate 中查询到

- `Ctrl + n` 快速查找一个类

- `Ctrl + Shift + n` 快速查找一个一个文件

- `Ctrl + Shift + Alt + n` 快速查找一个方法所在的文件

- `Ctrl + G` 快速根据行和列查找

上面的是默认的快捷键, 可以根据个人习惯去更改

### 安装 Material 主题

[material 主题下载](https://plugins.jetbrains.com/plugin/8006-material-theme-ui)

由于 Sublime 和 Atom 用的都是这个,也习惯这个了,所以安装此主题

下载下来是一个 zip 包,要在setting中选择 plugin (插件来安装)

### 我的配置

[我的配置](https://git.oschina.net/BroQiang/software/raw/master/bro-settings.jar)

此配置包括所有的配置,快捷键,主题等都已经修改

