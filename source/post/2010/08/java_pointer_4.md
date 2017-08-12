```toml
title = "java中的指针(四)"
slug = "java_pointer_4"
desc = ""
date = "2010-08-12 16:15:24"
author = "admin"
tags = ["java","pointer"]
```

本文概要:java中的深拷贝,实现类的真正完全复制.<br/><br/>User.java<br/>[code=java]<br/>package test;<br/><br/>public class User implements Cloneable {<br/>	private int id;<br/>	private String name;<br/>	private int age;<br/>	private Website site;<br/><br/>	public User(


<!--more-->

本文概要:java中的深拷贝,实现类的真正完全复制.

<span style="color: #3366ff;">User.java</span>

package test;

public class User implements Cloneable {
private int id;
private String name;
private int age;
private Website site;

public User() {
this.site=new Website();
}

public User(int id, String name, int age,String url) {
this();
this.id = id;
this.name = name;
this.age = age;
this.site.setUrl(url);
}

public int getId() {
return id;
}

public void setId(int id) {
this.id = id;
}

<!--more-->

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

public String toString() {
return "{id:" + id + ",name:" + name + ",age:" + age + ",site:"+site.getUrl()+"}";
}

@Override
public Object clone() throws CloneNotSupportedException {
User u=new User();
u=(User)super.clone();
u.site=(Website)this.site.clone();
return u;
}

public void setSite(Website site) {
this.site = site;
}

public Website getSite() {
return site;
}
}

<span style="color: #3366ff;">Website.java</span>

package test;

public class Website implements Cloneable {
private String url;

public Website(){}

public Website(String url){
this.url=url;
}

public String getUrl() {
return url;
}

public void setUrl(String url) {
this.url = url;
}

@Override
public Object clone() throws CloneNotSupportedException {
return super.clone();
}
}

<span style="color: #3366ff;">CloneDemo.java</span>

package test;

public class CloneDemo {
public static void noClone(){
System.out.println("没有使用克隆");
User u1=new User(1,"章治鹏",22,"http://localhost/");
User u2=u1;
u2.setName("徐雄皓");
u2.getSite().setUrl("none");
System.out.println(u1);
System.out.println(u2);
System.out.println("----------------------------------");
}

public static void useClone() throws Exception{
System.out.println("使用克隆");
User u1=new User(1,"章治鹏",22,"http://localhost/");
User u2=(User)u1.clone();
u2.setName("徐雄皓");
u2.getSite().setUrl("none");
System.out.println(u1);
System.out.println(u2);
System.out.println("-----------------------------------");
}

public static void main(String[] args) throws Exception {
noClone();
useClone();
}
}