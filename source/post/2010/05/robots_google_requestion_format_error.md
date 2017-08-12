```toml
title = "robots.txt文件在google中多一个问号，提示格式有误"
slug = "robots_google_requestion_format_error"
desc = ""
date = "2010-05-22 11:50:23"
author = "admin"
tags = ["google","robots","seo"]
```

<p>&nbsp;robots.txt文件在google网站管理工具中总是提示第一句格式有错误</p><p>这是我的robots.txt文件</p><p>明明是正确的 &nbsp;但在google网站管理工具中总是提示第一行格式有错误</p><p>在第一行前面多出了一个问题 &nbsp;</p><p><p>User-agent: *</p><p>Disallow: /SCRIPT/</p><p>Disallow: /FUNCTION/</p><p>Disallow: /ADMIN/</p>...</p>


<!--more-->

<p>&nbsp;robots.txt文件在google网站管理工具中总是提示第一句格式有错误</p><p>这是我的robots.txt文件</p><p>明明是正确的 &nbsp;但在google网站管理工具中总是提示第一行格式有错误</p><p>在第一行前面多出了一个问题 &nbsp;</p><p><p>User-agent: *</p><p>Disallow: /SCRIPT/</p><p>Disallow: /FUNCTION/</p><p>Disallow: /ADMIN/</p><p>Disallow: /DATA/</p><p>Disallow: /XML-RPC</p><p>Disallow: /CSS</p><p>Disallow: /THEMES</p><p>&nbsp;</p><p>Sitemap:http://localhost/sitemap.xml</p><p>Sitemap:http://localhost/sitemap_wap.xml</p><p>&nbsp;</p><p>问题所在：编码应该为ANSI</p><p>解决办法：先将robots.txt文件下载下来，用记事本打开，另存为，编码选择为ANSI.再将文件上传到网站根目录，覆盖，问题解决。请耐心等待google重新下载你的robots文件</p></p>
