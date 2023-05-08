```toml
title = "go语言的中'继承'"
slug = "golang_extend"
description = ""
date = "2012-07-21 20:17:13"
author = "admin"
tags = ["go","继承","语言"]
```

最近看了下go语言，以前都只会java，则开始接触go语言时发现和java实在是有太多太多的不同，还有些不习惯，但慢慢的觉得还是挺有意思的。虽然学go语言感觉好像根本用不上，但多看看别的语言也是不错的。go语言默认是没有继承的，但结构体支持匿名字段，可以利用这个来实现"继承"。废话不多说，直接上代码，很简单，一看就会。

先大概说下这段代码，看起来会更方便些。

类Human。有2个字段：name,sex。有2个方法：walk，eat。

类SuperMan。有3个字段：Human，name，level。有2个方法：eat，fly。

这是标准说法，但你可以这么理解：SuperMan继承了Human，当然同样继承了所有字段和所有方法。同时又加入了自己的两个字段，其中有一个字段和父类是同名的，另外重写了父类中的一个方法，也添加了自己的一个方法。

代码如下：

&nbsp;
<pre class="brush:py">package main 

import(
	"fmt"
)

type Human struct{
	name string
	sex string
}

func (h Human) Eat(){
	fmt.Println("Human.Eat:",h)
}

func (h Human) Walk(){
	fmt.Println("Human.Walk:",h)
}

type SuperMan struct{
	Human
	name string
	level int
}

func (s SuperMan) Eat(){
	fmt.Println("SuperMan.Eat:",s)
}

func (s SuperMan) Fly(){
	fmt.Println("I believe I can fly!",s)
}

func test(h Human){
	fmt.Println("test pass!")
}

func main() {
	h:=Human{"zzp","man"}
	h.Eat()//调用自己的方法
	h.Walk()//调用自己的方法

	s:=SuperMan{Human{"sm","no"},"myname",99}

	fmt.Println(s.name)//myname
	fmt.Println(s.Human.name)//sm
        fmt.Println(s.sex)//no
        fmt.Println(s.Human.sex)//no

	s.Walk()//调用父类中的方法
	s.Eat()//调用自己重写的父类的方法
	s.Human.Eat()//调用父类中被自己重写的方法，这点比java高级
	s.Fly()//调用自己的方法

	test(h)
	//test(s)//导致错误，方法需要Human类型，但传的是SuperMan类型
	test(s.Human)//正确
}</pre>
&nbsp;

代码很简单，自己把代码复制出来运行一下，然后一行行对照着看，很容易就理解了。也没什么好讲的。