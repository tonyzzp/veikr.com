```toml
title = "安装xampp后apache正常启动 但无法访问localhost的解决办法"
slug = "xampp_apache_localhost"
description = ""
date = "2011-03-19 16:32:52"
author = "admin"
tags = ["apache","localhost","php","winsock","xampp","无法打开","解决办法"]
```

<p>&nbsp;文章概要:安装解压版的xampp后，apache显示正常启动了，但是localhost却无法访问。也排除了端口被占用的情况，那么要怎么样解决这个问题呢。&nbsp;安装xampp后apache显示正常启动，但是无法访问localhost。1.首先排除端口被占用的情况。使用netstat -ano命令查看80和443端口占用的进程ID，然后在任务管理器中查看该进程(菜单查看--显示列，选</p>


<!--more-->

文章概要:安装解压版的xampp后，apache显示正常启动了，但是localhost却无法访问。也排除了端口被占用的情况，那么要怎么样解决这个问题呢。

&nbsp;

安装xampp后apache显示正常启动，但是无法访问localhost。

<!--more-->

<span style="color: #ff0000;"><span style="font-size: x-large;">1.首先排除端口被占用的情况。</span></span>

使用netstat -ano命令查看80和443端口占用的进程ID，然后在任务管理器中查看该进程(菜单查看--显示列，选中PID)，如果是httpd，那么就是apache了，如果是其他程序，则先关掉这个程序。或者也可以修改apache的端口。

打开/apche/conf/httpd.conf

修改相应位置为

Listen 8090

ServerName localhost:8090

&nbsp;

打开 /apche/conf/extra/httpd-ssl.conf 修改为

&nbsp;

Listen:4433

ServerName localhost:4433

&nbsp;

<span style="color: #ff0000;"><span style="font-size: x-large;">2.如果已经排除端口占用情况，那么可能是winsock的问题了。</span></span>

使用360安全卫士可修复该问题。

打开360安全卫士-功能大全-网络修复（LSP），修复就可以了。

然后重新启动apache，于看看是不是可以访问localhost了？

&nbsp;