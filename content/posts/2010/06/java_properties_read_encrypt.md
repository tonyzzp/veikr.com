```toml
title = "java中读取properties配置文件,并完成简单的加密解密"
slug = "java_properties_read_encrypt"
description = ""
date = "2010-06-09 17:53:11"
author = "admin"
tags = ["java","properties","加密","文件","解密"]
```

<p>本文概要:读取properties文件,并对其中是值进行简单的加密,写入另一个文件.然后读取加密后的文件,进行解密操作.</p><p>这是今天去公司笔试的题目.</p><p><font color="#0080ff" size="4">原题大概如下:</font></p><p>有一个properties文件,里面有若干个配置属性,现有一个接口,&nbsp;</p><p>public interface Encode {&nbsp;<br />&nbsp;&nbsp;&nbsp; public void encode(String fileInputName,String fileOutputName) throws Exception;&nbsp;<br />&nbsp;&nbsp;&nbsp; public void decode(String fileInputName,String fileOutputName) throws Exception;&nbsp;<br />}</p><p>encode方法功能:读取配置文件,把其中每项的值的每个字母ASCII码值+10,然后把密码后的配置文件写入fileOutputName文件中.&nbsp;<br />decode方法功能与encode相反.&nbsp;<br />写一个类实现这个接口,并写出main方法进行测试.</p><p>哎...悲剧的我压根儿就没用过properties文件,自然是不做啊,我直接用最原始的方法去读熟稔串进行解析的,感觉应该也没有错的.回来后在网上查了下.&nbsp;<br />其实很简单.</p>


<!--more-->

<p>本文概要:读取properties文件,并对其中是值进行简单的加密,写入另一个文件.然后读取加密后的文件,进行解密操作.</p><p>这是今天去公司笔试的题目.</p><p><font color="#0080ff" size="4">原题大概如下:</font></p><p>有一个properties文件,里面有若干个配置属性,现有一个接口,</p><p>public interface Encode {   <br />&nbsp;&nbsp;&nbsp; public void encode(String fileInputName,String fileOutputName) throws Exception;    <br />&nbsp;&nbsp;&nbsp; public void decode(String fileInputName,String fileOutputName) throws Exception;    <br />}</p><p>encode方法功能:读取配置文件,把其中每项的值的每个字母ASCII码值+10,然后把密码后的配置文件写入fileOutputName文件中.   <br />decode方法功能与encode相反.    <br />写一个类实现这个接口,并写出main方法进行测试.</p><p>哎...悲剧的我压根儿就没用过properties文件,自然是不做啊,我直接用最原始的方法去读熟稔串进行解析的,感觉应该也没有错的.回来后在网上查了下.   <br />其实很简单.</p><p><font color="#0080ff" size="4">代码如下:</font></p><p><font color="#0080ff" size="4">prop.properties文件</font></p><p>name=tonyzzp   <br />age=21    <br />sex=male    <br />homepage=www.streamcave.com/</p><p>&nbsp;</p><p><font color="#0080ff" size="4">Encode.java文件</font></p>``````         prop.setProperty(name, result);```<pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,'Courier New',courier,monospace; font-size: 12px
">      }``````}``````
