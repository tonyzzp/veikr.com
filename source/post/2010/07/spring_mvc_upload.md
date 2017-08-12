```toml
title = "使用spring  mvc上传文件的简单教程"
slug = "spring_mvc_upload"
desc = ""
date = "2010-07-08 10:41:53"
author = "admin"
tags = ["java","mvc","spring","教程","文件","文件上传"]
```

本文概要：使用spring mvc进行简单的文件上传。<br/><br/>1、首先在spring中配置一个bean<br/>[code=xml]<br/><bean id="multipartResolver"<br/>		class="org.springframework.web.multipart.commons.CommonsMultipartResolver"><br/>		<property name="maxUploadSize" value="100000" />	</bean><br/>[/code]<br/><font color="Red">注意：这个bean的id一定要是multipartResolver，不然会出错</font><br/>...


<!--more-->

本文概要：使用spring mvc进行简单的文件上传。

1、首先在spring中配置一个bean

[xml]
&lt;bean id=&quot;multipartResolver&quot;
		class=&quot;org.springframework.web.multipart.commons.CommonsMultipartResolver&quot;&gt;
		&lt;property name=&quot;maxUploadSize&quot; value=&quot;100000&quot; /&gt;	&lt;/bean&gt;
[/xml]


<span style="color: red;">注意：这个bean的id一定要是multipartResolver，不然会出错</span>

2、写UploadFile.java

[java]
package zzp.bean;
public class UploadFile {
	private byte[] file;
	private String message;
	public byte[] getFile() {
		return file;
	}
	public void setFile(byte[] file) {
		this.file = file;
	}
	public String getMessage() {
		return message;
	}
	public void setMessage(String message) {
		this.message = message;
	}
[/java]



3、写上传控件

[java]
package zzp.controller;
import java.io.File;
import java.util.HashMap;
import java.util.Map;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import org.springframework.util.FileCopyUtils;
import org.springframework.validation.BindException;
import org.springframework.web.bind.ServletRequestDataBinder;
import org.springframework.web.multipart.MultipartHttpServletRequest;
import org.springframework.web.multipart.commons.CommonsMultipartFile;
import org.springframework.web.multipart.support.ByteArrayMultipartFileEditor;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.SimpleFormController;
import zzp.bean.UploadFile;
public class UploadController extends SimpleFormController {
	@Override
	protected ModelAndView onSubmit(HttpServletRequest request,
			HttpServletResponse response, Object command, BindException errors)
			throws Exception {
		UploadFile bean=(UploadFile)command;
		byte[] bytes=bean.getFile();&lt;br/&gt;		
		MultipartHttpServletRequest multireq=(MultipartHttpServletRequest)request;
		CommonsMultipartFile file=(CommonsMultipartFile) multireq.getFile(&quot;file&quot;);
		File save=new File(&quot;g:/upload/&quot;+file.getOriginalFilename());
		FileCopyUtils.copy(bytes, save);
		Map map=new HashMap();
		map.put(&quot;status&quot;, bean.getMessage());
		return new ModelAndView(getSuccessView(),map);
	}
	@Override
	protected void initBinder(HttpServletRequest request,
			ServletRequestDataBinder binder) throws Exception {
		binder.registerCustomEditor(byte[].class, new ByteArrayMultipartFileEditor());
	}
}
[/java]



4、配置spring

[xml]
&lt;bean class=&quot;org.springframework.web.servlet.handler.SimpleUrlHandlerMapping&quot;&gt;
		&lt;property name=&quot;mappings&quot;&gt;
			&lt;props&gt;	
			&lt;prop key=&quot;upload.htm&quot;&gt;upload&lt;/prop&gt;
			&lt;/props&gt;	
	&lt;/property&gt;	&lt;/bean&gt;
	&lt;bean id=&quot;upload&quot; class=&quot;zzp.controller.UploadController&quot;&gt;
		&lt;property name=&quot;commandClass&quot; value=&quot;zzp.bean.UploadFile&quot; /&gt;	
	&lt;property name=&quot;formView&quot; value=&quot;upload&quot; /&gt;	
	&lt;property name=&quot;successView&quot; value=&quot;uploadok&quot; /&gt;	&lt;/bean&gt;
[/xml]



5、编写jsp页面
upload.jsp

[html]
&lt;form action=&quot;upload.htm&quot; method=&quot;post&quot; enctype=&quot;multipart/form-data&quot;&gt;
&lt;input type=&quot;file&quot; name=&quot;file&quot;/&gt;
&lt;input type=&quot;text&quot; name=&quot;message&quot;/&gt;
&lt;button type=&quot;submit&quot;&gt;上传&lt;/button&gt;
&lt;/form&gt;
[/html]



uploadok.jsp

[java]${status}[/java]



<span style="color: green;">访问http://localhost:8080/springhibernate/upload.htm即可上传文件</span>。

&nbsp;