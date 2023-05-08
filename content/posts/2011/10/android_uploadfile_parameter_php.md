```toml
title = "android上传文件的同时并传递参数(php服务端源码)"
slug = "android_uploadfile_parameter_php"
description = ""
date = "2011-10-26 16:29:33"
author = "admin"
tags = ["httpclient","php","上传文件","参数"]
```

之前写的   <a title="android上传文件的同时并传递参数(附源码下载)" href="http://veikr.com/201109/android_uploadfile_parameter.html" target="_blank">android上传文件的同时并传递参数</a>   的文章

今天有位朋友要php端的代码，现在帖出来吧。

其实如果你也可以直接用我写好的一个 http://veikr.com/myupload/upload.php 来测试

刚才去看了下，有人用过，传了4个文件在里面。

<!--more-->

&nbsp;
<pre>&lt;?php
//echo $_FILES["pic"]["name"];
//echo $_FILES["pic"]["type"];
//echo $_FILES["pic"]["size"];
if($_FILES["pic"]["size"]&gt;512*1024){
	echo $_POST["name"];
	echo "invalidate file type";
}else{
	move_uploaded_file($_FILES["file"]["tmp_name"],"testuploadfile/".$_FILES["file"]["name"]);
	echo $_FILES["file"]["name"];
	echo $_POST["name"];
}
?&gt;</pre>
<pre></pre>
<pre></pre>