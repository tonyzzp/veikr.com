```toml
title = "java中字符与ASCII码值的转换"
slug = "java_char_ascii"
description = ""
date = "2010-06-09 16:16:11"
author = "admin"
tags = ["ascii","java","字符","转换"]
```

<p>&nbsp;本文概要:简单的介绍java中字符与ASCII码值的相互转换</p><p>今天去公司笔试,考了一道加密解密的题目,其实很简单,所有的字符ASCII码值+10即完成加密.</p><p>其实很简单,只需把char强制类型转换为int即得到了char的ASCII码值.</p><p>代码:</p><p>&nbsp;</p><p>package org.zzp.test;</p><p>&nbsp;</p><p>public class TestASCII {</p><p><span class="Apple-tab-span" style="white-space:pre">	</span>public static void main(String[] args) {</p><p>...</p><p>&nbsp;</p>


<!--more-->

<p>&nbsp;本文概要:简单的介绍java中字符与ASCII码值的相互转换</p><p>今天去公司笔试,考了一道加密解密的题目,其实很简单,所有的字符ASCII码值+10即完成加密.</p><p>其实很简单,只需把char强制类型转换为int即得到了char的ASCII码值.</p><p>代码:</p><p>&nbsp;</p><p>package org.zzp.test;</p><p>&nbsp;</p><p>public class TestASCII {</p><p><span class="Apple-tab-span" style="white-space:pre">	</span>public static void main(String[] args) {</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>String a=&quot;abcdefg&quot;;</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>StringBuffer sb=new StringBuffer();</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>for(char c:a.toCharArray()){</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>System.out.println((int)c);</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>//c=(char)((int)c+10);</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>c+=1;</p><p><span class="Apple-tab-span" style="white-space:pre">			</span>sb.append(c);</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>}</p><p><span class="Apple-tab-span" style="white-space:pre">		</span>System.out.println(sb);</p><p><span class="Apple-tab-span" style="white-space:pre">	</span>}</p><p>}</p><p>&nbsp;</p>
