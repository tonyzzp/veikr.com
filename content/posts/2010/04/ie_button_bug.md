```toml
title = "ie里的button标签的一个bug"
slug = "ie_button_bug"
description = ""
date = "2010-04-23 14:56:45"
author = "admin"
tags = ["bug","ie","javascript"]
```

<p>做毕业设计的时候，偶像间发现了ie的button标签的一个bug </p>  <p>原始的按钮我们这样写</p>  <p>&lt;input type=”button” id=”button_id” value=”值” /&gt;&#160;&#160;&#160; </p>  <p>这个按钮是value也是按钮上显示的文字 </p>  <p>而新的button标签是这样定义按钮的</p>  <p>&lt;button id=”button_id” value=”值”&gt;这是按钮&lt;/button&gt;</p>  <p>这个按钮的值和按钮上显示的文字是独立的 </p>  <p>但是ie却有个bug</p>  <p>在用button定义一个按钮的时候，取这个元素的值，取到的却是按钮上显示的文字，也就是“这是按钮”，而正确的值应该是“值”</p>  <p>firefox、chrome都没有这个问题。 </p>  <p>另外，我用的是jquery的$(“#button_id”).val()取的值，没有用原始的js取。不知道会不会不一样呢.. </p>  <p>希望ie再能对标准支持的好一点。这样能为网页开发人员省正好多事啊，也不用每做个东西，就要开几个浏览器去测试了。。悲哀。。</p>


<!--more-->

<p>做毕业设计的时候，偶像间发现了ie的button标签的一个bug </p>  <p>原始的按钮我们这样写</p>  <p>&lt;input type=”button” id=”button_id” value=”值” /&gt;&#160;&#160;&#160; </p>  <p>这个按钮是value也是按钮上显示的文字 </p>  <p>而新的button标签是这样定义按钮的</p>  <p>&lt;button id=”button_id” value=”值”&gt;这是按钮&lt;/button&gt;</p>  <p>这个按钮的值和按钮上显示的文字是独立的 </p>  <p>但是ie却有个bug</p>  <p>在用button定义一个按钮的时候，取这个元素的值，取到的却是按钮上显示的文字，也就是“这是按钮”，而正确的值应该是“值”</p>  <p>firefox、chrome都没有这个问题。 </p>  <p>另外，我用的是jquery的$(“#button_id”).val()取的值，没有用原始的js取。不知道会不会不一样呢.. </p>  <p>希望ie再能对标准支持的好一点。这样能为网页开发人员省正好多事啊，也不用每做个东西，就要开几个浏览器去测试了。。悲哀。。</p>
