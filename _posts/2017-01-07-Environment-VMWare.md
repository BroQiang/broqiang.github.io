---
layout: post
title: 'VMWare 虚拟机安装'
date: '2017-01-07'
header-img: "img/post-bg-unix.jpg"
tags:
    - Environment
author: 'Bro Qiang'
---


## VMware Workstation 虚拟机安装

## 虚拟机软件介绍

- [ VMWare Workstation](http://www.vmware.com/cn/products/workstation/workstation-evaluation.html) 
    个人认为最强大的，不过要收费，可以试用，支持Windows和Linux

    License: `5A02H-AU243-TZJ49-GTC7K-3C61N` ,此 Key 源自 [Baidu](https://zhidao.baidu.com/question/1240914582586009779.html), 测试后请及时删除

    此处就是以此软件进行讲解

- [Oracle VM VirtualBox](https://www.virtualbox.org/) 
    开源产品，支持Windows/Linux/Mac OS X

- 还有一些，比如KVM/Hyper-V等，其他产品没有使用过，在此就不提了


[VMware 官网](http://www.vmware.com/cn.html)

## 获取软件

- [VMware Workstation 12 Pro for Windows（64 位）](https://download3.vmware.com/software/wkst/file/VMware-workstation-full-12.5.5-5234757.exe)

- [VMware Workstation 12 Pro for Linux（64 位）](https://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-12.5.5-5234757.x86_64.bundle)

    如果地址失效，直接去 [官网](http://www.vmware.com/cn.html) 手动找到链接下载即可

## 软件安装

- Window 双击刚刚下载的`VMware-workstation-full-12.5.5-5234757.exe` 文件，一直下一步，直到完成

- Linux 先给下载下来的文件添加执行权限，然后再执行安装文件

    打开一个终端`Ctrl+Shift+t`,找到下载文件目录，如果没选择的话默认会下载到`Downloads`目录

    ```shell
    $ cd ~/Downloads
    $ chmod +x VMware-Workstation-Full-12.5.5-5234757.x86_64.bundle
    $ sudo ./VMware-Workstation-Full-12.5.5-5234757.x86_64.bundle
    ```

    然后基本也是一路下一步，直到完成

## 配置虚拟机

- 双击虚拟机软件，打开软件，输入`Ctrl+n` （也可以再菜单中找到新建虚拟机）

- 选择Custom，点击下一步

- 选择虚拟机版本，默认即可，下一步

- 选择安装镜像，暂时先不选，（选择也没关系，这个随时可以更改）选择稍后安装操作系统

- 选择客户机操作系统

    选中Linux，在下拉列表中选中`Ubuntu 64-bit` (此处根据实际的操作系统去选择即可，本文档是Ubuntu)

- 设置虚拟机名称

    名字随意取，不过建议不要使用中文，最好起的有点具体含义，方便以后虚拟机多了之后进行区分，如`Ubuntu16.10_64-Develop`

    第二行是虚拟机保存的位置，

    Windows推荐放在一个较大的分区， 只要空间够即可

    Linux也推荐放在较大的分区，最后是家目录,如`/Home/user/vmware/VirtualMachine` （user是当前登录用户名）,如果目录不存在，创建即可 `$ mkdir -p /home/user/vmware/VirtualMachine`

- 选择Cpu

    建议和物理Cpu对应，一般PC都是一颗Cpu，4或8核心，此处就选择1颗Cpu，n核（n<=物理核数)

- 内存选择

    内存不要超过软件提示的最大推荐内存即可，不过建议给宿主机多留些内存，分配虚拟机够用即可，如4G

- 网络选择

    选择第一个，桥接网络（此种方式连接可以通过虚拟路由，为虚拟机单独分配一个IP）

- IO控制器类型，默认即可

- 磁盘类型，默认即可

- 磁盘，选择创建一个新的磁盘（第一个选项）

- 分配磁盘
    磁盘空间，如果只是安装测试的Ubuntu，分配20G就够用，不过后期有可能会安装一些软件和项目，推荐40G

    立即分配磁盘空间，如果磁盘空间有限就不要勾选（不勾选会动态使用磁盘，比如分配了20G，但实际可能只会用5G，勾选后会立即占用磁盘，理论上会使得虚拟机运行快一些，不过实际使用中感觉不明显，推荐不勾选）

    下面推荐选择单一虚拟磁盘，倒数第二个选项（方便未来复制和备份虚拟机）

- 选择磁盘文件

    这个是虚拟磁盘的保存位置，默认会放到之前选择的`Virtual Machine`中，也可以根据需要指定位置，一般默认即可

- 点击完成，虚拟机创建完成

## 选择操作系统镜像

如果前面选择安装镜像，选择稍后安装操作系统，此处选择，如果已经选择了，可以忽略此部

- 在虚拟机配置界面，选择编辑虚拟机配置

- 选中`CD/DVD`

- 选择右侧的使用ISO镜像

- 选择镜像即可（镜像的获取在下一节介绍）
 
