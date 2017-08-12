```toml
title = "发现jquery的val()方法的一个bug（待验证）"
slug = "jquery_val_bug"
desc = ""
date = "2010-04-23 14:49:13"
author = "admin"
tags = ["bug","jquery"]
```

<p>jquery的val()方法：返回元素的值，也就是value属性</p>  <p>比如</p>  <p>&lt;input id=”acct” type=”text” value=”我是值” /&gt;</p>  <p>则$(“#id”).val() 得到的结果应该是&#160; ”我是值“</p>  <p>这也相当于.aatr(“value”)方法。。</p>  <p>&#160;</p>  <p>但是今天发现一个bug</p>  <p>&lt;li id=”idid’ value=”值”&gt;石沉溪的博客<a href="http://www.cnblogs.com/tonyzzp">http://www.cnblogs.com/tonyzzp</a> &lt;/li&gt;</p>  <p>通过$(“idid”).val()却得不到值。</p>  <p>但通过.attr(“value”)可以。</p>  <p>在ie8&#160;&#160; firefox3.5&#160;&#160; chrome5&#160; 中测试 都是这样。。</p>


<!--more-->

<p>jquery的val()方法：返回元素的值，也就是value属性</p>  <p>比如</p>  <p>&lt;input id=”acct” type=”text” value=”我是值” /&gt;</p>  <p>则$(“#id”).val() 得到的结果应该是&#160; ”我是值“</p>  <p>这也相当于.aatr(“value”)方法。。</p>  <p>&#160;</p>  <p>但是今天发现一个bug</p>  <p>&lt;li id=”idid’ value=”值”&gt;石沉溪的博客<a href="http://www.cnblogs.com/tonyzzp">http://www.cnblogs.com/tonyzzp</a> &lt;/li&gt;</p>  <p>通过$(“idid”).val()却得不到值。</p>  <p>但通过.attr(“value”)可以。</p>  <p>在ie8&#160;&#160; firefox3.5&#160;&#160; chrome5&#160; 中测试 都是这样。。</p>
