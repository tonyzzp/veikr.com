```toml
title = "jsp中的自定义标签的简单教程"
slug = "jsp_customer_tag"
desc = ""
date = "2010-06-04 18:14:53"
author = "admin"
tags = ["java","jsp","tag","教程","标签","自定义"]
```

<p>&nbsp;&nbsp;今天去找工作,我说我用过jstl标签.然后他问我 有没有试过自定义标签.我说没有.后来他说他们会五天内通知我,让我回去准备一下.</p><div style="background-color: rgb(255, 255, 255); padding-top: 5px; padding-right: 5px; padding-bottom: 5px; padding-left: 5px; margin-top: 0px; margin-right: 0px; margin-bottom: 0px; margin-left: 0px; font-family: Arial, Verdana, sans-serif; font-size: 12px; line-height: 160%; "><p>上次我们班有个同学找工作,别人问个问题,他不会.回来也不管,结果去笔试又考了这个题....悲剧了.</p><p>这次我一定要吸取教训,把问过的几个问题都搞懂了.</p><p>先来看看自定义标签.</p><p><span style="color: rgb(255, 0, 0); "><span style="font-size: larger; ">自定义标签使用方法</span></span></p><p>1、写一个类，继承TagSupport,这个类就是用来处理标签的.</p><p>类里主要有2个方法doStartTag()和doEndTag(),分别对开始闭合标签进行处理</p><p>2、写.tld标签文件</p><p>3、在web.xml中对tld文件进行配置</p><p>&nbsp;</p><p><span style="color: rgb(51, 102, 255); ">废话少说,直接看代码.下面写个显示当前时间的自定义标签</span></p><p>代码比较简单,大家一看就懂.</p><p>&nbsp;</p><p><span style="background-color: rgb(255, 255, 0); ">ShowTime.java</span></p><p>&nbsp;</p><p>package org.zzp.tag;</p><p>&nbsp;</p><p>import java.io.IOException;</p><p>import java.text.SimpleDateFormat;</p><p>import java.util.Date;</p><p>&nbsp;</p><p>import javax.servlet.jsp.JspException;</p><p>import javax.servlet.jsp.JspWriter;</p><p>import javax.servlet.jsp.tagext.TagSupport;</p><p>&nbsp;</p><p>public class ShowTime extends TagSupport {</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>private static final long serialVersionUID = 3593807751447286551L;</p><p>&nbsp;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>@Override</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>public int doEndTag() throws JspException {</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>JspWriter out=pageContext.getOut();</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>Date date=new Date();</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>SimpleDateFormat sdf=new SimpleDateFormat(&quot;yyyy-MM-dd HH:mm:ss&quot;);</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>try {</p><p><span class="Apple-tab-span" style="white-space: pre; ">			</span>out.println(sdf.format(date));</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>} catch (IOException e) {</p><p><span class="Apple-tab-span" style="white-space: pre; ">			</span>// TODO Auto-generated catch block</p><p><span class="Apple-tab-span" style="white-space: pre; ">			</span>e.printStackTrace();</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>}</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>return super.doEndTag();</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>}</p><p>&nbsp;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>@Override</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>public int doStartTag() throws JspException {</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span></p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>return super.doStartTag();</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>}</p><p>}</p><p>&nbsp;</p><p>&nbsp;</p><p><span style="background-color: rgb(255, 255, 0); ">MyTag.tld</span></p><p>&nbsp;</p><p>&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot; ?&gt;</p><p>&lt;!DOCTYPE taglib</p><p>PUBLIC &quot;-//Sun Microsystems, Inc.//DTD JSP Tag Library 1.2//EN&quot;</p><p>&quot;http://java.sun.com/dtd/web-jsptaglibrary_1_2.dtd&quot;&gt;</p><p>&lt;taglib&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>&lt;tlib-version&gt;1.0&lt;/tlib-version&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>&lt;jsp-version&gt;1.0&lt;/jsp-version&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>&lt;short-name&gt;mytags&lt;/short-name&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>&lt;tag&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>&lt;name&gt;time&lt;/name&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>&lt;tag-class&gt;org.zzp.tag.ShowTime&lt;/tag-class&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>&lt;/tag&gt;</p><p>&lt;/taglib&gt;</p><p>&nbsp;</p><p><span style="background-color: rgb(255, 255, 0); "><br type="_moz" /></span></p><p><span style="background-color: rgb(255, 255, 0); ">web.xml</span></p><p>&lt;web-app&gt;</p><p>&nbsp;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>&lt;jsp-config&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>&lt;taglib&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">			</span>&lt;taglib-uri&gt;/mytag&lt;/taglib-uri&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">			</span>&lt;taglib-location&gt;/WEB-INF/MyTag.tld&lt;/taglib-location&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">		</span>&lt;/taglib&gt;</p><p><span class="Apple-tab-span" style="white-space: pre; ">	</span>&lt;/jsp-config&gt;</p><p>&lt;/web-app&gt;</p><p>其中,taglib-location是tld文件的位置</p><p>&nbsp;</p><p><span style="background-color: rgb(255, 255, 0); ">tag.jsp</span></p><p>&nbsp;</p><p>&nbsp;</p><p>&lt;%@ page language=&quot;java&quot; contentType=&quot;text/html; charset=UTF-8&quot;</p><p>&nbsp;&nbsp; &nbsp;pageEncoding=&quot;UTF-8&quot;%&gt;</p><p>&lt;%@taglib prefix=&quot;mine&quot; uri=&quot;/mytag&quot; %&gt;</p><p>&lt;!DOCTYPE html PUBLIC &quot;-//W3C//DTD HTML 4.01 Transitional//EN&quot; &quot;http://www.w3.org/TR/html4/loose.dtd&quot;&gt;</p><p>&lt;html&gt;</p><p>&lt;head&gt;</p><p>&lt;meta http-equiv=&quot;Content-Type&quot; content=&quot;text/html; charset=UTF-8&quot;&gt;</p><p>&lt;title&gt;Insert title here&lt;/title&gt;</p><p>&lt;/head&gt;</p><p>&lt;body&gt;</p><p>&lt;mine:time&gt;&lt;/mine:time&gt;</p><p>&lt;/body&gt;</p><p>&lt;/html&gt;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p><p>&nbsp;</p></div>...


<!--more-->

今天去找工作,我说我用过jstl标签.然后他问我 有没有试过自定义标签.我说没有.后来他说他们会五天内通知我,让我回去准备一下.
<div style="background-color: #ffffff; font-family: Arial, Verdana, sans-serif; font-size: 12px; line-height: 160%; padding: 5px; margin: 0px;">

上次我们班有个同学找工作,别人问个问题,他不会.回来也不管,结果去笔试又考了这个题....悲剧了.

这次我一定要吸取教训,把问过的几个问题都搞懂了.

先来看看自定义标签.

<!--more-->

<span style="color: #ff0000;"><span style="font-size: larger;">自定义标签使用方法</span></span>

1、写一个类，继承TagSupport,这个类就是用来处理标签的.

类里主要有2个方法doStartTag()和doEndTag(),分别对开始闭合标签进行处理

2、写.tld标签文件

3、在web.xml中对tld文件进行配置

<span style="color: #3366ff;">废话少说,直接看代码.下面写个显示当前时间的自定义标签</span>

代码比较简单,大家一看就懂.

<span style="background-color: #ffff00;">ShowTime.java</span>

package org.zzp.tag;

import java.io.IOException;

import java.text.SimpleDateFormat;

import java.util.Date;

import javax.servlet.jsp.JspException;

import javax.servlet.jsp.JspWriter;

import javax.servlet.jsp.tagext.TagSupport;

public class ShowTime extends TagSupport {

<span style="white-space: pre;"> </span>private static final long serialVersionUID = 3593807751447286551L;

<span style="white-space: pre;"> </span>@Override

<span style="white-space: pre;"> </span>public int doEndTag() throws JspException {

<span style="white-space: pre;"> </span>JspWriter out=pageContext.getOut();

<span style="white-space: pre;"> </span>Date date=new Date();

<span style="white-space: pre;"> </span>SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

<span style="white-space: pre;"> </span>try {

<span style="white-space: pre;"> </span>out.println(sdf.format(date));

<span style="white-space: pre;"> </span>} catch (IOException e) {

<span style="white-space: pre;"> </span>// TODO Auto-generated catch block

<span style="white-space: pre;"> </span>e.printStackTrace();

<span style="white-space: pre;"> </span>}

<span style="white-space: pre;"> </span>return super.doEndTag();

<span style="white-space: pre;"> </span>}

<span style="white-space: pre;"> </span>@Override

<span style="white-space: pre;"> </span>public int doStartTag() throws JspException {

<span style="white-space: pre;"> </span>

<span style="white-space: pre;"> </span>return super.doStartTag();

<span style="white-space: pre;"> </span>}

}

<span style="background-color: #ffff00;">MyTag.tld</span>

&lt;?xml version="1.0" encoding="UTF-8" ?&gt;

&lt;!DOCTYPE taglib

PUBLIC "-//Sun Microsystems, Inc.//DTD JSP Tag Library 1.2//EN"

"http://java.sun.com/dtd/web-jsptaglibrary_1_2.dtd"&gt;

&lt;taglib&gt;

<span style="white-space: pre;"> </span>&lt;tlib-version&gt;1.0&lt;/tlib-version&gt;

<span style="white-space: pre;"> </span>&lt;jsp-version&gt;1.0&lt;/jsp-version&gt;

<span style="white-space: pre;"> </span>&lt;short-name&gt;mytags&lt;/short-name&gt;

<span style="white-space: pre;"> </span>&lt;tag&gt;

<span style="white-space: pre;"> </span>&lt;name&gt;time&lt;/name&gt;

<span style="white-space: pre;"> </span>&lt;tag-class&gt;org.zzp.tag.ShowTime&lt;/tag-class&gt;

<span style="white-space: pre;"> </span>&lt;/tag&gt;

&lt;/taglib&gt;

<span style="background-color: #ffff00;">
</span>

<span style="background-color: #ffff00;">web.xml</span>

&lt;web-app&gt;

<span style="white-space: pre;"> </span>&lt;jsp-config&gt;

<span style="white-space: pre;"> </span>&lt;taglib&gt;

<span style="white-space: pre;"> </span>&lt;taglib-uri&gt;/mytag&lt;/taglib-uri&gt;

<span style="white-space: pre;"> </span>&lt;taglib-location&gt;/WEB-INF/MyTag.tld&lt;/taglib-location&gt;

<span style="white-space: pre;"> </span>&lt;/taglib&gt;

<span style="white-space: pre;"> </span>&lt;/jsp-config&gt;

&lt;/web-app&gt;

其中,taglib-location是tld文件的位置

<span style="background-color: #ffff00;">tag.jsp</span>

&lt;%@ page language="java" contentType="text/html; charset=UTF-8"

pageEncoding="UTF-8"%&gt;

&lt;%@taglib prefix="mine" uri="/mytag" %&gt;

&lt;!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"&gt;

&lt;html&gt;

&lt;head&gt;

&lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8"&gt;

&lt;title&gt;Insert title here&lt;/title&gt;

&lt;/head&gt;

&lt;body&gt;

&lt;mine:time&gt;&lt;/mine:time&gt;

&lt;/body&gt;

&lt;/html&gt;

</div>