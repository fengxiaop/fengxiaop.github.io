---
title: nginx搭建前端项目
date: 2021-10-12 10:52:08
tags: nginx前端
---

所需Xshell +Xtfp+服务器+ip

利用Xshell链接到服务器后

![image-](https://raw.githubusercontent.com/fengxiaop/gallery/master/image/Snipaste_2021-10-12_14-31-03.png)

点击之后会弹出xftp的窗口

![image-20211012100409206](https://github.com/fengxiaop/gallery/blob/master/image/image-20211012100409206.png?raw=true)

xtfp这软件上手很容易

只需要左右拖拽文件即刻互相传输

#### **1.首先在Xshell上利用yum工具下载nginx**

```
yum install nginx -y
```

#### **2.测试启动nginx** 

```
nginx
```

#### 3.配置nginx配置文件

```
1.进入/etc/nginx文件夹
cd /etc/nginx
2.编辑nginx.conf
vim nginx.conf
3.添加一个server
server实例：
server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        
        root         /usr/share/nginx/html;        #修改为root         /data/www;
        
        include /etc/nginx/default.d/*.conf;

        location / {
        }

        error_page 404 /404.html;
            location = /40x.html {
        }
        
        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

```

#### 4.贴上我自己的nginx.conf完整配置

```
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
    
    server {
        listen       8001 default_server;
        listen       [::]:8001 default_server;
        server_name  _;
        
        root         /usr/local/java/resources;        #修改为root         /data/www;
        
        include /etc/nginx/default.d/*.conf;

        location / {
        }

        error_page 404 /404.html;
            location = /40x.html {
        }
        
        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

# Settings for a TLS enabled server.
#
#    server {
#        listen       443 ssl http2 default_server;
#        listen       [::]:443 ssl http2 default_server;
#        server_name  _;
#        root         /usr/share/nginx/html;
#
#        ssl_certificate "/etc/pki/nginx/server.crt";
#        ssl_certificate_key "/etc/pki/nginx/private/server.key";
#        ssl_session_cache shared:SSL:1m;
#        ssl_session_timeout  10m;
#        ssl_ciphers HIGH:!aNULL:!MD5;
#        ssl_prefer_server_ciphers on;
#
#        # Load configuration files for the default server block.
#        include /etc/nginx/default.d/*.conf;
#
#        location / {
#        }
#
#        error_page 404 /404.html;
#            location = /40x.html {
#        }
#
#        error_page 500 502 503 504 /50x.html;
#            location = /50x.html {
#        }
#    }

}
```

其中8001端口为我的静态资源访问端口
/usr/local/java/resources 为我的静态资源存放位置

#### 5.重启nginx

```
nginx -s reload
```

#### 6.测试nginx静态资源访问是否成功

```
 例如：/usr/local/java/resources下有一个index.html文件
 访问则是：www.huhdcc.top:8001/index.html
```

如果还不能使用的话 是服务器没有开放端口问题  

进入阿里云

进入找到域名

添加一个子域名

![image-20211012104756836](https://github.com/fengxiaop/gallery/blob/master/image/image-20211012104756836.png?raw=true)

添加域名解析

![](https://github.com/fengxiaop/gallery/blob/master/image/image-20211012104811440.png?raw=true)

开放服务器端口

![image-20211012104914746](https://github.com/fengxiaop/gallery/blob/master/image/image-20211012104914746.png?raw=true)

