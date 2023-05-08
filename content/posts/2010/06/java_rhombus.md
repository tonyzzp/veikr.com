```toml
title = "用java输出一个菱形"
slug = "java_rhombus"
desc = ""
date = "2010-06-09 15:35:28"
author = "admin"
tags = ["java","图形","菱形","输出"]
```

<p>在学编程的循环语句时经常会遇到要输出一个特定规则图形的题目,不管是什么语言,几乎都有这样的题目.<br />今天去公司笔试,也遇到了这样的题目,写了好长时间,写出来了,考官也没有认真看,只是说出这道题只是考一下循环语句.<br />回来后我又试了下,写的程序有些问题,然后又小小改进了一下,可以了.<br />代码如下.</p><p><span style="color: rgb(51, 102, 255); "><span style="font-size: large; ">用java输出一个菱形</span></span></p>...


<!--more-->

<p>在学编程的循环语句时经常会遇到要输出一个特定规则图形的题目,不管是什么语言,几乎都有这样的题目.<br />今天去公司笔试,也遇到了这样的题目,写了好长时间,写出来了,考官也没有认真看,只是说出这道题只是考一下循环语句.<br />回来后我又试了下,写的程序有些问题,然后又小小改进了一下,可以了.<br />代码如下.</p><p><span style="color: rgb(51, 102, 255); "><span style="font-size: large; ">用java输出一个菱形</span></span></p><p><p>package org.zzp.test;</p><p>&nbsp;</p><p>public class PrintRhombus {</p><p><span class="Apple-tab-span" style="white-space:pre">	</span>public static void main(String[] args) {</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>int n=4;</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>for(int i=0;i&lt;9;i++){</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>for(int j=0;j&lt;Math.abs(n);j++){</p><p><span class="Apple-tab-span" style="white-space:pre">				</span>System.out.print(&quot; &quot;);</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>}</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>for(int j=0;j&lt;9-2*Math.abs(n);j++){</p><p><span class="Apple-tab-span" style="white-space:pre">				</span>System.out.print(&quot;*&quot;);</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>}</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>for(int j=0;j&lt;Math.abs(n);j++){</p><p><span class="Apple-tab-span" style="white-space:pre">				</span>System.out.print(&quot; &quot;);</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>}</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>System.out.println();</p><p><span class="Apple-tab-span" style="white-space:pre">				</span>n--;</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>}</p><p><span class="Apple-tab-span" style="white-space:pre">	</span>}</p><p>}</p></p>
