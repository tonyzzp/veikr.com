```toml
title = "不使用struts标签显示表单验证的错误信息"
slug = "none_struts_validate_error_message"
desc = ""
date = "2010-06-28 19:08:10"
author = "admin"
tags = ["actionerror","actionmessage","fielderror","java","struts2","标签","验证"]
```

本文概要:在使用struts2的表单验证的时候,会有一些信息(比如字段错误信息)返回到jsp页面中,显示给用户.<br/>使用struts标签可以很简单的达到目的.但是struts标签却自带样式,排版起来非常不方便.这里就介绍怎么样不使用struts标签,来显示出这些信息<br/><br/>比如有如下网页:<br/>[code=java]<br/>actionerror:<br/>actionmessage:<br/><br/><br/>	<br/>	提交<br/><br/>[/java]<br/>


<!--more-->

本文概要:在使用struts2的表单验证的时候,会有一些信息(比如字段错误信息)返回到jsp页面中,显示给用户.
使用struts标签可以很简单的达到目的.但是struts标签却自带样式,排版起来非常不方便.这里就介绍怎么样不使用struts标签,来显示出这些信息

比如有如下网页:

[java]
actionerror:&lt;s:actionerror /&gt;
actionmessage:&lt;s:actionmessage/&gt;
&lt;hr/&gt;&lt;form action=&quot;validation.action&quot; method=&quot;post&quot;&gt;	
&lt;input type=&quot;text&quot; name=&quot;username&quot; /&gt;&lt;s:fielderror key=&quot;username&quot;/&gt;
	&lt;button type=&quot;submit&quot;&gt;提交&lt;/button&gt;
&lt;/form&gt;
[/java]



在这段代码中,actioinerror标签用来显示错误信息:比如 注册失败
actionmessage用来显示提示信息,比如  注册成功.   (一般来说,这两个字段只会有一个里面有值.)
fielderror用来显示具体某个字段的错误.  比如:用户名长度太小.

而.使用struts标签会带有默认的排版,非常不方便.
所以我一直在找不使用struts标签来显示这些信息

方法很简单.使用EL表达式

actionmessage         ${actionMessages[0]}
actionerror           ${actionErrors[0]}
fielderror            ${fieldErrors.username[0]}


注意:每个字段都是一个list,所以需要使用下标.