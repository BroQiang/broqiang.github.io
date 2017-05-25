---
layout: post
title: 'Linux 编译安装 Nginx 1.12'
date: '2017-04-18'
header-img: "img/post-bg-unix.jpg"
tags:
     - Nginx
author: 'Bro Qiang'
---

## Linux 编译安装 Nginx 1.12

当前最新稳定版本: 1.12

[官网](http://nginx.org/)

### 获取软件

```shell
# 下载当前最新稳定版
$ wget http://nginx.org/download/nginx-1.12.0.tar.gz

# 解压到src目录
$ sudo tar xzvf nginx-1.12.0.tar.gz -C /usr/local/src/
```

### 解决依赖关系

```shell
# Ubuntu 执行下面命令
$ sudo apt install -y libpcre3-dev zlib1g-dev libssl-dev

# CentOS 执行下面命令
# $ sudo yum install -y pcre-devel openssl-devel zlib-devel
```

### 创建守护进程用户

如果安装 PHP 的时候已经创建了,此步骤忽略

```shell
$ sudo useradd -M -s /sbin/nologin www
```

### 编译安装

参数多数用了默认的, 如果有特殊需求,可以查看 [官方参数配置](http://nginx.org/en/docs/configure.html)

```shell
# 进入到解压后的源码目录
$ cd /usr/local/src/nginx-1.12.0/

# 配置
sudo ./configure --prefix=/usr/local/nginx --user=www --group=www --with-select_module \
    --with-poll_module --with-http_ssl_module --with-pcre --with-pcre-jit --with-zlib= \
    --pid-path=/usr/local/nginx/run/nginx.pid

# 编译 & 安装
$ sudo make
$ sudo make install
```

### 配置自动启动

```shell
# 新建 service 文件
$ sudo vim /lib/systemd/system/nginx.service

# 写入下面内容
[Unit]
Description=nginx - high performance web server
Documentation=http://nginx.org/en/docs/
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/run/nginx.pid
ExecStartPre=/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target

# 配置开机自动启动
$ sudo systemctl enable nginx

# 启动服务
$ sudo systemctl start nginx

# 停止服务
$ sudo systemctl stop nginx
```

### nginx.conf 配置

简单配置了下,进行了一些基本的优化

这个只是最初步的优化,真实环境要根据实际情况去优化

实际生产中各种原因都会影响性能,有时候并不是参数给的高性能就会提高

这个里面的参数要根据实际的服务器配置,并发访问情况等去优化,很难一步到位的

```shell
# 修改配置前先将原本的备份一份, 要养成良好习惯,因为谁也不能保证自己的修改就是 100% 正确, 必要时候要能够还原
$ cd /usr/local/nginx/conf/
$ sudo mv nginx.conf nginx.conf_20170418_bak

$ sudo vim /usr/local/nginx/conf/nginx.conf
```

将默认的内容全部删除,写入下面内容

```shell
# 守护进程用户
user  www;

#启动进程,通常设置成和cpu的数量相等
worker_processes  8;

events {
    # epoll是多路复用IO(I/O Multiplexing)中的一种方式,
    # 仅用于linux2.6以上内核,可以大大提高nginx的性能
    use   epoll;

    # 单个worker process进程的最大并发链接数
    # 并发总数理论值是 worker_processes 和 worker_connections 的乘积
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;


    # sendfile 指令指定 nginx 是否调用 sendfile 函数（zero copy 方式）来输出文件
    # 对于普通应用，必须设为 on, 下载等高 IO 的服务可以设置成 off
    sendfile        on;

    # 连接超时时间
    keepalive_timeout  120;

    # 是否开启gzip压缩
    gzip  on;

    # 设定请求缓冲
    client_header_buffer_size    128k;
    large_client_header_buffers  4 128k;


    # 将默认的 server 删除,全部通过 conf.d 引入,按照功能将配置分开

    include conf.d/*.conf;
}

```

### 配置 server (虚拟主机)

```shell
# 创建 虚拟主机存放目录 目录名称就是上面配置文件中 include 的目录
$ sudo mkdir /usr/local/nginx/conf/conf.d

# 进入刚刚引入的 conf.d 目录
$ cd /usr/local/nginx/conf/conf.d

# 有新的虚拟主机就再创建一个 xxx.conf 即可
$ sudo vim test.conf
```


写入下面内容


```shell

server {
    
    listen       80; # 端口,一般http的是80
    server_name  localhost; # 一般是域名,本机就是localhost
    index index.php index.html;  # 默认可以访问的页面,按照写入的先后顺序去寻找
    root  /home/bro/test; # 项目根目录

    # 防止访问版本控制内容
    location ~ .*.(svn|git|cvs) {
        deny all;
    }

    # 此处不是必须的,需要时候配置
    location / {
        # Thinkphp 3.2 Url 重写
        if (!-e $request_filename){
            rewrite ^/(.*)$ /index.php/$1 last;
        }

        # Laravel 5.4 Url 重写
        try_files $uri $uri/ /index.php?$query_string;
    }


    # 下面是所有关于 PHP 的请求都转给 php-fpm 去处理
    location ~ \.php {

        # 注意： unix sock 和 ip ，两种方式只能选择一种

        # 基于unix sock 访问,Ubuntu Apt 方式安装的PHP默认是以sock方式启动
        # fastcgi_pass    unix:/run/php/php7.0-fpm.sock;

        # 基于IP访问
        fastcgi_pass    127.0.0.1:9000;

        fastcgi_split_path_info ^(.+\.php)(.*)$;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include         fastcgi_params;
    }

    fastcgi_intercept_errors on;
    # 日志保存目录,一般按照项目单独保存, 开发环境就无所谓了
    #access_log  logs/localhost_access.log access; 
}

```

