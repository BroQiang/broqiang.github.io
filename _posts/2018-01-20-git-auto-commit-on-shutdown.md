---
layout: post
title: 'Linux 关机时自动提交 git'
date: '2018-01-20'
header-img: "img/post-bg-unix.jpg"
tags:
     - PHP
author: 'Bro Qiang'
---

# Linux 关机时自动提交 git

有这个想法，是因为个人比较马虎，经常忘记提交代码，就导致在家中写完的代码第二天回到公司没法继续，导致晚上的工作就白费了，于是就冒出了这个自动提交git的想法。

原理很简单，自己写一个可以自动提交的脚本，在关机之前手动提交一次，最好的办法就是利用 Systemd，在关机的时候自动执行。

> 下面的内容原则上来说 CentOS7、Fedora、Ubuntu都可以实现，不过实测的只有 Ubuntu 17.10（因为我的开发环境是这个）

> 需要 git 手动提交过，并已经自动保存好了密码等信息

## 自动提交git的脚本

这个脚本可以实现手动执行提交，也可以通过关机时自动提交

```shell
#!/bin/bash
#
# 自动提交 git 脚本
# 2018-01-22 By BroQiang
#
# Update：
#   - 添加自动 pull ，配合 systemd 实现开机自动 pull 代码

root_dir="/home/bro/Repository/gitee /home/bro/Repository/Github"
commit_date=$(date +%Y-%m-%d_%H-%M-%S)
# 使用 git 仓库的普通用户
myuser="bro"

action=${1:-'stop'}

# 自动提交函数
for dir in ${root_dir}
do  
    for git_dir in $(ls ${dir})
    do  
        if [[ $UID -eq 0 ]]; then
            # 这里写的不优雅，原本想封装到函数中，但是不知道 su - bro -c 怎么调用函数……
            # 如果有人知道，可以告诉我 broqiang@qq.com，万分感谢了
            if [[ "$action" == "start" ]]; then
                /bin/su - ${myuser} -c "cd ${dir}/${git_dir};/usr/bin/git pull"
            fi

            if [[ "$action" == "stop" ]]; then
                /bin/su - ${myuser} -c "cd ${dir}/${git_dir};/usr/bin/git add ."
                /bin/su - ${myuser} -c "cd ${dir}/${git_dir};/usr/bin/git commit -m 'shell auto commit on '${commit_date}"
                /bin/su - ${myuser} -c "cd ${dir}/${git_dir};/usr/bin/git push"
            fi
        else
            cd ${dir}/${git_dir}
    

            if [[ "$action" == "start" ]]; then
                /usr/bin/git pull
            fi

            if [[ "$action" == "stop" ]]; then
                /usr/bin/git add .
                /usr/bin/git commit -m "auto commit on${commit_date}"
                /usr/bin/git push
            fi
        fi
    done
done
```

## 配置 Systemd 的 service

可以配置一个 Service 来实现关机时候自动执行上面的脚本，实现自动提交。

新建一个 Service

```shell
sudo vim /lib/systemd/system/git-auto-commit.service
```

写入下面内容

```shell
[Unit]
Description=Auto commit code on reboot and shutdown
Requires=network.target
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
#Type=simple
ExecStart=/home/bro/bin/git_auto_commit start

RemainAfterExit=true 

ExecStop=/home/bro/bin/git_auto_commit stop

[Install]
WantedBy=multi-user.target graphical.target

```

将 Service 开机自动启用

> 此步骤不要忘记，否则不能随着系统开机和关闭自动提交

```shell
sudo systemctl enable git-auto-commit
```

现在就可以重启查看效果了

```shell
reboot
```

## 更新记录

#### 2018-01-22

添加开机自动 pull 代码