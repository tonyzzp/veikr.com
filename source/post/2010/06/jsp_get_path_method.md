```toml
title = "jsp中获取路径的各种方法"
slug = "jsp_get_path_method"
desc = ""
date = "2010-06-11 11:11:38"
author = "admin"
tags = ["java","jsp","request","路径"]
```

<p>&nbsp;本文概要:主要简单介绍jsp中获取路径的各种方法.<br />比如request.getRequestURI &nbsp; &nbsp; request,getRequestURL &nbsp; &nbsp;request.getContextPath &nbsp; &nbsp;request.getRealpath等等</p><p>&nbsp;尝试把下面的代码放到不同的站点、不同路径下运行 查看效果</p><p>&nbsp;</p><p><p>request.getRealPath(&quot;&quot;):&lt;br /&gt;</p>...</p>


<!--more-->

<p>&nbsp;本文概要:主要简单介绍jsp中获取路径的各种方法.<br />比如request.getRequestURI &nbsp; &nbsp; request,getRequestURL &nbsp; &nbsp;request.getContextPath &nbsp; &nbsp;request.getRealpath等等</p><p>&nbsp;尝试把下面的代码放到不同的站点、不同路径下运行 查看效果</p><p>&nbsp;</p><p><p>request.getRealPath(&quot;&quot;):&lt;br /&gt;</p><p>&lt;%=request.getRealPath(&quot;&quot;)%&gt;&lt;p/&gt;</p><p>&nbsp;</p><p>request.getRealPath(&quot;/&quot;):&lt;br /&gt;</p><p>&lt;%=request.getRealPath(&quot;/&quot;)%&gt;&lt;p/&gt;</p><p>&nbsp;</p><p>request.getScheme():&lt;br/&gt;&lt;%=request.getScheme() %&gt;&lt;p/&gt;</p><p>request.getServerName():&lt;br/&gt;&lt;%=request.getServerName() %&gt;&lt;p/&gt;</p><p>request.getServerPort():&lt;br/&gt;&lt;%=request.getServerPort() %&gt;&lt;p/&gt;</p><p>request.getMethod():&lt;br/&gt;&lt;%=request.getMethod() %&gt;&lt;p/&gt;</p><p>request.getRequestedSessionId():&lt;br/&gt;&lt;%=request.getRequestedSessionId() %&gt;&lt;p/&gt;</p><p>request.getRequestURI():&lt;br/&gt;&lt;%=request.getRequestURI() %&gt;&lt;p/&gt;</p><p>request.getRequestURL():&lt;br/&gt;&lt;%=request.getRequestURL() %&gt;&lt;p/&gt;</p><p>request.getQueryString():&lt;br/&gt;&lt;%=request.getQueryString() %&gt;&lt;p/&gt;</p><p>request.getServletPath():&lt;br/&gt;&lt;%=request.getServletPath() %&gt;&lt;p/&gt;</p><p>request.getProtocol():&lt;br/&gt;&lt;%=request.getProtocol() %&gt;&lt;p/&gt;</p><p>request.getContextPath():&lt;br/&gt;&lt;%=request.getContextPath() %&gt;&lt;p/&gt;</p><p>request.getSession().getServletContext().getRealPath(request.getRequestURI()):&lt;br/&gt;&lt;%=request.getSession().getServletContext().getRealPath(request.getRequestURI()) %&gt;&lt;p/&gt;</p></p>
