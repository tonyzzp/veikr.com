```toml
title = "java中怎么样对list进行排序"
slug = "java_list_sort"
desc = ""
date = "2010-09-17 15:48:41"
author = "admin"
tags = ["java","list","排序","教程"]
```

本文概要:在java中怎么样对一个list按自己的想法进行任意排序.比如按list中元素的name属性或按time属性.<br/><br/><font color="Green">主要用到了Collections.sort()方法,<br/>该方法有2个重载.其中一个方法只有一个参数,即排序对象,排序方法默认(这个我没试过,你可以自己试试)</font><br/>[FONT-COLOR=Red](纠错:此方法并不是默认排


<!--more-->

<h2>本文概要:在java中怎么样对一个list按自己的想法进行任意排序.比如按list中元素的name属性或按time属性.</h2>
<span style="color: green;">
</span>
<h3><span style="color: green;">主要用到了Collections.sort()方法,
该方法有2个重载.其中一个方法只有一个参数,即排序对象,排序方法默认(这个我没试过,你可以自己试试)</span>
<span style="color: red;">(纠错:此方法并不是默认排序)</span>
第二个方法有2个参数,第一个参数即为排序对象,第二个参数是个Comparetor,这就是今天要讲的.
直接看代码吧,3个java类,很简单,一看就懂.</h3>
<!--more-->

<span style="color: #3366ff;">User.java</span>

<span style="color: #3366ff;"> </span>

[code lang="java"]&lt;/span&gt;

import java.util.Date;

public class User {
private Date time;
private String name;

public User(Date time, String name) {
this.time = time;
this.name = name;
}

public String toString() {
return &quot;[name:&quot; + name + &quot;,time:&quot; + time.toLocaleString() + &quot;]&quot;;
}

public Date getTime() {
return time;
}

public void setTime(Date time) {
this.time = time;
}

public String getName() {
return name;
}

public void setName(String name) {
this.name = name;
}
}

[/code]

<span style="color: #3366ff;">UserComparetor.java</span>

<span style="color: #3366ff;"> </span>

[java]

import java.util.Comparator;

public class UserComparetor implements Comparator {

@Override
 public int compare(User o1, User o2) {
 long l1 = o1.getTime().getTime();
 long l2 = o2.getTime().getTime();
 if (l1 &gt; l2)
 return 1;
 else if (l1 &lt; l2)
 return -1;
 else
 return 0;
 }
 }

[/java]

<span style="color: yellow;"><span style="color: #3366ff;">Test.java</span></span>

<span style="color: yellow;"><span style="color: #3366ff;"> </span></span>

[java]

import java.util.ArrayList;
 import java.util.Calendar;
 import java.util.Collections;
 import java.util.List;

public class Test {
 public static void main(String[] args) {
 List us=new ArrayList();
 Calendar cal=Calendar.getInstance();
 cal.set(2010, 5, 6);
 User u=new User(cal.getTime(),&quot;许嵩&quot;);
 us.add(u);

cal.set(2009, 5, 30);
 u=new User(cal.getTime(),&quot;张杰&quot;);
 us.add(u);

cal.set(2010, 3, 1);
 u=new User(cal.getTime(),&quot;张靓颖&quot;);
 us.add(u);

for(User user:us){
 System.out.println(user);
 }
 System.out.println(&quot;排序后&quot;);
 Collections.sort(us, new UserComparetor());
 for(User user:us){
 System.out.println(user);
 }
 }
 }

[/java]