```toml
title = "java中的指针(三)"
slug = "java_pointer_3"
desc = ""
date = "2010-08-12 15:43:23"
author = "admin"
tags = ["java","pointer"]
```

本文概要:前几篇文章中谈到了java中的指针.现在有个问题是,如果你先定义了一个对象,现在想把这个对象拿来用,会改变一些值.但是又不想影响到原来的对象,那该怎么办呢?方法是克隆.<br/><br/>User.java<br/>[code=java]<br/>package test;<br/><br/>public class User implements Cloneable {<br/>	private int id;<br/>	private Strin


<!--more-->

本文概要:前几篇文章中谈到了java中的指针.现在有个问题是,如果你先定义了一个对象,现在想把这个对象拿来用,会改变一些值.但是又不想影响到原来的对象,那该怎么办呢?方法是克隆.

<span style="color: #3366ff;">User.java</span>

package test;

public class User implements Cloneable {
private int id;
private String name;
private int age;

public User() {
}

public User(int id, String name, int age) {
this.id = id;
this.name = name;
this.age = age;
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

public String toString() {
return "{id:" + id + ",name:" + name + ",age:" + age + "}";
}

@Override
public Object clone() throws CloneNotSupportedException {
// TODO Auto-generated method stub
return super.clone();
}
}

<span style="color: red;">
注意:覆盖Object中的clone方法,但是查注意把protect改为public
另外需要注意,要实现cloneable接口,该接口中没有任何方法,只是个标志而已.
</span>

<span style="color: #3366ff;">CloneDemo.java</span>

package test;

public class CloneDemo {
public static void noClone(){
System.out.println("没有使用克隆");
User u1=new User(1,"章治鹏",22);
User u2=u1;
u2.setName("徐雄皓");
System.out.println(u1);
System.out.println(u2);
System.out.println("----------------------------------");
}

public static void useClone() throws Exception{
System.out.println("使用克隆");
User u1=new User(1,"章治鹏",22);
User u2=(User)u1.clone();
u2.setName("徐雄皓");
System.out.println(u1);
System.out.println(u2);
System.out.println("-----------------------------------");
}

public static void main(String[] args) throws Exception {
noClone();
useClone();
}
}

这样就完成了克隆,但这只是浅克隆.只有在类是简单类时才有效.假如某个类中还包含其他类,就需要进行深克隆.