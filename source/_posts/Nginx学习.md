---
title: Nginx学习
date: 2023-11-12 14:06:47
tags: Nginx
categories: 学习
---

# 1.Nginx 简介

## 1.1 什么是 Nginx

Nginx (engine x) 是一个高性能的 HTTP 和反向代理 web 服务器，同时也提供了 IMAP/POP3/SMTP 服务。

其将源代码以类 BSD 许可证的形式发布，因它的稳定性、丰富的功能集、简单的配置文件和低系统资源的消耗而闻名。

Nginx 是一款轻量级的 Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，在 BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实上 nginx 的并发能力在同类型的网页服务器中表现较好。

Nginx 专为性能优化而开发，性能是其最重要的考量，实现上非常注重效率，能经受高负载的考验，有报告表明能支持高达 50000 个并发连接数。

## 1.2 正向代理

Nginx 不仅可以做反向代理，实现负载均衡。还能用作正向代理来进行上网等功能。

正向代理:如果把局域网外的 Internet 想象成一个巨大的资源库，则局域网中的客户端要访问 Internet，则需要通过代理服务器来访问，这种代理服务就称为正向代理。·

![](/images/正向代理.png)

## 1.3 反向代理

反向代理，其实客户端对代理是无感知的，因为客户端不需要任何配置就可以访问，我们只需要将请求发送到反向代理服务器，由反向代理服务器去选择目标服务器获取数据后,在返回给客户端，此时反向代理服务器和目标服务器对外就是一个服务器，暴露的是代理服务器地址，隐藏了真实服务器 IP 地址。

![](/images/反向代理.png)

## 1.4 正向代理和反向代理的异同

**相同点**

正向代理和反向代理所处的位置都是客户端和真实服务器之间，所做的事情也都是把客户端的请求转发给服务器，再把服务器的响应转发给客户端。

**不同点**

正向代理是客户端的代理，服务器不知道真正的客户端是谁；反向代理是服务器的代理，客户端不知道真正的服务器是谁

正向代理一般是客户端架设的；反向代理一般是服务器架设的

正向代理主要是用来解决访问限制问题；反向代理则是提供负载均衡、安全防护等作用。二者都能提高访问速度

## 1.5 通过故事理解正向代理和反向代理

**（正向代理）**

同学 A 急需一笔钱，他直接向富豪马云借钱，但是他俩之间毫无关系，结果当然是没有借到。经过一番打听，同学 A 的老师王先生是马云的好朋友，于是 A 同学请求王老师，让王老师帮忙向马云借钱，最终马云同意借钱给王老师，王老师把这笔钱转交给了 A 同学。

上文就相当于一个正向代理的过程，A 同学为客户端，马云为服务器，王老师为正向代理。A 同学请求王老师向马云借钱，这个过程中 A 同学隐藏了自己的角色，马云事实上是不知道到底是谁借的钱。相当于服务器不知道真正发起请求的客户端是谁。

**（反向代理）**

如果遇到困难需要拨打 10086 客服电话，可能一个地区的 10086 客服有几十个，但是我们不需要关心电话那头的人是谁。只需要拨通 10086 的总机号码，电话那头总有客服会回应。

这里的 10086 总机号码就相当于反向代理，客户端不知道真正提供服务的人是谁。

## 1.6 负载均衡

负载均衡，顾名思义就是将负载分摊到多个系统中进行处理，达到均衡的状态。

随着互联网不断发展，网站的访问量也在不断增加。如果只依靠单台服务器进行处理，可能会遇到瓶颈，导致整个网站崩溃。而采用负载均衡的方式，可以将负载分摊到多台服务器上进行处理，提高整个系统的稳定性和吞吐量。

另外，负载均衡还可以提高网站的可用性。在某些情况下，某些服务器可能出现故障，无法正常工作。但是采用负载均衡的方式，可以将故障服务器的负载转移到其他正常的服务器上，确保网站一直处于可用状态。

## 1.7 动静分离

动静分离是指在 web 服务器架构中，将静态页面与动态页面或者静态内容接口和动态内容接口分开不同系统访问的架构设计方法，进而提升整个服务访问性能和可维护性。

# 2.Nginx 的安装

## 2.1 基本安装与启动

1）使用远程连接工具连接 linux 操作系统

2）https://nginx.org/

3）安装 nginx

把安装压缩文件放到 linux 系统中

解压缩 nginx-xx.tar.gz 包`tar -xvf nginx-xx.tar.gz`

进入解压缩目录,执行`./configure`

4）nginx 相关素材（依赖）

**安装 gcc**

yum install -y gcc

**安装 perl 库**

yum install -y pcre pcre-devel

**安装 zlib 库**

yum install -y zlib zlib-devel

**执行命令`./configure --prefix=/usr/local/nginx`**

接下来执行：

`make && make install`

安装成功之后,在/usr 下多出一个文件夹 local/nginx,在 nginx 里边有 sbin 有启动脚本

5）启动 nginx

进入/usr/local/nginx/sbin

```json
./nginx 启动
./nginx -s stop 快速停止
./nginx -s quit 优雅关闭,在退出前完成已经接受的连接请求
./nginx -s reload 重新加载配置
./nginx -v 查看版本号
```

6）关闭防火墙

`systemctl stop firewalld.service`

禁止防火墙开机启动

`systemctl disable firewalld.service`

重启防火墙

`firewall -cmd --reload`

浏览器再次访问,成功

![](/images/nginx.png)

## 2.2 安装成系统服务

创建服务脚本

`vi /usr/lib/systemd/system/nginx.service`

服务脚本内容

```[unit]
[Unit]
Description=nginx -  web server
After=network.target remote-fs.target nss-1ookup.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/logs/nginx.pid
ExecStartPre=/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
ExecStart=/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s stop
ExecQuit=/usr/local/nginx/sbin/nginx -s quit
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

重新加载系统服务

`systemctl daemon-reload`

查看先前启动的服务还在不在

`ps -ef | grep nginx`

关闭 nginx

`./nginx -s stop`

启动服务

`systemctl start nginx.service`

开机启动

`systemctl enable nginx.service`

查看状态

`systemctl status nginx.service`

# 3.Nginx 配置文件

nginx 配置文件位置：`/usr/local/nginx/conf/nginx.conf`

nginx 配置文件由三部分组成

## 第一部分：全局块

**从配置文件开始到 events 块之间的内容，主要会设置一些影响 nginx 服务器整体运行的配置指令**，主要包括配置运行 Nginx 服务器的用户(组)、允许生成的 worker process 数，进程 PID 存放路径、日志存放路径和类型以及配置文件的引入等。

比如上面第一行配置的：

`worker_processes  1;`

这是 Nginx 服务器并发处理服务的关键配置，**worker_processes 值越大，可以支持的并发处理量也越多**，但是会受到硬件、软件等设备的制约

## 第二部分：events 块

比如上面的配置：

`events {
    worker_connections  1024;
}`

**events 块涉及的指令主要影响 Nginx 服务器与用户的网络连接**，常用的设置包括是否开启对多 work process 下的网络连接进行序列化，是否允许同时接收多个网络连接，选取哪种事件驱动模型来处理连接请求，每个 word process 可以同时支持的最大连接数等。

**上述例子就表示每个 work process 支持的最大连接数为 1024**。

这部分的配置对 Nginx 的性能影响较大，在实际中应该灵活配置。

## 第三部分：http 块

```
http {
include mime.types;
default_type application/octet-stream;
sendfile on;
keepalive_timeout 65;
server {
listen 80;
server_name localhost;

        location / {
            root   html;
            index  index.html index.htm;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

}
```

这算是**Nginx 服务器配置中最频繁的部分**，代理、缓存和日志定义等绝大多数功能和第三方模块的配置都在这里。

需要注意的是:**http 块也可以包括 http 全局块、server 块**。

### ①http 全局块

http 全局块配置的指令包括文件引入、MIME-TYPE 定义、日志自定义、连接超时时间、单链接请求数上限等。

### ②server 块

这块和虚拟主机有密切关系，虚拟主机从用户角度看，和一台独立的硬件主机是完全一样的，该技术的产生是为了节省互联网服务器硬件成本。

每个 http 块可以包括多个 server 块，而每个 server 块就相当于一个虚拟主机。

而每个 server 块也分为全局 server 块，以及可以同时包含多个 locaton 块。

**1、全局 server 块**

最常见的配置是本虚拟机主机的监听配置和本虚拟主机的名称或 IP 配置。

**2、location 块**

一个 server 块可以配置多个 location 块。

这块的主要作用是基于 Nginx 服务器接收到的请求字符串（例如 server_name/uri-string )，对虚拟主机名称(也可以是 IP 别名)之外的字符串(例如前面的/uri-string)进行匹配，对特定的请求进行处理。地址定向、数据缓存和应答控制等功能，还有许多第三方模块的配置也在这里进行。
