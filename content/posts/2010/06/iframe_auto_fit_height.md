```toml
title = "iframe自适应高度(适合IE firefox  opera)"
slug = "iframe_auto_fit_height"
description = ""
date = "2010-06-08 14:30:59"
author = "admin"
tags = ["html","iframe","浏览器","自适应","高度"]
```

<p>做有些网页的时候用frameset会很方便,但是frameset很影响速度,而且还很不美观,并且seo也不好.所以用iframe还是比较好的选择.   <br />后来看到QQ空间个人中心也用的iframe,很漂亮.很好用.于是也试着用iframe.但是自适应高度很是个问题.不同的游戏器都会不一样,说到这儿我要再深深的BS一下IE..    <br />做了很多尝试,在网上看了很久,做了下小小的总结.希望对大家有帮助</p><p><font color="#ff0000" size="5">怎么获取网页的高度</font></p><p><font color="#0080ff" size="4">对于IE(我用的IE8,IE6就不知道行不行了)</font></p><p><font color="#000000" size="4">document.getElementById(&ldquo;myframe&rdquo;).Document.body.scrollHeight;</font></p><p><font color="#0080ff" size="4">对于其他浏览器(firefox&nbsp; opera)</font></p><p><font color="#000000" size="4">document.getElementById(&ldquo;myframe&rdquo;).contentDocument.body.scrollHeight;</font></p><p><font color="#0080ff" size="4">共用方法(IE8&nbsp; firefox&nbsp; opera)</font></p><p><font color="#000000" size="4">document.getElementById(&ldquo;myframe&rdquo;).contentWindow.document.body.scrollHeight;</font></p><p>&nbsp;</p><p><font color="#0080ff" size="4">代码</font></p>``````<span style="co
lor: #0000ff">&gt;</span><span style="color: #0000ff">&lt;/</span><span style="color: #800000">iframe</span><span style="color: #0000ff">&gt;</span>``````


<!--more-->

做有些网页的时候用frameset会很方便,但是frameset很影响速度,而且还很不美观,并且seo也不好.所以用iframe还是比较好的选择.
后来看到QQ空间个人中心也用的iframe,很漂亮.很好用.于是也试着用iframe.但是自适应高度很是个问题.不同的游戏器都会不一样,说到这儿我要再深深的BS一下IE..
做了很多尝试,在网上看了很久,做了下小小的总结.希望对大家有帮助

<span style="color: #ff0000; font-size: large;">怎么获取网页的高度</span>

<span style="color: #0080ff; font-size: medium;">对于IE(我用的IE8,IE6就不知道行不行了)</span>

<span style="color: #000000; font-size: medium;">document.getElementById(“myframe”).Document.body.scrollHeight;</span>

<span style="color: #0080ff; font-size: medium;">对于其他浏览器(firefox  opera)</span>

<span style="color: #000000; font-size: medium;">document.getElementById(“myframe”).contentDocument.body.scrollHeight;</span>

<span style="color: #0080ff; font-size: medium;">共用方法(IE8  firefox  opera)</span>

<span style="color: #000000; font-size: medium;">document.getElementById(“myframe”).contentWindow.document.body.scrollHeight;</span>

<span style="color: #0080ff; font-size: medium;">代码</span>
```
``````
``````
``````
``````
```  5: function change(){```
```  6: var o=document.getElementById("myframe");```
```  7: var height= o.contentWindow.document.body.scrollHeight;```
```  8: o.height=height;```
```  9: }```
``` 10:```
``` 11: function show(){```
``` 12: var o=document.getElementById("myframe");```
``` 13: alert(o.contentWindow.document.body.scrollHeight);```
``` 14: }```
``````
``````
``````
``````
``````
``````
``````
``````
```<span style="co
lor: #0000ff;">&gt;</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">iframe</span><span style="color: #0000ff;">&gt;</span>```
``````
``````
```
<span style="color: #ff0000; font-size: medium;">注:</span>

<span style="color: #000000; font-size: medium;">我用的浏览器版本</span>

<span style="color: #000000; font-size: medium;">IE8   firefox3.5   opera10.05</span>

代码下载: <a href="/assets/UPLOAD_OLD/2010/6/iframe.zip" target="_blank">iframe.zip</a>