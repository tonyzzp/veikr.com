```toml
title = "tomcat6+mysql连接池的简单实现(亲自试验通过)"
slug = "tomcat6_mysql_connection_pool"
description = ""
date = "2010-04-23 15:03:07"
author = "admin"
tags = ["mysql","tomcat","连接池"]
```

<p>在网上找了很久，文章都是你抄、我抄你。看来看去都一样的，google往后翻N页&#160; 进去一看都是一样的。郁闷至极。</p>  <p>于上是CSDN论坛求助，还是java\web坛子里的朋友热情些，终于算是搞好了，自己再试了下，把心得发出来大家指点指点。</p>  <p><font color="#0080ff">1、mysql-connector-java-5.0.8-bin.jar文件，也就是mysql驱动包。<font color="#ff0000">注意：要放到tomcat6/lib目录下。放到web-inf/lib下不行</font>，不知道为什么，我会再试试。</font></p>  <p><font color="#0080ff">2、修改tomcat6/conf/context.xml文件，以&lt;context&gt;标签之间加上</font></p>  `````` 24: 	out.println(&quot;<span style="color:
#8b0000">测试成功！</span>&quot;);`````````


<!--more-->

<p>在网上找了很久，文章都是你抄、我抄你。看来看去都一样的，google往后翻N页&#160; 进去一看都是一样的。郁闷至极。</p>  <p>于上是CSDN论坛求助，还是java\web坛子里的朋友热情些，终于算是搞好了，自己再试了下，把心得发出来大家指点指点。</p>  <p><font color="#0080ff">1、mysql-connector-java-5.0.8-bin.jar文件，也就是mysql驱动包。<font color="#ff0000">注意：要放到tomcat6/lib目录下。放到web-inf/lib下不行</font>，不知道为什么，我会再试试。</font></p>  <p><font color="#0080ff">2、修改tomcat6/conf/context.xml文件，以&lt;context&gt;标签之间加上</font></p>  `````` 24: 	out.println(&quot;<span style="color:
#8b0000">测试成功！</span>&quot;);`````````
