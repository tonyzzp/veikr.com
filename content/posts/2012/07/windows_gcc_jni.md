```toml
title = "在windows下使用gcc编译jni的简单教程"
slug = "windows_gcc_jni"
description = ""
date = "2012-07-29 21:12:06"
author = "admin"
tags = ["gcc","java","jni","mingw","教程"]
```

<span style="color: #0000ff;">1、安装MinGW</span>，这个可以为windows提供gcc编译环境。

到<a href="http://sourceforge.net/projects/mingw/files/">http://sourceforge.net/projects/mingw/files/</a> 下载，是.exe的，在线安装，但很快。安装时选c compiler就行了，也可以把c++的也装了。安装完成后，为了方便使用最好配置一下环境变量。把MinGW/bin目录加入环境变量。

&nbsp;

<span style="color: #0000ff;">2、编写JAVA文件</span>。

写个最简单的：
<pre class="brush:java">public class Test {

	static{
		System.loadLibrary("lib");
	}

	static native void print(int a);

	public static void main (String args[]) {
		print(3);
	}
}</pre>
然后编译java文件 javac Test.java

<!--more-->

<span style="color: #0000ff;">3、生成.h头文件</span>。

javah Test

就这一个简单的命令就行了。(如果有包名，需要类似javah com.google.Test这样，注意命令行目录)

&nbsp;

<span style="color: #0000ff;">4、实现.c文件</span>。

.h生成后可以打开看一下，里面有个方法是需要自己实现的。如下：

JNIEXPORT void JNICALL Java_Test_print
(JNIEnv *, jclass, jint);

这个就是我们java里写的print方法了。

这里简单说一下c的方法名命名规则是Java_packagename_Classname_method

要实现的就是这个方法了。
<pre class="brush:cpp">#include &lt;stdio.h&gt;
#include &lt;jni.h&gt;
#include "Test.h"

JNIEXPORT void JNICALL Java_Test_print(JNIEnv *env, jclass jthiz,jint a){
	printf("Hello JNI!%d\n",a);
}</pre>
这里简单说一下，include的第一个是c的标准输入输出库，第2个是jni库，这个文件是在java/include里的，第3个就是自己刚才生成的头文件了，注意一定要用“”，不是用&lt;&gt;

方法的前2个参数是固定的，不用管。

&nbsp;

<span style="color: #0000ff;">5、把.c文件编译成.dll</span>

命令：

gcc -I%JAVA_HOME%\include -I%JAVA_HOME%\include\win32 -shared -Wl,--kill-at -s -o lib.dll Test.c

&nbsp;

解释一下：

-I(大写字母I，include的意思)是加入自己的库，也就是告诉编译器jni.h的位置。当然不加这个参数也可以，自己把jni.h和jni_md.h文件复制出来和Test.c放一起，另外include改为""

-shared表示编译成.dll库文件

-s参数可以大幅减小.dll文件的大小，不加也可以

-o表示目标文件名，不加也可以，会有默认名，但要自己改成java中导入库的名字，这里是lib

-Wl,--kill-at  这个参数我也不明白，反正要加，不加能编译成.dll，但java中会报错。(是小写字母L，不是数字1)

&nbsp;

好了，java Test看结果吧。