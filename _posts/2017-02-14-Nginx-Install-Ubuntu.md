---
layout: post
title: 'Ubuntu apt 方式安装 Nginx'
date: '2017-02-14'
header-img: "img/post-bg-unix.jpg"
tags:
    - Nginx
author: 'Bro Qiang'
---

## Ubuntu apt 方式安装 Nginx

```shell
$ sudo apt install -y nginx
```

### 启动/停止服务

```shell
# 启动服务
sudo systemctl start nginx

# 停止服务
sudo systemctl stop nginx

# 重启服务
sudo systemctl restart nginx
```

### Vitrual host demo

```shell
server {
    listen       80;
    server_name  localhost;
    index index.php index.html;
    root  /home/bro/www/localhost;

    location ~ .*.(svn|git|cvs) {
        deny all;
    }

    location / {
        # Thinkphp 3.2 Url 重写
        if (!-e $request_filename){
            rewrite ^/(.*)$ /index.php/$1 last;
        }

        # Laravel 5.4 Url 重写
        try_files $uri $uri/ /index.php?$query_string;
    }



    location ~ \.php {

        # 注意： unix sock 和 ip ，两种方式只能选择一种

        # 基于unix sock 访问,Ubuntu Apt 方式安装的PHP默认是以sock方式启动
        fastcgi_pass    unix:/run/php/php7.0-fpm.sock;

        # 基于IP访问
        # fastcgi_pass    127.0.0.1:9000;

        fastcgi_split_path_info ^(.+\.php)(.*)$;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include         fastcgi_params;
    }

    fastcgi_intercept_errors on;
    #access_log  logs/localhost_access.log access;
}

```