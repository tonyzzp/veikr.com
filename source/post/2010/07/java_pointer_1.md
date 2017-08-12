```toml
title = "Java中的指针(一)"
slug = "java_pointer_1"
desc = ""
date = "2010-07-27 15:07:49"
author = "admin"
tags = ["java","pointer","指针"]
```

本文概要:学过java的都知道,java的一些特性(或者说java所宣传的java的优势).其中有一条就是java没有指针.java去掉了c++中常见的指针,指针虽然很方便,但很多时候往往带带很多麻烦,使用的时候也是胆战心惊.但事实上java真的没有指针吗?<br/><br/>在有的时候,你可以会遇到一个问题,从某个地方取出的某个对象,你对它做了改变,你会发现原来的那个对象也被一起改变了.<br/>比如下面这个事例<br/>User.java<br/>[code=java]<br/>package test;<br/><br/>public class User implements Cloneable {<br/>...


<!--more-->

本文概要:学过java的都知道,java的一些特性(或者说java所宣传的java的优势).其中有一条就是java没有指针.java去掉了c++中常见的指针,指针虽然很方便,但很多时候往往带带很多麻烦,使用的时候也是胆战心惊.但事实上java真的没有指针吗?

在有的时候,你可以会遇到一个问题,从某个地方取出的某个对象,你对它做了改变,你会发现原来的那个对象也被一起改变了.
比如下面这个事例
<span style="color: #3366ff;">User.java</span>

package test;

public class User implements Cloneable {
private int id;
private String name;
private int age;

public User(){

}

public User(int id,String name,int age){
this.id=id;
this.name=name;
this.age=age;
}

public int getId() {
return id;
}
public void setId(int id) {
this.id = id;
}
public String getName() {
return name;
}
public void setName(String name) {
this.name = name;
}
public int getAge() {
return age;
}
public void setAge(int age) {
this.age = age;
}

public String toString(){
return "{id:"+id+",name:"+name+",age:"+age+"}";
}
}


<span style="color: #3366ff;">test.jsp</span>


&lt;%
User user=new User(1,"章治鹏",22);
session.setAttribute("user",user);
%&gt;

<hr />

${sessionScope.user}

<hr />

&lt;%
user=(User)session.getAttribute("user");
user.setName("zzp");
%&gt;
${sessionScope.user }



执行结果是什么呢?
{id:1,name:章治鹏,age:22}
{id:1,name:zzp,age:22}

很多人可能在想,一般时候我会这样做

User u=(User)session.getAttribute("user");
u.setName="zzp";
session.setAttribute("user",u);

但事实上你看到了,你不需要这样做.
因为你在session.setAttribute("user",user)
的时候,放入session的只不过是user的一个引用,也就是user这个对象的指针,并不是把整个user对象放入到了session中.
而你使用session.getAttribute("user");得到的也只是session中user这个属性的所对应的user对象的指针,也就是内存地址.
当你对它进行改变的时候,session中的user所指的也自然改变了(事实上他们是一个东西,内存值是一样的)

下节中将会继续对java中的指针进行讲解.
经验不足,欢迎大家拍砖.

&nbsp;