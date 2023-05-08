```toml
title = "android中如何获得webView中的内容"
slug = "android_webview_content-html"
description = ""
date = "2011-06-13 18:08:01"
author = "admin"
tags = ["android","webview","例子","教程"]
```

本文概要：在程序中经常会用到webView来显示网页，但如果能够得到网页中的内容呢，本文将给你一个最简单的事例。文章最后附代码下载。

在做新浪微博客户端的时候需要用到oauth认证，会弹出新浪的认证网页，用户在新浪的网页中授权后返回到程序中完成认证。使用的是类似weibo://OauthActivity这样的URI返回的，也就类似于<a href="http://weibo.com">http://weibo.com</a>这样。但是UC浏览器却无法完成这个地址的跳转，android自带浏览器是没有问题的，所以就想到在程序中内嵌一个webView去显示新浪的网页进行授权。

<!--more-->

方法很简单，还是直接上代码清楚一些。第一段代码很少，过一下就行了，看到后面你就明白了。
<blockquote>class Handler {
public void show(String data) {
Toast.makeText(WebViewActivity.this, "执行了handler.show方法", 0).show();
new AlertDialog.Builder(WebViewActivity.this).setMessage(data).create().show();
}
}</blockquote>
这是一个内部内，定义了一个方法，对话框弹出传过来的内容，这个就是用来显示webView中的内容的。

下面是关键代码，大家先看，后面会有解释。
<blockquote>webView = new WebView(this);
setContentView(webView);
webView.loadUrl(" http://veikr.com/wap/ ");
webView.getSettings().setJavaScriptEnabled(true);
webView.addJavascriptInterface(new Handler(), "handler");
webView.setWebViewClient(new WebViewClient() {
@Override
public void onPageFinished(WebView view, String url) {
Toast.makeText(WebViewActivity.this, "网页加载完成", 0).show();
view.loadUrl("javascript:window.handler.show(document.body.innerHTML);");
super.onPageFinished(view, url);
}
});</blockquote>
1. webView.getSettings().setJavaScriptEnabled(true);

设置webView支持js.

2.webView.addJavascriptInterface(new Handler(), "handler");

使用了这段代码后就相当于在网页的js中增加了一个叫handler的类，而这个handler就是前面写的内部类。可以直接在网页中这样使用：onClick=”javascript:handler.show(‘hello’)”

也就是说直接通过网页中的js来执行java代码。

3.webView.setWebViewClient(new WebViewClient()

为webView设置一个处理器(暂且这样叫吧)，在webView加载完成后执行下面的方法

view.loadUrl("javascript:window.handler.show(document.body.innerHTML);");

document.body.innerHTML是一段js，会获取到网页中body标签里的内容，然后把这个值传递给Handler类的show方法。完成。

大家可以用浏览器打开一个网页，加载完成后，在浏览器地址栏输入

javascript:alert(document.body.innerHTML);

看看有什么效果？是不是弹出对话框显示了网页的body内容？

这个也是用到了这个道理。

下载代码 <a href="http://veikr.com/wp-content/uploads/2011/06/WebViewDemo.zip">WebViewDemo</a>