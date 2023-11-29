---
layout: "post"
title: "Nginx"
date: "2020-2-1 14:44"
categories: Nginx
tags: [Computer Language, Nginx]
---

# Nginx背景

Nginx与Apache一样都是一种WEB服务器。基于REST架构风格，以统一资源描述符（Uniform Resoucrces Identifier）URI或者统一资源定位符(Uniform Resources Locator)URL作为共同一句，通过HTTP协议提供各种网络服务。

`REST架构风格`: 架构的一种编码规范

普通的请求格式为： 域名:端口号/接口地址 e.g. http://ip:port/queryUserInfo?id=1

使用REST风格的请求方式： http://ip:port/queryUserInfo/1

`Apache`

优点： 稳定 开源 跨平台

缺点: 重量级 不支持高并发 运行数以万计的并发访问会导致服务器消耗大量内存

# Nginx概述

- 高性能的HTTP和反向代理web服务器，轻量级

- 提供IMAP/POP3/SMTP服务

- 发布于2004年10月4日(第一个公开版本为0.1.0)，稳定版1.4.0与2013年4月24日发布，选择1.4.0之后的版本使用

- 由C语言编写

- 跨平台服务器

- Nginx有自己的函数库，并且除了zlib PCRE 和OpenSSL之外，标准模块只使用系统库C库函数，如不需要或考虑到潜在的授权冲突，可以不使用这些第三方库

# Nginx优势

- 占有内存少，在3w并发的连接中，开启10个nginx进程消耗内存大约为150M

- 处理高并发能力强，官方测试能支持5w并发连接

- 简单，配置文件通俗易懂

- 免费、开源

- 支持Rewriter重写，能根据域名、URL的不同，将HTPP请求分到不同的后端服务器群组

- 内置健康检查，如果nginx后端有几个服务器宕机了，不会影响前端访问，能自动检测服务状态

- 节省带宽，支持GZIP压缩，可以添加浏览器本地缓存的Header头

- 稳定性高，反向代理，很少宕机

# Nginx应用场景

## 功能与应用场景

- web服务器、轻量级 —— 充当代理服务器

- 负载均衡 —— IP负载、静态负载

- 支持缓存 —— 动静分离

- 能处理高并发 —— 限流、健康监控


# Linux下Nginx安装(未跟着操作，此段先跳过)

# Nginx命令(Linux环境下)

## 启动Nginx

`cd sbin/` 切换到安装目录下的`/sbin`目录，该目录下有`nginx`的命令

`./nginx` 直接运行`nginx`命令

### 查看Nginx是否启动成功

方法1： `ss -tanl` 

    查看正在运行的端口号，找到nginx默认端口号`80`，若`80`端口正常启动，表示Nginx启动成功

方法2： `ps -ef|grep nginx`

    查看nginx的进程，若启动成功则会出现两个nginx进程，master为主进程，负责接收请求；worker为子进程，负责转发请求

方法3： 在浏览器中输入`服务器ip`,若访问不到，可能是因为当前机器无法访问服务器，若服务器本地访问不到端口，应先开启端口 (虚拟机的防火墙需要通过80端口，自己的电脑关闭防火墙)

        开启端口: `/sbin/iptables -I INPUT -p tcp --dport -j ACCEPT`
        
        若端口开启后依旧访问不到，则需要关闭本地防火墙

出现`Welcome to nginx!`界面则表示启动成功

## 停止Nginx

使用 `./nginx -s stop` 或 `./nginx -s quit`命令都能停止运行

- `./nginx -s stop` 先查出nginx的进程id再使用kill命令强制杀掉进程

- `./nginx -s quit` 待nginx进程处理任务完毕进行停止

## 重启nginx

`./nginx -s reload`

# Nginx配置文件

打开配置文件夹中的`nginx.conf`文件，默认的配置文件中包含三个大模块：

- 基础全局模块： 

        ```conf
        #user  nobody;
        # nginx进程数，建议设置为CPU总核心数，默认为1
        worker_processes  1;

        # 定义全局错误日志类型 [debug | info | notice | warn | error | crit]
        #error_log  logs/error.log;
        #error_log  logs/error.log  notice;
        #error_log  logs/error.log  info;

        # 进程pid文件，指定nginx进程运行文件存放地址
        #pid        logs/nginx.pid;

        # 最大打开文件数连接,连接上限，与工作模式相关
        worker_rlimit_nofile 65535;
        ```

- 事件模块(events)

用于配置网络模块，网络信息

        ```conf
            events {
                # 单个进程最大连接数 最大连接数=连接数*进程数
                worker_connections  1024;

                # 网络连接超时时间，默认为60s
                keepalive_timeout 60;

                # 头部信息的缓存大小
                client_header_buffer_size 4k;
            }
        ```

- 请求(http)模块

```conf

    http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
		
        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
	
	server {
        listen       9000;
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```

## 核心模块

1. HTTP模块(代理、缓存、日志定义和第三方模块)
2. EVENTS模块(网络连接)
3. 全局模块(全局指令，日志路径，PID路径，用户信息等)

### HTTP模块子模块

```conf

    http {
    
    #### 全局模块 

    # 文件扩展名与文件类型映射表
    include       mime.types;

    # 默认的文件类型(stream流类型、text类型、XML、HTML等，默认为字符流)
    default_type  application/octet-stream;

    # 默认编码 默认为utf-8
    # charset utf-8;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    

    #### FASTCGI模块 用于改善网络性能，减少资源占用，提高访问速度

    # fastcgi_connect_timeout 300;
    # fastcgi_send_timeout 300;
    # fastcgi_read_timeout 300;

    #### Gzip模块 

    # 默认关闭压缩模式
    #gzip  on;

    #### server模块，虚拟主机模块，一个http可以含有多个server
    server {
        # 监听端口
        listen       80;

        # 域名可以有多个， 用空格隔开
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;
		
        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }
	
	server {
        listen       9000;
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```

## 代理模式

正向代理、反向代理、透明代理

Ngnix下载安装后默认为正向代理，但Nginx最常用的是反向代理，因此需要手动配置。

Nginx配置中，若`http`模块配置了`upstream servermap`则表示反向代理，无则为正向代理，默认为无。

# Nginx集群搭建

1. 搭建三台tomcat服务器及一台代理服务器nginx，并保证分别可以单独访问

2. 配置nginx
    - `cp nginx.conf nginx.conf.bak` 

        备份`nginx.conf`文件，命名为`nginx.conf.bak`

    - `vi nginx.conf` 修改`nginx.conf`文件

    在`nginx.conf`文件中的`http`模块中添加反向代理配置： 

    a. 配置服务器

        ```conf

            ...
            http {
                # 将请求转发到以下配置中的服务器中
                upstream localhost {
                    server 第一台服务器的ip或域名;
                    server 第二台服务器的ip或域名;
                    server 第三台服务器的ip或域名;
                }
            }

        ```
    
    b. 修改默认重定向地址

        ```conf

            ...
            http {
                # 将请求转发到以下配置中的服务器中
                upstream localhost {
                    server 第一台服务器的ip或域名;
                    server 第二台服务器的ip或域名;
                    server 第三台服务器的ip或域名;
                }
                ...
                server {
                    listen 80;
                    server_name localhost;

                    location / {
                        # root html;
                        # index index.html index.htm;

                        # 添加请求代理配置
                        proxy_pass http://localhost;
                    }
                }
            }

        ```

    `proxy_pass`和`updstream`后面跟的都是`server_name`,即上述改动中，浏览器访问`http://localhost:80`时，会先找到代理配置` proxy_pass http://localhost;`,再根据`upstream`中`server_name`为`localhost`的配置启动对应的服务器。

3. 修改完`nginx.conf`文件后需要重启`nginx`

# Nginx负载均衡

Nginx支持的负载策略： 轮询法(默认)、加权轮询法(权重法)、源地址哈希法、最小连接数法、第三方法则(Fair、url_hash)

## 轮询法

将请求按照顺序轮流分配到后端服务器上，均衡地对待后端的每一台服务器，不关心服务器实际的连接数和当前的系统负载

```conf
    upstream localhost {
        server 192.168.1.1:8080 weight=1;
        server 192.168.1.2:8080 weight=1;
        server 192.168.1.3:8080 weight=1;
    }

```

上述配置中`weight`表示权重，值越大表示权重越高，接收请求的几率越大，连接数越多。`weight`相同时，还是轮询法，可不写`weight`

## 加权轮询法(weight)

性能比较强的服务器可以将`weight`值调高一点

    ```conf
        upstream localhost {
            server 192.168.1.1:8080 weight=10;
            server 192.168.1.2:8080 weight=3;
            server 192.168.1.3:8080 weight=1;
        }
    ```

## 源地址哈希法

Nginx获取客户端的IP地址，通过哈希函数计算得到一个数值，用该数值对服务器列表的个数进行取模运算，得到的结果便是客户端要访问服务器的序号，同一个ip地址最终计算出来的后端服务器的序号是一致的。

哈希法可以保证同一个ip的请求被打到固定的机器上，可以解决集群模式下session共享问题：

    ```conf
        upstream localhost {
            # 使用哈希法
            ip_hash;
            server 192.168.1.1:8080 weight=1;
            server 192.168.1.2:8080 weight=1;
            server 192.168.1.3:8080 weight=1;
        }
    ```

## 最小连接数法

由于后台服务器配置不尽相同，对于请求的速度有快有慢，最小连接数法根据后台服务器当前的连接情况，动态地选取其中当前积压连接数最少的一台服务器来处理当前的请求，尽可能地提高后端服务的利用率，合理分流到每台服务器。

    ```conf
        upstream localhost {
            # 使用最小连接数法
            least_conn;
            server 192.168.1.1:8080 weight=1;
            server 192.168.1.2:8080 weight=1;
            server 192.168.1.3:8080 weight=1;
        }
    ```

## 第三方模块算法

### 第三方模块的下载和安装

#### Fair插件安装

- 下载地址： https://github.com/gnosek/nginx-upstream-fair

- 解压zip

- 增加模块: `./configure --prefix=/opt/nginx --add-module=/opt/nginx-upstream-fair-master`

- default_port问题修改： `cd nginx-upstream-fair-master`

- `sed -i 's/default_port/no_port/g' ngx_http_upstream_fair_module.c`

- `make`

- `make install`

#### hash插件安装

- 下载地址: https://github.com/evanmiller/nginx_upstream_hash

- 解压zip

- 增加模块 `./configure --prefix=/opt/nginx --add-module=/opt/nginx-upstream-hash-master`

- `make`

- `make install`

**此算法在Nginx1.7.2版本中已被废弃**

### Fair

- 比weight、ip_hash更智能的负载均衡算法

- 可根据页面大小和加载时间长短智能地进行负载均衡，根据后台服务器响应时间来分配请求，相应时间段的优先分配

- Nginx本身不支持fair，需要安装upstream_fair模块

    ```conf
    upstream localhost {
            # fair
            fair;
            server 192.168.1.1:8080 weight=1;
            server 192.168.1.2:8080 weight=1;
            server 192.168.1.3:8080 weight=1;
        }
    ```

### url_hash

**此算法在Nginx1.7.2版本中已被废弃**

根据访问的URL的哈希结果来分配请求，使每个URL定向到一台后端服务器，可进一步提高后端缓存服务器的效率，使用此算法时，与`Fair`一样先安装第三方插件

    ```conf
    upstream localhost {
            # url_hash
            hash $request_uri;
            server 192.168.1.1:8080 weight=1;
            server 192.168.1.2:8080 weight=1;
            server 192.168.1.3:8080 weight=1;
        }
    ```