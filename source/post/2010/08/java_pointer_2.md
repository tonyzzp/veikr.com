```toml
title = "Java中的指针(二)"
slug = "java_pointer_2"
desc = ""
date = "2010-08-05 10:46:13"
author = "admin"
tags = ["java","pointer"]
```

本文摘要:接着上次的来,讲java中的指针.上篇文章中举了个例子,把某对象存入session,再取出来,改变其中的变量值,那么不需要再进行session.setAttribute,但是session中的对象也已经跟着改变了.这次再举个例子,是list<br/>直接看代码<br/><br/><br/>User.java<br/>[code=java]<br/>package test;<br/><br/>public class User implements Cloneable {<br/>	private int id;<br/>	private String name;<br/>...


<!--more-->

本文摘要:接着上次的来,讲java中的指针.上篇文章中举了个例子,把某对象存入session,再取出来,改变其中的变量值,那么不需要再进行session.setAttribute,但是session中的对象也已经跟着改变了.这次再举个例子,是list
直接看代码

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

<!--more-->

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

@Override
public Object clone() throws CloneNotSupportedException {
return super.clone();
}
}

<span style="color: #3366ff;">ListDemo.java</span>

package test;

import java.util.ArrayList;
import java.util.List;

public class ListDemo {
public static void main(String[] args) {
List list=new ArrayList();
for(int i=0;i&lt;3;i++){
User u=new User(i,"第"+i+"号",20+i);
list.add(u);
}
System.out.println(list);
for(User u:list){
u.setName("一样的名字");
}
System.out.println(list);
}
}

执行结果是什么呢?.
你肯定已经猜到了.
[{id:0,name:第0号,age:20}, {id:1,name:第1号,age:21}, {id:2,name:第2号,age:22}]
[{id:0,name:一样的名字,age:20}, {id:1,name:一样的名字,age:21}, {id:2,name:一样的名字,age:22}]

再下一次中,将会更深一步讲解java中的探针.
文章写的不好,班门弄斧了,高手莫笑.