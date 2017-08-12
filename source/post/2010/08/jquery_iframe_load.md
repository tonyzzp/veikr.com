```toml
title = "使用jquery获取iframe加载完成事件"
slug = "jquery_iframe_load"
desc = ""
date = "2010-08-25 11:50:24"
author = "admin"
tags = ["iframe","javascript","jquery","js","事件","加载"]
```

本文概要：网页中的iframe加载完成后，希望做一些工作。比如在iframe内容改变前在某处显示"正在加载"，在加载完成后，显示内容改为"加载完成"。那么该怎么处理呢？<br/><br/>在jquery中iframe加载完成事件为load，而不是ready<br/><br/>[code=html]<br/><br/><br/><br/><br/><br/>$(function(){<br/>	$("#phone").change(function(){<br/>		$("#message")


<!--more-->

本文概要：网页中的iframe加载完成后，希望做一些工作。比如在iframe内容改变前在某处显示"正在加载"，在加载完成后，显示内容改为"加载完成"。那么该怎么处理呢？

在jquery中iframe加载完成事件为load，而不是ready
<span style="color: red;">访问<a href="/TestRun/jquery_iframe_load.html" target="_blank">运行查看效果</a></span>