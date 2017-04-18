---
layout: post
title: 'Ubuntu 16.10 编译安装 Mysql5.7'
date: '2017-04-18'
header-img: "img/post-bg-unix.jpg"
tags:
    - Mysql
author: 'Bro Qiang'
---

## Ubuntu 16.10 编译安装 Mysql5.7

Ubuntu 下快速安装直接 apt 方式即可, 一般的开发环境也足够了

个人比较喜欢新版本,一般有新版本就会尝试一下

此文档也使用CentOS,只是依赖关系部分不同,其他全部相同, 依赖部分写了,不过注释了

### 安装前准备

- 获取 Mysql

    当前的最新版本是 5.7.18 ,有了集成 boost 的版本, 这个比较友善 5.7.17 的时候还要单独去下载 80M 左右的 boost

    ```shell
    # 下载源码包
    $ wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-boost-5.7.18.tar.gz

    # 解压到src
    $ sudo tar xzvf mysql-boost-5.7.18.tar.gz -C /usr/local/src/

    # 修改权限
    $ sudo chown bro:bro /usr/local/src/mysql-5.7.18

    ```

- 安装依赖关系

    ```shell
    # 安装开发工具包, 一般默认就会已经安装了
    $ sudo apt install -y build-essential cmake libncurses5-dev bison

    # CentoOS 用下面方式安装依赖关系
    # $ sudo yum install gcc gcc-c++ cmake bison bison-devel ncurses ncurses-devel autoconf
    ```

- 创建守护进程用户

    ```shell
    $ sudo useradd -M -s /sbin/nologin mysql
    ```

### 编译安装

此处只配置了常规参数，更多参数请看 [官方参数说明](https://dev.mysql.com/doc/refman/5.7/en/source-configuration-options.html)

```shell
# 进入到之前解压的源码包目录
$ cd /usr/local/src/mysql-5.7.18/

# 创建编译后的代码保存位置
$ sudo mkdir build
$ cd build

# cmake 创建make需要的文件（makefile等）
# 参数说明
# -DCMAKE_INSTALL_PREFIX= 指定安装目录
# -DEFAULT_CHARSET= 指定默认字符集，如果不设置，安装完成后也可以配置
$ sudo cmake .. -DCMAKE_INSTALL_PREFIX=/usr/local/mysql -DDEFAULT_CHARSET=utf8mb4 \
    -DWITH_BOOST=/usr/local/src/mysql-5.7.18/boost/boost_1_59_0 -DMYSQL_DATADIR=/data/mysql/data

# 编译
$ make

# 安装到 /usr/local/mysql
$ make install

```

### 配置环境变量

非必须，不过不配置的话以后就都要绝对路径执行mysql命令……

可以配置全局, 也可以配置当前用户, 我一般配置全局, 因为习惯平时使用普通用户, 会和root用户sudo或者su

```shell
# 在 /etc/profile.d 下创建一个mysql用的配置文件
# 建议不要直接写在/etc/profile 中, 功能上没有区别, 不过配置多了之后可读性差点
$ sudo vim /etc/profile.d/mysql.sh

# 写入下面内容
export MYSQL_PATH=/usr/local/mysql
export PATH=$PATH:$MYSQL_PATH/bin

$ source /etc/profile.d/mysql.sh
```

### 编辑配置文件

可以直接放在`/etc/my.cnf`, 也可以 `/etc/mysql/my.cnf`

此处选择的第三种方式,个人比较喜欢所有和mysql相关的都放在一个目录下, 方便查找和备份

```shell
# 在mysql根目录下新建一个etc目录
$ sudo mkdir /usr/local/mysql/etc

# 创建my.cnf文件
$ sudo vim /usr/local/mysql/etc/my.cnf

# 写入下面内容


[client]

[mysqld]
basedir=/usr/local/mysql
datadir=/data/mysql/data
socket=/tmp/mysql.sock
character_set_filesystem = utf8mb4
character_set_server = utf8mb4
symbolic-links=0

log-error=/data/mysql/log/mysqld.log
pid-file=/data/mysql/run/mysqld.pid
```

### 初始化数据库

需要注意:  

- MySQL 5.7.6 之前, 可以使用 mysql_install_db 初始化数据库

- MySQL 5.7.6 之后, 就需要使用  mysqld with the --initialize or --initialize-insecure 初始化


```shell
# 创建数据仓库目录
$ sudo mkdir -p /data/mysql/data/

# 创建日志目录
$ sudo mkdir -p /data/mysql/log/

# 创建保存 PID 目录
$ sudo mkdir -p /data/mysql/run/

# 将 mysql 目录权限改成 mysql 用户
$ sudo chown -R mysql:mysql /data/mysql

# 初始化, 需要注意,配置文件及目录一定要正确
$ sudo /usr/local/mysql/bin/mysqld --defaults-file=/usr/local/mysql/etc/my.cnf  --initialize --user=mysql

```

### 配置 Mysql 自启动服务


```shell
# 复制启动脚本到init.d下
$ sudo cp mysql.server /etc/init.d/mysqld

# 启动服务
$ sudo /etc/init.d/mysqld start

# 停止服务
$ sudo /etc/init.d/mysqld stop

# 配置开机自动启动
$ sudo systemctl enable mysqld
```

### 配置root@localhost用户

Mysql 5.7 开始,初始化数据库之后不再是空的root密码,而是在日志文件中写入一个随机密码

安装完之后需要想默认给的密码修改

```shell
# 查询默认密码, root@localhost: 后面是密码
$ sudo grep 'root'@'localhost' /data/mysql/log/mysqld.log 

# 用查询到的用户登录密码 mysql
$ /usr/local/mysql/bin/mysql -uroot -p

mysql> ALTER USER root@localhost IDENTIFIED BY '1';

# 如果是5.7.6以前版本是下面方式
mysql> SET PASSWORD FOR user = PASSWORD('new_password');

# 测试,执行下面语句,可以查询出用户,配置正确
mysql> select user,host from mysql.user;

# 顺便查询一下字符集, 看看配置文件中的配置是否生效
mysql> show variables like '%char%';
# 正常应该显示下面结果
+--------------------------+----------------------------------+
| Variable_name            | Value                            |
+--------------------------+----------------------------------+
| character_set_client     | utf8                             |
| character_set_connection | utf8                             |
| character_set_database   | utf8mb4                          |
| character_set_filesystem | utf8                             |
| character_set_results    | utf8                             |
| character_set_server     | utf8mb4                          |
| character_set_system     | utf8                             |
| character_sets_dir       | /usr/local/mysql/share/charsets/ |
+--------------------------+----------------------------------+
8 rows in set (0.01 sec)

```
