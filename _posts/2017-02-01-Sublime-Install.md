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


## Windows 版本

Windows 版本比较简单，直接下载下来双击安装即可。

- [Windows 32位](https://download.sublimetext.com/Sublime%20Text%20Build%203143%20Setup.exe)

- [WIndows 64位](https://download.sublimetext.com/Sublime%20Text%20Build%203143%20x64%20Setup.exe)

> 后面的配置全部都是 Linux 下的配置， Windows 下不一定完全兼容，可以参考，会有不太一样的地方。

## Linux 版本

Linux 官方已经不再直接提供 `deb` 和 `rpm` 包，不过提供了配置软件源的方式，可以通过 `apt` 或 `yum` 方式安装。详细可以查看 [官方文档](https://www.sublimetext.com/docs/3/linux_repositories.html) 。

#### Ubuntu 安装

```bash
# 安装 GPG key
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

# 配置软件源
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

# 更新软件源并安装 Sublime
sudo apt-get update
sudo apt-get install sublime-text
```

#### CentOS 安装

```bash
# 安装 GPG key
sudo rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg

# 配置软件源
sudo yum-config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo

# 安装
sudo yum install sublime-text
```

#### Fedora 安装

```bash
# 安装 GPG key
sudo rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg

# 配置软件源
sudo dnf config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo

# 安装
sudo dnf install sublime-text
```

#### tar 包安装

这个是官方提供的二进制包，直接下载后直接使用即可，不过使用此方法需要手动配置图标、快速启动、菜单等选项，所以 `不推荐` 此种方式安装。

- [32 位下载地址](https://download.sublimetext.com/sublime_text_3_build_3143_x32.tar.bz2) 
- [64 位下载地址](https://download.sublimetext.com/sublime_text_3_build_3143_x64.tar.bz2)

```bash
# 32 位
wget https://download.sublimetext.com/sublime_text_3_build_3143_x32.tar.bz2
# 解压
tar xjvf sublime_text_3_build_3143_x32.tar.bz2 -C /opt

# 64 位
wget https://download.sublimetext.com/sublime_text_3_build_3143_x64.tar.bz2
# 解压
tar xjvf sublime_text_3_build_3143_x64.tar.bz2 -C /opt

# 使用，直接到安装目录下执行安装目录下的 sublime_text 即可
/opt/sublime_text/sublime_text
```

#### 通过安装脚本自动安装

因为 `网络` 的原因， Sublime 的软件源会偶尔无法安装，并且每次重新安装都要配置很多插件，所以我写了个自动安装包，已经包含了 `PHP` 开发常用的插件，所以 `强烈推荐` 此种方式安装。


**获取安装包：**

- 浏览器直接 [下载](https://github.com/BroQiang/Software_Sublime/archive/V1.0.1.tar.gz)

- 通过 `git` 将代码 clone 到本地 `git clone https://github.com/BroQiang/Software_Sublime.git`

**安装**

```bash
# 进入下载好的安装包
cd Software_Sublime

# 直接执行安装包中的 start.sh 即可
./start.sh
```

更多的使用方法见： [Sublime 安装脚本](https://github.com/BroQiang/Software_Sublime)


## 安装包控制器

包控制器是用来安装和管理插件的工具，如果不安装这个就没法安装插件。

> 如果是安装脚本安装的话，这步就可以忽略了。


按快捷键`Ctrl+Shift+p`

输入 `Install Package Control`

回车,等待安装成功的提示即可


## 安装字体

推荐Google的`Roboto Mono`字体，也可以使用自己喜好的字体，这个看个人喜好。

下载地址: [https://fonts.google.com/specimen/Roboto+Mono](https://fonts.google.com/specimen/Roboto+Mono)

下载完直接解压到系统的字体目录即可

```bash
sudo unzip Roboto_Mono.zip -d /usr/share/fonts/Roboto_Mono
```

配置文件中加入`"font_face": "Roboto Mono",`

## 安装配置主题

#### Material Theme 主题

个人非常喜好这个主题，这个可以根据个人喜好，如果喜欢默认主题就可以忽略此部

通过包控制器安装即可

- 按快捷键 `Ctrl+Shift+p`

- 输入 `package Control: install Package`

- 输入 `Material Theme`

- 回车,等待安装成功的提示即可

> 后面安装插件都是这个步骤，就不在详细写安装步骤了。



#### 修改左侧目录树和Tab字体大小

如果分辨率比较高的电脑，左侧目录树的字体会非常的小，可以通过下面方式安装

- 安装 `PackageResourceViewer`

- `Ctrl+Shift+p` 输入 `PackageResourceViewer`

- 输入 `PackageResourceVIewer: Extract Package`

- 输入模板名称（根据使用的去查找) `Material Theme`

- 编辑模板配置文件

    在终端输入
```bash
# 可以按照自己的习惯打开文件， vim 或者 gedit 等都可以。
subl ~/.config/sublime-text-3/Packages/Material\ Theme/Material-Theme.sublime-theme
```

- 修改Tab标签字体大小（顶部的标签）

    在367行（根据实际情况，可以搜索`// Tab Labels`找到）

    将`"font.size": 11`改成想要的大小，如`"font.size": 12,`

- 修改左侧目录树

    查找`sidebar_label`,有很多个，找到的最上面的一个（第一个）

    在找到行下面加入`"font.size": 14,` 字体大小看个人喜好配置



## 配置文件备份

此配置是我当前正在使用的,留作备份,下次安装的时候可以快速恢复。

这个根据个人实际配置去配置，需要注意，如果是 Windows 下的 Sublime 不要使用，会有不兼容的地方。

```json
{
    "color_scheme": "Packages/Material Theme/schemes/Material-Theme.tmTheme",
    "expand_tabs_on_save": true,
    "font_face": "Roboto Mono",
    "font_size": 12,
    "ignored_packages":
    [
        "vim"
    ],
    "line_padding_bottom": 6,
    "line_padding_top": 6,
    "marin": 0,
    "material_theme_accent_cyan": true,
    "material_theme_big_fileicons": true,
    "material_theme_bold_tab": true,
    "material_theme_bright_scrollbars": true,
    "material_theme_contrast_mode": true,
    "material_theme_small_statusbar": true,
    "material_theme_small_tab": true,
    "tab_size": 4,
    "theme": "Material-Theme.sublime-theme",
    "translate_tabs_to_spaces": true
}
```


## 快捷键备份

这个是我平时使用的快捷键，备份下来，方便快速恢复。

```json
[
    //自动补全命名空间
    {"keys": ["f9"], "command": "expand_fqcn"}, 
    //自动寻找命名空间
    {"keys": ["f8"], "command": "find_use"}, 
    //自动生产构造函数
    {"keys": ["f7"], "command": "insert_php_constructor_property"}, 
    // 全屏的快捷键
    {"keys": ["alt+enter"], "command": "toggle_full_screen"}, 
    // 打开、关闭菜单栏的快捷键
    {"keys": ["ctrl+k", "ctrl+m"], "command": "toggle_menu"},
    // 复制文件的路径
    { "keys": ["ctrl+shift+alt+c"], "command": "copy_path" },
]
```

## License Key

Sublime Text 3 build 3143 LICENSE，来自 [gist](https://gist.github.com/jochemstoel/29205b69712924c7ba8d3f83b6dd0dd9) 

仅用于测试，请支持正版，请测试后将其删除。


```
—– BEGIN LICENSE —–
TwitterInc
200 User License
EA7E-890007
1D77F72E 390CDD93 4DCBA022 FAF60790
61AA12C0 A37081C5 D0316412 4584D136
94D7F7D4 95BC8C1C 527DA828 560BB037
D1EDDD8C AE7B379F 50C9D69D B35179EF
2FE898C4 8E4277A8 555CE714 E1FB0E43
D5D52613 C3D12E98 BC49967F 7652EED2
9D2D2E61 67610860 6D338B72 5CF95C69
E36B85CC 84991F19 7575D828 470A92AB
—— END LICENSE ——
```



