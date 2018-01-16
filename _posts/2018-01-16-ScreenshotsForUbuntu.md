---
layout: post
title: 'Ubuntu 17.10 截图工具'
date: '2018-01-16'
header-img: "img/post-bg-unix.jpg"
tags:
     - Linux
author: 'Bro Qiang'
---

# Ubuntu 17.10 截图工具

因为 Ubuntu 17.10 默认使用了 Wayland，虽然也可以切换到 xorg ，但是我的笔记是雷神 st pro，不能使用 xorg，切换到 xorg 之后显卡不能正常工作，所以只能选择可以在 Wayland 下可以工作的截图工具，以前 16.04 时候使用的 深度截图、shutter 都不能正常工作了，不过还好找到了一个可以替换的，不是很出名，搜索了好久才找到的，不过非常好用，比之前的 shutter 和 深度截图都要方便。

Github仓库： [flameshot](https://github.com/lupoDharkael/flameshot)

## 安装

#### Ubuntu 17.10

其他版本没有尝试，原则上来说也是可以成功安装。

```shell
# 安装依赖
sudo apt install git g++ build-essential qt5-qmake qt5-default qttools5-dev-tools

# 编译
qmake && make

# 安装
sudo make install
```

#### Fedora

这个是文档中写的方法，没有实测

```shell
sudo dnf install qt5-devel gcc-c++ git qt5-qtbase-devel qt5-linguist
qmake-qt5 && make
sudo make install
```

## 使用

可以通过命令直接使用，也可以配置一个快捷键，快速使用

#### 命令

```shell
# 开始截图，直接就是截图界面，有些类似 QQ 截图和 深度截图，不过比 QQ 截图更加强大
flameshot gui

# 开始截图，并配置默认的保存位置，和上面的界面相同，只是有了一个默认保存位置
# 创建默认保存目录，只要是真实存在并且有写入权限的目录即可，可以根据跟人爱好去配置
mkdir -p ~/Pictures/Screenshot
# 截图后图片会默认保存到 Screenshot 目录
lameshot gui -p ~/Pictures/Screenshot

# 延时启动，单位事毫秒，如 2000 就是 2秒，这种方式适用于截取右键菜单，也是比较方便的
flameshot gui -d 2000
```

#### 可以配置一个快捷键

设置->设备->键盘,在最下面，选择添加一个自定义快捷键

如我的：

- 名称： `截图`

    这个可以随意起，叫什么都可以

- 命令： `flameshot gui -p /home/bro/Pictures/Screenshot/`

    命令可以根据需要，上面命令中列出的都可以使用

- 快捷键： `Alt+S`

    开启截图的快捷键，可以根据个人爱好去设置，只要不和其他快捷键冲突即可。

#### 配置

- 界面

    可以根据个人爱好去选择使用哪些按钮

- 文件名编辑器

    可以设置自动生成的文件名，比如我的是 `%Y-%m-%d_%H-%M-%S` 可以按照 `2018-01-16_10-13-58` 这种格式生成截图名称

## 使用

可以通过上面任意方式启动截图，启动后会出现下面界面

![示意图](https://github.com/lupoDharkael/flameshot/raw/master/img/appPreview/animatedUsage.gif)

使用方法：

和 QQ 截图类型，包括矩形、椭圆等选项。

快捷键：

- ESC 退出截图（不保存）

- CTRL + C 保存到剪切板，可以将结果复制到其他文本编辑器，如 wps office 等。

- CTRL + S 保存图片，如果配置了默认目录（-p 参数）就直接保存，如果没有配置，会出现一个选择目录的步骤。

- CTRL + Z 回退

- 鼠标右键 可以选择颜色

- 滚轮 可以定义边框、箭头等宽度

## 不足

也有一个不太好的地方，就是现在还不支持输入文字，不知道未来更新会不会加上，不过现在也已经比 Ubuntu 和 Gnome 自带的截图工具强了很多了，除了文字，个人觉得比 QQ 截图也强大。


