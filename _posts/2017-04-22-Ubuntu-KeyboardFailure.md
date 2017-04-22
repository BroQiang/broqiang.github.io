---
layout: post
title: 'Ubuntu USB 键盘时好时坏解决'
date: '2017-04-22'
header-img: "img/post-bg-unix.jpg"
tags:
     - Ubuntu
author: 'Bro Qiang'
---

## Ubuntu 键盘时好时坏解决

键盘型号: 罗技（Logitech）MK275 无线光电键鼠套装 

主机是自己购买配件组装的兼容机

这个问题困扰很久了, 直到今天中午忍受不了了, 就去 google 啃英文了, 搜索到 [一篇文章](https://askubuntu.com/questions/772056/keyboard-stops-working-ubuntu-16-04)

给了我启发,大概意思就是 USB 自动挂起引起的, 禁用 USB 自动挂起即可解决.

我觉得我应该就是这个问题, 因为无线套装用的是一个USB接收器, 即使我键盘在用,但是鼠标没动,估计系统也给我判断为休眠了...



## 方式一

### 查找设备对应的电源选项

```shell

# 查看USB设置被识别的标识, 可以根据键盘型号去筛选下
$ sudo dmesg |grep Logitech

# 我的显示下面结果, 上面两行是键盘的, 下面两行是鼠标的(个人推断), 所以它们两个共用端口 1-7 
[    1.479458] input: Logitech USB Receiver as /devices/pci0000:00/0000:00:14.0/usb1/1-7/1-7:1.0/0003:046D:C534.0001/input/input6
[    1.536000] hid-generic 0003:046D:C534.0001: input,hidraw0: USB HID v1.11 Keyboard [Logitech USB Receiver] on usb-0000:00:14.0-7/input0
[    1.536144] input: Logitech USB Receiver as /devices/pci0000:00/0000:00:14.0/usb1/1-7/1-7:1.1/0003:046D:C534.0002/input/input8
[    1.596386] hid-generic 0003:046D:C534.0002: input,hiddev0,hidraw1: USB HID v1.11 Mouse [Logitech USB Receiver] on usb-0000:00:14.0-7/input1

# 如果不清楚键盘型号, 可以先执行下面这条命令确定键盘型号再去执行上面命令
# 还是不清楚关键字的话只能自己一行一行花点时间去找了
$ sudo dmesg |grep Keyboard

# 所以他对应的接口就是 1-7 , 查询一下
$ ls -l /sys/bus/usb/devices/1-7

# 结果,果然有, 找对了
lrwxrwxrwx 1 root root 0 4月  22 23:31 /sys/bus/usb/devices/1-7 -> ../../../devices/pci0000:00/0000:00:14.0/usb1/1-7


# 找到端口下的电源选项, 根据上面找到的端口,分别是 
$ ls /sys/bus/usb/devices/1-7/power

```

### 禁用自动挂起


```shell

# 可以查询下,默认的自动延时参数
$ cat /sys/bus/usb/devices/1-7/power/autosuspend_delay_ms

# 默认是 2000, 不清楚是秒还是毫秒, 将这个数值改成 -1, 就是禁用 自动延时, 此 usb 设备就不会自动省电了
$ sudo sh -c "echo -1 > /sys/bus/usb/devices/1-7/power/autosuspend_delay_ms"

```

### 配置开机自动执行

安装上面操作配置完成后, 下次重启还是会恢复成默认, 所以配置成开机自动执行

Ubuntu 16.10 默认已经没有了 rc.local 配置文件 , 自己写一个,并将上面的命令加入进去

```shell

# -- 创建 rc.local 脚本
$ sudo vim /etc/rc.local

# 写入下面内容

#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

echo -1 > /sys/bus/usb/devices/1-7/power/autosuspend_delay_ms

exit 0


# -- 配置 rc.local 服务

$ sudo vim /etc/systemd/system/rc-local.service

# 写入下面内容

[Unit]
Description=/etc/rc.local Compatibility
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target

# 配置开机自动启动
$ sudo systemctl enable rc-local.service

```


## 方式二

使用 Laptop Mode Tools - Linux 系统下的笔记本电源管理软件

```shell
# 安装软件
$ sudo apt install laptop-mode-tools

# 配置
$ sudo vim /etc/laptop-mode/conf.d/runtime-pm.conf

# 找到下面
AUTOSUSPEND_TIMEOUT=2
# 改成
AUTOSUSPEND_TIMEOUT=-1

# 不确定是否需要重启,我配置完了重启了
$ sudo reboot
```
