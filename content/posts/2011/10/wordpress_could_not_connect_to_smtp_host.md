```toml
title = "wordpress发邮件出现Could not connect to SMTP host的解决办法(转载)"
slug = "wordpress_could_not_connect_to_smtp_host"
description = ""
date = "2011-10-26 22:54:39"
author = "admin"
tags = ["fsockopen","mail","pfsockopen","smtp","wordpress","wp-mail-smtp","邮件"]
```

很多php主机都禁用了mail()函数，所以一般找一个smtp的插件来完成发送邮件的工作。

wp-mail-smtp这个插件不错，但可能很多人都遇到过 could not connect to SMTP host的错误。

这个问题纠结很久，网上到处找，遇到这个问题的人也很多，后来终于找到了一篇文章介绍的解决办法。

<!--more-->
其实是主机禁用了fsockopen()函数，你可以写一个phpinfo看一下是否禁用了这个函数。
```&lt;?php
phpinfo();
?&gt;```
然后你可以在disable_functions一栏看到fsockopen，果然被禁用。
解决办法：
<span style="color: #ff0000;">用pfsockopen()函数直接替换掉 fsockopen()</span>
如果pfsockopen函数被禁用的话，换其他可以操作Socket函数来代替, 如stream_socket_client()
找到wp-includes/class.smtp.php 文件
把
@fsockopen 改成 @pfsockopen

方法转自<a href="http://www.hujuntao.com/archives/could-not-connect-to-smtp-host.html">http://www.hujuntao.com/archives/could-not-connect-to-smtp-host.html</a>
已不知道原出处。