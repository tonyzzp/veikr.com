```toml
title = "eclipse下启动tomcat出现Setting property 'source' to 'org.eclipse.jst.jee.server: '错误的解决办法"
slug = "eclipse_tomcat_setting_property_source_org_eclipse_jst_jee_server"
date = "2010-04-23 14:54:43"
author = "admin"
tags = ["eclipse","tomcat","错误"]
```

在eclipse中启动tomcat时出现Setting property 'source' to 'org.eclipse.jst.jee.server:你的站点名'   did not find a matching property警告


<!--more-->

<p>在eclipse中启动tomcat时出现Setting property 'source' to 'org.eclipse.jst.jee.server:你的站点名'&#160;&#160; did not find a matching property错误</p>  <p>&#160;</p>  <p>解决办法：</p>  <p>1、在server控制台内，在服务器上点右键--属性</p>  <p>2、general选项卡中点switch location</p>  <p>这时，location变为:/servers/tomcat6.0 server at localhost.server</p>  <p>3、在project explore中找到tomcat项目--Tomcat v6.0 Server at localhost.server&#160; 这个文件 ，双击打开 </p>  <p>4、在最下面的server option里选中publis module context to separate xml file.保存。（保存时要先停止服务器）</p>  <p>&#160;</p>  <p>问题完美解决。</p>
