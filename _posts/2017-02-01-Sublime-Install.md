---
layout: post
title: 'Sublime 安装'
date: '2017-02-01'
header-img: "img/post-bg-unix.jpg"
tags:
     - Editor
     - Sublime
author: 'Bro Qiang'
---

# Sublime的安装配置

用过几个编辑器，比如Atom（非常强大，也非常喜欢，尤其是用来写markdown）,不过对不是对PHP不友好，就是对Linux不友好，最后没办法，还是转回了Sublime，在Linux下，他对中文不友好，有个替代方案，凑合用，还好写代码的时候就是表单注释之类的用到中文，不算太多，还能凑合用

### 获取软件

官方下载：　[http://www.sublimetext.com/3](http://www.sublimetext.com/3)


### 安装

- Ubuntu直接下载Deb包
    ```shell
# 可以根据下载的版本去安装，这样就不用管版本了
$sudo dpki -i sublime-text_build*
    ```

- 其他版本，直接解压就可以用了


### 安装包控制器

这个是Sublime的精髓,后面安装的时候都会用到

- 安装

    按快捷键`Ctrl+Shift+p`

    输入 `Install Package Control`

    回车,等待安装成功的提示即可


### 安装字体

推荐Google的`Roboto Mono`字体

- 下载地址: [https://fonts.google.com/specimen/Roboto+Mono](https://fonts.google.com/specimen/Roboto+Mono)

- 下载完直接解压到系统的字体目录即可

    `$ sudo unzip Roboto_Mono.zip -d /usr/share/fonts/Roboto_Mono`

    配置文件中加入`"font_face": "Roboto Mono",`

### 安装配置主题

- 通过包控制器安装 `Material Theme`

- 修改左侧目录树和Tab字体大小

    - 安装 `PackageResourceViewer`

    - 通过 `PackageResourceViewer` 生成模板配置文件

        输入 `PackageResourceVIewer: Extract Package`

        输入模板名称（根据使用的去查找) `Material Theme`
    - 编辑模板配置文件

        - 在终端输入  `$ subl .config/sublime-text-3/Packages/Material\ Theme/Material-Theme.sublime-theme`

            subl是sublime文本编辑器的命令，也可以用vim gedit等，看使用习惯

        - 修改Tab标签字体大小

            在359行（根据实际情况，可以搜索`// Tab Labels`找到）

            将`"font.size": 11`改成想要的大小，如`"font.size": 12,`

        - 修改左侧目录树

            查找`sidebar_label`,有很多个，找到的最上面的一个（第一个）

            在找到行下面加入`"font.size": 14,` 字体大小看个人喜好配置
            

### 配置文件备份

此配置是我当前正在使用的,留作备份,下次安装的时候可以快速恢复

```json
{
    "color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
    "expand_tabs_on_save": true,
    "font_face": "Roboto Mono",
    "font_size": 12,
    "ignored_packages":
    [
        "Vintage"
    ],
    "line_padding_bottom": 6,
    "line_padding_top": 6,
    "marin": 0,
    "material_theme_accent_cyan": true,
    "material_theme_big_fileicons": true,
    "material_theme_bold_tab": true,
    "material_theme_bright_scrollbars": true,
    "material_theme_small_statusbar": true,
    "material_theme_small_tab": true,
    "tab_size": 4,
    "theme": "Material-Theme.sublime-theme",
    "translate_tabs_to_spaces": true
}

```


### License Key

License 来自搜索出来的这篇 [博客](http://blog.csdn.net/hexon804/article/details/50982952)

仅用于测试，请测试后删除


```
—– BEGIN LICENSE —–
Ryan Clark
Single User License
EA7E-812479
2158A7DE B690A7A3 8EC04710 006A5EEB
34E77CA3 9C82C81F 0DB6371B 79704E6F
93F36655 B031503A 03257CCC 01B20F60
D304FA8D B1B4F0AF 8A76C7BA 0FA94D55
56D46BCE 5237A341 CD837F30 4D60772D
349B1179 A996F826 90CDB73C 24D41245
FD032C30 AD5E7241 4EAA66ED 167D91FB
55896B16 EA125C81 F550AF6B A6820916
—— END LICENSE ——
```


