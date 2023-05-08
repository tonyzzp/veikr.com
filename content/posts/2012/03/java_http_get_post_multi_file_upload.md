```toml
title = "java的http请求(get/post/上传文件)(附源码下载)"
slug = "java_http_get_post_multi_file_upload"
description = ""
date = "2012-03-24 12:22:12"
author = "admin"
tags = ["get","http","java","post","下载","文件上传","源码"]
```

使用标准http协议实现，(HttpUrlConneciton)，不使用第三方包
<div></div>
<div><span style="color: #ff0000;">一、get请求</span></div>
<div>URL url=new URL("http://www.baidu.com/s?wd=abcdefg");</div>
<div>HttpURLConnection conn = (HttpURLConnection) url.openConnection();</div>
<div>InputStream is = conn.getInputStream();</div>
<div>is.read(.....</div>
<div></div>
<div></div>
<div><span style="color: #ff0000;">二、简单post请求</span></div>
<div>只需要将参数用 &amp; 和 = 连接，然后用流写出去就行了。</div>
<div>
<div>URL url=new URL("http://www.baidu.com/s");</div>
<div>HttpURLConnection conn = (HttpURLConnection) url.openConnection();</div>
<div>conn.setDoInput(true);</div>
<div>conn.setDoOutput(true);</div>
<div>OutputStream out=conn.getOutputStream();</div>
<div>out.write("wd=abcdefg&amp;wd2=hijklmn".getBytes());</div>
<div>out.flush();</div>
<div>out.close();</div>
<div>InputStream is = conn.getInputStream();</div>
<div>is.read(.....</div>
</div>
<div></div>
<div><span style="color: #ff0000;">三、上传多文件</span></div>
<div>比如实现如下请求</div>
<div>参数：</div>
<div>name=zzp</div>
<div>age=23</div>
<div></div>
<div>文件：</div>
<div>icon=new File(file1);</div>
<div>music=new File(audio);</div>
<div></div>
<div>需要向服务器发送的数据如下：</div>
<div>首先需要定义一个boundary，一个随机字符串即可，但整个请求过程中需要是一致的。</div>
<div>BOUNDARY="abcdefg";</div>
<div>首先需要</div>
<div>conn.setRequestProperty("Content-Type","multipart/form-data;boundary=abcdefg");</div>
<div></div>
<div>全部数据请求如下(包括内容中的引号。包括所有换行与空行，换行符是\r\n)(两个横线之间的是需要发送的全部内容):</div>
<div>排版很麻烦。。换行总是被去掉，所以以下用[\r\n]表示换行，程序中直接往流里写\r\n就行了。</div>

<hr />

<div>--abcdefg[\r\n]</div>
<div>Content-Disposition:form-data;name="name"[\r\n]</div>
<div>[\r\n]</div>
<div>zzp[\r\n]</div>
<div>--abcdefg[\r\n]</div>
<div>Content-Disposition:form-data;name="age"[\r\n]</div>
<div>[\r\n]</div>
<div>23[\r\n]</div>
<div>--abcdefg[\r\n]</div>
<div>Content-Disposition:form-data;name="icon";filename="file1其实这个是随便的"[\r\n]</div>
<div>Content-Type:image/png[\r\n]</div>
<div>[\r\n]</div>
<div>file1.getBytes()[\r\n]</div>
<div>--abcdefg[\r\n]</div>
<div>Content-Disposition:form-data;name="music";filename="mymusic.mp3"[\r\n]</div>
<div>Content-Type:audio/mpeg[\r\n]</div>
<div>[\r\n]</div>
<div>audio.getBytes()[\r\n]</div>
<div>--abcdefg--</div>
<div>

<hr />

</div>
<div>源码下载：</div>
<div><a href="http://veikr.com/wp-content/uploads/2012/03/zzpCommon.zip">zzpCommon</a></div>