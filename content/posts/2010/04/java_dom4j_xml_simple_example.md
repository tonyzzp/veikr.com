```toml
title = "java中使用dom4j读xml文件简单教程"
slug = "java_dom4j_xml_simple_example"
desc = ""
date = "2010-04-23 15:04:56"
author = "admin"
tags = ["dom4j","java","xml"]
```

java中用dom4j读取,修改,创建xml文件.功能强大还简单.


<!--more-->

<p>需要dom4j.jar文件 ，自行下载。</p>  <p>test.xml</p>  <pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  1: <span style="color: #0000ff">&lt;?</span>xml version=&quot;1.0&quot; encoding=&quot;gbk&quot;<span style="color: #0000ff">?&gt;</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  2: </pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  3: <span style="color: #0000ff">&lt;</span><span style="color: #800000">students</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  4:   <span style="color: #0000ff">&lt;</span><span style="color: #800000">person</span> <span style="color: #ff0000">sex</span>=<span style="color: #0000ff">&quot;男&quot;</span> <span style="color: #ff0000">age</span>=<span style="color: #0000ff">&quot;21&quot;</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  5:     <span style="color: #0000ff">&lt;</span><span style="color: #800000">id</span><span style="color: #0000ff">&gt;</span>1<span style="color: #0000ff">&lt;/</span><span style="color: #800000">id</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  6:     <span style="color: #0000ff">&lt;</span><span style="color: #800000">name</span><span style="color: #0000ff">&gt;</span>章治鹏<span style="color: #0000ff">&lt;/</span><span style="color: #800000">name</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  7:     <span style="color: #0000ff">&lt;</span><span style="color: #800000">homepage</span><span style="color: #0000ff">&gt;</span>http://blog.csdn.net/tonyzzp<span style="color: #0000ff">&lt;/</span><span style="color: #800000">homepage</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  8:   <span style="color: #0000ff">&lt;/</span><span style="color: #800000">person</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  9:   <span style="color: #0000ff">&lt;</span><span style="color: #800000">person</span> <span style="color: #ff0000">age</span>=<span style="color: #0000ff">&quot;20&quot;</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 10:     <span style="color: #0000ff">&lt;</span><span style="color: #800000">id</span><span style="color: #0000ff">&gt;</span>2<span style="color: #0000ff">&lt;/</span><span style="color: #800000">id</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 11:     <span style="color: #0000ff">&lt;</span><span style="color: #800000">name</span><span style="color: #0000ff">&gt;</span>徐雄皓<span style="color: #0000ff">&lt;/</span><span style="color: #800000">name</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 12:     <span style="color: #0000ff">&lt;</span><span style="color: #800000">homepage</span> <span style="color: #ff0000">boolean</span>=<span style="color: #0000ff">&quot;false&quot;</span><span style="color: #0000ff">&gt;</span>http://www.xxh.com<span style="color: #0000ff">&lt;/</span><span style="color: #800000">homepage</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 13:   <span style="color: #0000ff">&lt;/</span><span style="color: #800000">person</span><span style="color: #0000ff">&gt;</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 14: <span style="color: #0000ff">&lt;/</span><span style="color: #800000">students</span><span style="color: #0000ff">&gt;</span></pre></pre><pre>&#160;</pre><pre>&#160;</pre><pre>XMLStudentsParam.java</pre><pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  1: <span style="color: #0000ff">package</span> org.zzp.common.xml.dom4j;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  2: </pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  3: <span style="color: #0000ff">public</span> enum XMLStudentsParam {</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  4: 	id,name,homepage,sex,age</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  5: }</pre></pre><p>&#160;</p><p>&#160;</p><p>Dom4jReadDemo.java</p><pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  1: <span style="color: #0000ff">package</span> org.zzp.common.xml.dom4j;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  2: </pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  3: <span style="color: #0000ff">import</span> java.util.Iterator;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  4: <span style="color: #0000ff">import</span> java.util.List;</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  5: </pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  6: <span style="color: #0000ff">import</span> org.dom4j.Attribute;</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  7: <span style="color: #0000ff">import</span> org.dom4j.Document;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  8: <span style="color: #0000ff">import</span> org.dom4j.DocumentException;</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px">  9: <span style="color: #0000ff">import</span> org.dom4j.Element;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 10: <span style="color: #0000ff">import</span> org.dom4j.io.SAX
Reader;</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 11: </pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 12: <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> Dom4jReadDemo {</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 13:  <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">void</span> main(String[] args) {</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 14:   <span style="color: #0000ff">try</span> {</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 15:    Document doc=<span style="color: #0000ff">new</span> SAXReader().read(&quot;<span style="color: #8b0000">test.xml</span>&quot;);</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 16:    Element root=doc.getRootElement();</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 17:    System.out.println(&quot;<span style="color: #8b0000">根节点名：</span>&quot;+root.getName());</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 18:    List&lt;Element&gt; students=root.elements();</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 19:    System.out.println(&quot;<span style="color: #8b0000">共有学生数</span>&quot;+students.size()+&quot;<span style="color: #8b0000">\n</span>&quot;);</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 20:    <span style="color: #008000">//遍历每个学生</span></pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 21:    <span style="color: #0000ff">for</span>(Iterator&lt;Element&gt; it= students.iterator();it.hasNext();){</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 22:     Element student=(Element)it.next();</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 23:     List&lt;Element&gt; student_s=student.elements();</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 24:     <span style="color: #008000">//遍历每个学生的子标签</span></pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 25:     <span style="color: #0000ff">for</span>(Iterator&lt;Element&gt; its=student_s.iterator();its.hasNext();){</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 26:      Element param=(Element)its.next();</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 27:      <span style="color: #0000ff">switch</span>(XMLStudentsParam.valueOf(param.getName())){</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 28:      <span style="color: #0000ff">case</span> name:</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 29:       System.out.print(&quot;<span style="color: #8b0000">姓名：</span>&quot;);</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 30:       <span style="color: #0000ff">break</span>;</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 31:      <span style="color: #0000ff">case</span> id:</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 32:       System.out.print(&quot;<span style="color: #8b0000">编号：</span>&quot;);</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 33:       <span style="color: #0000ff">break</span>;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 34:      <span style="color: #0000ff">case</span> homepage:</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 35:       System.out.print(&quot;<span style="color: #8b0000">主页：</span>&quot;);</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 36:       <span style="color: #0000ff">if</span> (param.attribute(&quot;<span style="color: #8b0000">boolean</span>&quot;)!=<span style="color: #0000ff">null</span> &amp;&amp; !param.attribute(&quot;<span style="color: #8b0000">boolean</span>&quot;).getText().equals(&quot;<span style="color: #8b0000">true</span>&quot;)) {</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 37:        System.out.print(&quot;<span style="color: #8b0000">(网页未经验证)</span>&quot;);</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 38:       }</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 39:       <span style="color: #0000ff">break</span>;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 40:      }</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 41:      System.out.println(param.getText());</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 42:     }</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 43:     <span style="color: #008000">//遍历每个学生的属性</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 44:     <span style="color: #0000ff">for</span>(Iterator&lt;Attribute&gt; ita=student.attributeIterator();ita.hasNext();){</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 45:      Attribute a=(Attribute)ita.next();</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px
"> 46:      <span style="color: #0000ff">switch</span>(XMLStudentsParam.valueOf(a.getName())){</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 47:      <span style="color: #0000ff">case</span> sex:</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 48:       System.out.print(&quot;<span style="color: #8b0000">性别：</span>&quot;);</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 49:       <span style="color: #0000ff">break</span>;</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 50:      <span style="color: #0000ff">case</span> age:</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 51:       System.out.print(&quot;<span style="color: #8b0000">年龄：</span>&quot;);</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 52:       <span style="color: #0000ff">break</span>;</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 53:      }</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 54:      System.out.println(a.getText());</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 55:     }</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 56:     System.out.println();</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 57:    }</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 58:   } <span style="color: #0000ff">catch</span> (DocumentException e) {</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 59:    <span style="color: #008000">// TODO Auto-generated catch block</span></pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 60:    e.printStackTrace();</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 61:   }</pre><pre style="background-color: #ffffff; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 62:  }</pre><pre style="background-color: #eaeaea; margin: 0em; width: 100%; font-family: consolas,&#39;Courier New&#39;,courier,monospace; font-size: 12px"> 63: }</pre></pre>