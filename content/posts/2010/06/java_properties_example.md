```toml
title = "java中操作properties属性文件的简单教程"
slug = "java_properties_example"
description = ""
date = "2010-06-09 16:11:20"
author = "admin"
tags = ["java","properties","属性","教程"]
```

<p>java中常会用到properties文件作为配置文件,可以很容易的读取和设置,来对工程进行一些配置.<br>今天去公司笔试,考了这题,一点儿不会.我完全是按最原始的方法去读文件,写的.回来后在网上搜了下,感觉还是比较简单的,在这儿献个丑.</p> <p><font color="#0080ff" size="4">prop.properties文件</font></p> <p>name=许嵩<br>age=21  <p><font color="#0080ff" size="4">TestProp.java文件</font></p>``````}`````````
程序中,读取prop.properties文件,打印中其中的所有属性.然后增加了一个属性.再把配置写入到另一个文件中.<br>如果要修改其中一个属性的话,也很简单.只用prop.setProperty(“key”,”value”);就可以了``````&nbsp;```


<!--more-->

<p>java中常会用到properties文件作为配置文件,可以很容易的读取和设置,来对工程进行一些配置.<br>今天去公司笔试,考了这题,一点儿不会.我完全是按最原始的方法去读文件,写的.回来后在网上搜了下,感觉还是比较简单的,在这儿献个丑.</p> <p><font color="#0080ff" size="4">prop.properties文件</font></p> <p>name=许嵩<br>age=21  <p><font color="#0080ff" size="4">TestProp.java文件</font></p>``````}`````````
程序中,读取prop.properties文件,打印中其中的所有属性.然后增加了一个属性.再把配置写入到另一个文件中.<br>如果要修改其中一个属性的话,也很简单.只用prop.setProperty(“key”,”value”);就可以了``````&nbsp;```
