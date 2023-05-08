```toml
title = "android新浪微博客户端oauth认证中UC无法跳转的问题"
slug = "android_sina_oauth_uc_jump"
description = ""
date = "2011-06-14 13:00:05"
author = "admin"
tags = ["oauth","uc","新浪微博","浏览器"]
```

在开发新浪微博android客户端的时候需要oauth认证，也就是说要打开一个新浪的网页，用户在授权之后会再跳转回应用完完成授权。在请求用户授权的时候会提供一个callback地址，用户完成授权操作后会跳转回这个地方。但由于某些原因，UC并无法完成跳转，而系统自带浏览器却没有这个问题。本文就给出2个解决方案来解决这个问题。

<!--more-->

一、在应用中内嵌入一个webView完成授权。

方法很简单，使用webView的loadurl方法打开授权网址就可以了。但是授权完成后需要获取到网页中显示的pin，具体方法请参考昨天写的文章 <a title="android中如何获得webView中的内容" href="http://veikr.com/201106/android_webview_content-html.html" target="_blank">android中如何获得webView中的内容</a> 。在这里就不再赘述了。

但由于这种方法用户无法看到浏览器地址栏，而是在你的应用中输入了用户名和密码，所以用户会觉得不放心。那可以试试下面的方法。

二、直接打开系统自带浏览器完成授权。

我们一般使用

[java]

Intent i=new Intent();

i.setAction(Intent.ACTION_VIEW,Uri.parse(&quot;http://veikr.com&quot;));

startActivity(i);

[/java]

来打开某个网址，但用户有可能选择使用第三方浏览器(如UC)来打开，不过第三方浏览是无法支持自定义schema的(比如veikr://OauthActivity)。

只需要这样，就可以直接打开系统自带浏览器。

[java]

Intent intent = new Intent();

ComponentName name = new ComponentName(&quot;com.android.browser&quot;, &quot;com.android.browser.BrowserActivity&quot;);

intent.setComponent(name);

intent.setData(Uri.parse(&quot;http://veikr.com/wap/&quot;));

intent.setAction(Intent.ACTION_VIEW);
startActivity(intent);

[/java]

附：这里提一下怎么使浏览器打开类似veikr://OauthActivity这样的地址。

写一个activity，然后部署的时候

[xml]

&lt;activity android:name=&quot;WebViewActivity&quot;&gt;

     &lt;intent-filter&gt;
          &lt;category android:name=&quot;android.intent.category.BROWSABLE&quot;&gt;&lt;/category&gt;
          &lt;data android:scheme=&quot;veikr&quot; android:host=&quot;OauthActivity&quot;&gt;&lt;/data&gt;
     &lt;/intent-filter&gt;
&lt;/activity&gt;

[/xml]

你需要把"veikr://OauthActivity"作为callback传递给新浪的oauth认证地址，在完成认证后会返回这个地址，然后你的应用程序的这个activity就可以接管过来了。
在oncreate中使用getIntent().getData()就可以得到uri，pin就在uri中。