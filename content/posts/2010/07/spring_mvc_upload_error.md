```toml
title = "使用spring  mvc上传文件的常见错误解决办法"
slug = "spring_mvc_upload_error"
desc = ""
date = "2010-07-08 13:47:16"
author = "admin"
tags = ["java","mvc","spring","文件上传","解决办法","错误"]
```

<p>本文摘要：在使用spring mvc上传文件时的常见错误的解决办法&nbsp;1、 异常：org.apache.catalina.connector.RequestFacade cannot be cast to org.springframework.web.multipart.MultipartHttpServletRequest解决办法：在spring里面配置   重点：id一定要是mult</p>


<!--more-->

<p>本文摘要：在使用spring mvc上传文件时的常见错误的解决办法</p><p>&nbsp;</p><p>1、 <span style="color: rgb(255, 0, 0); ">异常：org.apache.catalina.connector.RequestFacade cannot be cast to org.springframework.web.multipart.MultipartHttpServletRequest</span></p><p><span style="color: rgb(51, 153, 102); ">解决办法：在spring里面配置 </span></p><p><bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"><property name="maxUploadSize" value="100000"></property></bean><span style="color: rgb(51, 153, 102); ">  重点：id一定要是multipartResolver，否则也会出同样的错误</span></p><p>&nbsp;</p><p>2、 <span style="color: rgb(255, 0, 0); ">异常：nested exception is java.lang.NoClassDefFoundError: org/apache/commons/fileupload/FileItemFactory</span></p><p><span style="color: rgb(51, 153, 102); ">解决办法：需要common-fileupload.jar包</span></p><p>&nbsp;</p><p>3、<span style="color: rgb(255, 0, 0); ">异常：java.lang.ClassNotFoundException: org.apache.commons.io.output.DeferredFileOutputStream</span></p><p><span style="color: rgb(51, 153, 102); ">解决办法：需要common-io.jar包</span></p>
