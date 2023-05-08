```toml
title = "php文件上传 [function.move-uploaded-file]: failed to open stream 错误解决办法"
slug = "php_upload_function_move_uploaded_file_failed_open_stream"
description = ""
date = "2010-04-23 14:52:45"
author = "admin"
tags = ["php","文件上传","错误"]
```

php文件上传中出现如下错误Warning: move_uploaded_file(upload/pal4bz111.jpg) [function.move-uploaded-file]: failed to open stream: No such file or directory inE:\Eclipse\Workspace\PHPTest\file_upload\t2.php on line 24 Warning: move_uploaded_file() [function.move-uploaded-file]: Unable to move 'D:\xampplite\tmp\php7FC5.tmp' to 'upload/pal4bz111.jpg' inE:\Eclipse\Workspace\PHPTest\file_upload\t2.php on line 24 Stored in: upload/pal4bz111.jpg


<!--more-->

<p>php文件上传中出现如下错误 </p>  <p>&#160;</p>  <p><b>Warning</b>: move_uploaded_file(upload/pal4bz111.jpg) [function.move-uploaded-file]: failed to open stream: No such file or directory in<b>E:\Eclipse\Workspace\PHPTest\file_upload\t2.php</b> on line <b>24</b>     <br /><b>Warning</b>: move_uploaded_file() [function.move-uploaded-file]: Unable to move 'D:\xampplite\tmp\php7FC5.tmp' to 'upload/pal4bz111.jpg' in<b>E:\Eclipse\Workspace\PHPTest\file_upload\t2.php</b> on line <b>24</b>     <br />Stored in: upload/pal4bz111.jpg</p>  <p>&#160;</p>  <p>解决办法</p>  <p>将</p>  <p>move_uploaded_file($_FILES[&quot;file&quot;][&quot;tmp_name&quot;],&quot;<font color="#ff0000">upload/</font>&quot; . $_FILES[&quot;file&quot;][&quot;name&quot;])</p>  <p>改为</p>  <p>move_uploaded_file($_FILES[&quot;file&quot;][&quot;tmp_name&quot;],&quot;<font color="#ff0000">d:/</font>&quot; . $_FILES[&quot;file&quot;][&quot;name&quot;])</p>  <p>&#160;</p>  <p>注：windows环境</p>
