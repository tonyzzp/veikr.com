```toml
title = "jquery如何选择不含某属性的元素"
slug = "java_select_none_attribute"
desc = ""
date = "2010-07-27 16:16:48"
author = "admin"
tags = ["javascript","jquery","元素","属性","选择器"]
```

jquery的选择器有很多种<br/>今天遇到一个问题<br/>怎么样选择不含某个属性的元素的呢.<br/>尝试过很多种写法<br/>比如:<br/>$("span[class=null]")<br/>$("span[class==ull]")<br/>$("span[!class]")<br/>$("span[^class]")<br/>....都没成功<br/>后来尝试了最傻的方法  居然成功了<br/>$("span[class='']")


<!--more-->

jquery的选择器有很多种<br/>今天遇到一个问题<br/>怎么样选择不含某个属性的元素的呢.<br/>尝试过很多种写法<br/>比如:<br/>$("span[class=null]")<br/>$("span[class==null]")<br/>$("span[!class]")<br/>$("span[^class]")<br/>....都没成功<br/>后来尝试了最傻的方法  居然成功了<br/>$("span[class='']")
