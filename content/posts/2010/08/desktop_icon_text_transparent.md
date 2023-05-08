```toml
title = "让桌面图标文字背景透明的解决办法"
slug = "desktop_icon_text_transparent"
desc = ""
date = "2010-08-18 16:23:24"
author = "admin"
tags = ["windows","xp","图标","桌面","背景","透明"]
```

本文概要：xp环境下，让桌面图标下面的文字背景变透明的办法<br/><br/>可能这里面的一些办法你看过，但还是希望你把每一个都看完，都试一遍，肯定会好的。<br/><br/>1、桌面右键--排列图标--锁定WEB项目   去掉这选项<br/>2、控制面板--辅助选项--显示   去掉高对比度<br/>3、我的电脑右键--属性--高级--性能（设置）--为图标设置阴影   选中<br/>4、注册表(运行regedit) --HKEY_CURRENT_U


<!--more-->

本文概要：xp环境下，让桌面图标下面的文字背景变透明的办法<br/><br/>可能这里面的一些办法你看过，但还是希望你把每一个都看完，都试一遍，肯定会好的。<br/><br/>1、桌面右键--排列图标--锁定WEB项目   去掉这选项<br/>2、控制面板--辅助选项--显示   去掉高对比度<br/>3、我的电脑右键--属性--高级--性能（设置）--为图标设置阴影   选中<br/>4、注册表(运行regedit) --HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced 中的ListviewShadow键值数据为1<br/><br/>最后，重启explorer   任务管理器--进程--explorer 结束进程<br/>文件--新建--  explorer<br/><br/>任务完成 。
