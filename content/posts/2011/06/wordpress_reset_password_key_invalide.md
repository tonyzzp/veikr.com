```toml
title = "wordpress重置密码的时候'key似乎无效'的解决办法"
slug = "wordpress_reset_password_key_invalide"
desc = ""
date = "2011-06-14 11:09:19"
author = "admin"
tags = ["key似乎无效","php","wordpress","取回","密码"]
```

wordpress有用户注册功能，如果用户忘记了密码，可以通过邮箱找回。但你肯定遇到过点击链接后提示“抱歉，key似乎无效”的情况。可能wordpress的小BUG，或者说是收件人邮箱系统的BUG。收到的密码重置链接会类似这样<a href="http://veikr.com/wp-login.php?action=rp&amp;key=QKO8DDJ3WbIcb506Teiz&amp;login=aaaaa" target="_blank">http://veikr.com/wp-login.php?action=rp&amp;key=QKO8DDJ3WbIcb506Teiz&amp;login=aaaaa</a> 。可能是为了美观，在链接前后增加了&lt;&gt;，但邮件又是纯文本格式的，邮箱收到后会自动添加超链接，好心办了坏事儿。结果链接就变成了<a href="http://veikr.com/wp-login.php?action=rp&amp;key=QKO8DDJ3WbIcb506Teiz&amp;login=aaaaa&gt;" target="_blank">http://veikr.com/wp-login.php?action=rp&amp;key=QKO8DDJ3WbIcb506Teiz&amp;login=aaaaa&gt;</a> 这样。后面多了个&gt;，这一点进去能不key无效吗？

<!--more-->

网上很多文章提到了这个问题，但解决办法都是说直接去修改数据库把管理员密码改回来。可这并不能彻底解决问题，因为这个功能并不仅仅是面向管理员的，也是面向普通用户的。我从来没学过ＰＨＰ，经过长时间折腾，总算是找到解决办法了。

<span style="color: #3366ff;">方法很简单，如下：</span>

找到wp-login.php文件，只需要修改一个小地方就可以了。

大概在１８０行，找到retrieve_password()方法，往下拉，有很多$message.=这样的语句，这个参数就是邮件主体内容。最后一行内容是$message .= '&lt;' . network_site_url("wp-login.php?action=rp&amp;key=$key&amp;login=" . rawurlencode($user_login), 'login') . "&gt;\r\n";  这个就是找回密码的链接，前后有&lt;&gt;，去掉就可以了。<span style="color: #ff0000;">注意需要改成这样：$message .=network_site_url("wp-login.php?action=rp&amp;key=$key&amp;login=" . rawurlencode($user_login), 'login') ;</span>

ＯＫ！万事大吉！