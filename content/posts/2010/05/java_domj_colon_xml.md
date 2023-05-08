```toml
title = "在java中使用dom4j解析带冒号节点的xml文件"
slug = "java_domj_colon_xml"
description = ""
date = "2010-05-11 11:15:39"
author = "admin"
tags = ["dom4j","java","xml"]
```

闲了无聊试试用java搞一个豆瓣的api，一直以为我对dom4j还算有些了解，一般的xml解析应用都还成的。结果，才发现连解析都还没学好。遇到个带冒号的节点，不会搞了。<br/><br/>类似这样<br/><br/><textarea class="code" rows="10" cols="50">
&lt;entry&gt;
&lt;db:uid&gt;streamcavee&lt;/db:uid&gt;
&lt;db:homepage&gt;www.streamcave.com&lt;/db:homepage&gt;
&lt;entry&gt;
</textarea><br/><br/>居然不会弄了。<br/>用root.element("db:uid")取出来的总是null<br/><br/>在网上搜出来的文章都是你抄我，我抄你。都郁闷死了。<br/>...


<!--more-->

闲了无聊试试用java搞一个豆瓣的api，一直以为我对dom4j还算有些了解，一般的xml解析应用都还成的。结果，才发现连解析都还没学好。遇到个带冒号的节点，不会搞了。<br/><br/>类似这样<br/><br/><textarea class="code" rows="10" cols="50">
&lt;entry&gt;
&lt;db:uid&gt;streamcavee&lt;/db:uid&gt;
&lt;db:homepage&gt;www.streamcave.com&lt;/db:homepage&gt;
&lt;entry&gt;
</textarea><br/><br/>居然不会弄了。<br/>用root.element("db:uid")取出来的总是null<br/><br/>在网上搜出来的文章都是你抄我，我抄你。都郁闷死了。<br/>为这还忍不住在围脖上暴了粗口。 罪过啊。<br/><br/>其实正确的解析应该是<br/>root.element("uid")这样就行了。<br/>不用管冒号前面的东西。。很简单吧。<br/>但我就纳闷儿了。我不可能没有这样试过啊。  。。见鬼了吧。。
