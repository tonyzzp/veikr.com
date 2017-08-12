```toml
title = "jsp部分乱码的解决办法"
slug = "jsp_messy_resolving"
desc = ""
date = "2010-04-23 14:59:32"
author = "admin"
tags = ["jsp","乱码","汉字"]
```

在用eclipse+dreamwaver做jsp的时候，发生了一件很奇怪的乱码问题同一个网页部分乱码我先经过一个servlet从数据库中查出数据  然后放到list里 发送到jsp页面我用了filter来控制编码为utf-8这个网页中的内容显示正常 但是从servlet传过来的东西是乱码在用eclipse+dreamwaver做jsp的时候，发生了一件很奇怪的乱码问题同一个网页部分乱码我先经过一个servlet从数据库中查出数据  然后放到list里 发送到jsp页面我用了filter来控制编码为utf-8这个网页中的内容显示正常 但是从servlet传过来的东西是乱码在用eclipse+dreamwaver做jsp的时候，发生了一件很奇怪的乱码问题,同一个网页部分乱码.我先经过一个servlet从数据库中查出数据  然后放到list里 发送到jsp页面,我用了filter来控制编码为utf-8,这个网页中的内容显示正常 ,但是从servlet传过来的东西是乱码


<!--more-->

<p>在用eclipse+dreamwaver做jsp的时候，发生了一件很奇怪的乱码问题</p>  <p>同一个网页部分乱码</p>  <p>我先经过一个servlet从数据库中查出数据&#160; 然后放到list里 发送到jsp页面</p>  <p>我用了filter来控制编码为utf-8</p>  <p>这个网页中的内容显示正常 </p>  <p>但是从servlet传过来的东西是乱码</p>  <p>我在serlvet里加了句</p>  <p>response.setCharacterEncoding(&quot;utf-8&quot;);</p>  <p>response.setContentType(&quot;text/html;charset=utf-8&quot;);</p>  <p>现在好了，servlet传过去的东西正常了。结果网页上的其他静态内容乱码了。。。</p>  <p>搞了好半天。</p>  <p>后来发现个问题</p>  <p>影响乱码的有2个原因</p>  <p>1、setContentType(&quot;text/html;charset=utf-8&quot;);</p>  <p>另一个重要的原因就是文件本身的编码。就是你这个.jsp文件的编码，这个也要一致才行</p>  <p>而eclipse和dreamwaver的文件编码不一样 所以导致了问题。</p>  <p>解决办法是用记事本打开jsp文件&#160;&#160; 另存为&#160; 编码选utf-8</p>  <p>然后就是</p>  <p>response.setCharacterEncoding(&quot;utf-8&quot;); </p>  <p>response.setContentType(&quot;text/html;charset=utf-8&quot;);</p>  <p>&lt;meta http-equiv=&quot;Content-Type&quot; content=&quot;text/html; charset=utf-8&quot;&gt;</p>  <p>&#160;</p>  <p>这些东西当然也要一致。</p>  <p>如果这时你在eclipse里发现文件看起来是乱码</p>  <p>那么很简单</p>  <p>在这个文件上点右键--选属性</p>  <p>在resource选项卡中&#160; 选编码为utf-8就可以了。</p>
