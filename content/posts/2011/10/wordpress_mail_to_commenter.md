```toml
title = "终于搞定了wordpress的评论回复邮件通知插件"
slug = "wordpress_mail_to_commenter"
desc = ""
date = "2011-10-29 15:23:57"
author = "admin"
tags = ["mail_to_commenter","wordpress","插件","解决办法","评论","通知","邮件"]
```

用过各种各样的邮件插件和评论回复邮件通知的插件，总是没有找到完美的，都会有这样或那样的问题。

这次下决心要把问题搞好，算起来总花了一天多时间。把经验分享一下，免得朋友们走弯路。

<!--more-->wordpress自带邮件功能，但是通过php的mail()函数的，而大多数主机都禁用了mail()函数。(其实我的主机是没有禁用这个函数的，但使用mail函数发的邮件都会被标记为来源不可信任，而且很容易被当成垃圾邮件直接删掉)。所以还是装个smtp的插件比较好。

关于smtp插件的问题，可以看<a title="wordpress发邮件出现Could not connect to SMTP host的解决办法(转载)" href="http://veikr.com/201110/wordpress_could_not_connect_to_smtp_host.html">这篇文章</a>  (可能很多朋友试过几乎所有的插件，试过网上几乎所有的方法都没解决问题，但也许这篇文章正是你想要的，因为smtp插件不生效的原因可能是个很冷门的原因)

&nbsp;

下面介绍评论邮件回复的插件。

我用的是mail to commenter。配置起来很简单，而且默认的邮件格式很简洁，支持嵌套，很不错。

但装上后也发现是不管用的，网上找了好久好久都没找到解决办法。后来自己无意中试了一下，居然找到问题了。

<span style="color: #ff0000;">是邮件头的问题</span>。

解决办法如下：

在插件编辑中找到mail to commenter插件的mailtocommenter_functions.php文件

往下拉，找到mailtocommenter_send_email方法。

方法的最后一句return @wp_mail(...)

<span style="color: #008000;">你只需要改成wp_mail($to,$subject,$message)就可以了，也就是把headers去掉</span>。

再试一次，邮件发送成功了。

但是你会发现邮件格式是乱的，链接全是乱的。因为邮件接收服务器把它当成了纯文本邮件，但是又自作主张的给网址加上了链接，所以就成了那个样子(我用的qq邮件收的邮件，不同的邮件可能会不一样)

那我们就再把header加上，

<span style="color: #008000;">直接把header改成 $headers = "Content-Type: text/html;charset=\"$charset\"\n"; </span>

return @wp_mail($to, $subject, $message,$headers);

也就是把from和mime去掉了，再测试，邮件发送成功，而且格式完好。看来真是header的问题。

不过这样做的话，发送人姓名就成了默认的wordpress。

所以我干脆去改了wp-mail-smtp插件，也就是把默认发送人姓名直接改成我博客的名字。

&nbsp;

找到wp-includes/pluggable.php文件，找到function wp_mail()函数

然后里面有一句
<pre><span style="color: #008000;">if ( !isset( $from_name ) )</span>
<span style="color: #008000;"> $from_name = 'veikr';</span></pre>
这里就是设置默认发送人姓名的。
改成你想要的就行了(中文会乱码)

好了，到此就全部改好了，再去试试吧。完全没问题了。