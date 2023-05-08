```toml
title = "诺基亚手机调制解调器驱动安装错误的解决办法"
slug = "nokia_moderm_driver_error"
description = ""
date = "2010-04-21 19:18:17"
author = "admin"
tags = ["driver","moderm","nokia"]
```

<p>在安诺基亚手机调制解调器的时候,发生错误.提交没有找到指定的系统文件..</p><p>解决办法</p>


<!--more-->

<p>在安诺基亚手机调制解调器的时候,发生错误.提交没有找到指定的系统文件..</p><p>解决办法</p><p>1.确实是丢失了系统文件 .在别人电脑上找到c:\windows\inf\mdmcpq.inf&nbsp;&nbsp;&nbsp;&nbsp; 和 c:\windows\system32\drivers\usbser.sys&nbsp;</p><p>2.mdmcpq.inf配置有问题</p><p>解决办法:</p><p>将</p><p>[FakeModemCopyFileSection]    <br />usbser.sys,,,0x20</p><p>&nbsp;</p><p>修改为</p><p>[FakeModemCopyFileSection]    <br />;usbser.sys,,,0x20</p><p>&nbsp;</p><p>也就是把这句配置注释掉.</p><p>&nbsp;</p><p>问题成功解决.</p>
