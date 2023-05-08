```toml
title = "以最简单的方式实现jsp+mysql分页"
slug = "simple_jsp_mysql_paging"
description = ""
date = "2010-04-23 15:01:28"
author = "admin"
tags = ["jsp","mysql","分页"]
```

刚开始弄 ,目前分页是在前台jsp中实现的   与bean相比 这样比较容易一些先把代码贴出来   正在研究怎么样用bean实现分页  等弄好了 再贴代码下面说下分页理论 select * from message order by time desc limit begin,sizebegin 数据记录从第几条开始    begin=(当前页数-1)*sizesize 每页的记录数下面是连接数据库的javabean;刚开始弄 ,目前分页是在前台jsp中实现的   与bean相比 这样比较容易一些先把代码贴出来   正在研究怎么样用bean实现分页  等弄好了 再贴代码下面说下分页理论 select * from message order by time desc limit begin,sizebegin 数据记录从第几条开始    begin=(当前页数-1)*sizesize 每页的记录数下面是连接数据库的javabean;


<!--more-->

<p>刚开始弄 ,目前分页是在前台jsp中实现的&#160;&#160; 与bean相比 这样比较容易一些</p>  <p>先把代码贴出来&#160;&#160; 正在研究怎么样用bean实现分页&#160; 等弄好了 再贴代码</p>  <p><font color="#ff0000">下面说下分页理论 select * from message order by time desc limit begin,size</font></p>  <p><font color="#ff0000">begin 数据记录从第几条开始&#160;&#160;&#160; </font><font color="#ff0000">begin=(当前页数-1)*size</font></p>  <p><font color="#ff0000">size 每页的记录数</font></p>  <p><font color="#0000ff">下面是连接数据库的javabean;</font></p>  <p><font color="#0000ff"></font></p>  <div id="codeSnippetWrapper">   <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">     ```    <pr
e style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum14">  14:</span>     }```<!--CRLF-->    ```    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: white; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black;
font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum29">  29:</span>     <span style="color: #0000ff">public</span> <span style="color: #0000ff">int</span> update(String sql) <span style="color: #0000ff">throws</span>  Exception{```<!--CRLF-->    ```
3:</span> <span style="color: #0000ff">int</span> page_count;    <span style="color: #008000">//总页数</span>```<!--CRLF-->    ```    <pre style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; margin: 0em; padding-left: 0px; width: 100%; padding-right: 0px; font-family: &#39;Courier New&#39;, courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-
style: none; overflow: visible; padding-top: 0px"><span style="color: #606060" id="lnum18">  18:</span> out.println(<span style="color: #006080">&quot;总记录数为:&quot;</span> + result_count + <span style="color: #006080">&quot;     每页记录数为:&quot;</span> + size + <span style="color: #006080">&quot;     总页数为:&quot;</span> + page_count + <span style="color: #006080">&quot;     当前是第&quot;</span> + p + <span style="color: #006080">&quot;页&quot;</span>);```<!--CRLF-->    ```  33:</
span> &lt;tr&gt;&lt;td colspan=<span style="color: #006080">&quot;2&quot;</span>&gt;&lt;%=rs.getString(5)%&gt;&lt;/td&gt;&lt;/tr&gt;```<!--CRLF-->    ```
