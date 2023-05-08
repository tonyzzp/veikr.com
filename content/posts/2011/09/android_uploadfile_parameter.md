```toml
title = "android上传文件的同时并传递参数(附源码下载)"
slug = "android_uploadfile_parameter"
description = ""
date = "2011-09-05 17:23:25"
author = "admin"
tags = ["httpclient","上传文件","参数"]
```

教你android平台如何上传文件并传递参数。

android的sdk中自带了apache的httpclient库，但是精简过的，只具有部分功能，所以有些功能的支持还是需要自己另外导入httpclient库的

先介绍下用到的主要类

httpclient，它把请求发到服务器，并接收服务器返回的结果

httppost，向服务器的请求，内容都放在这里面

multiPartEntity，multiPart实体，这里面装的有参数和文件

StringBody，装参数的

Filebody，装文件的

httpResponse，服务器的返回

&nbsp;

OK，开始吧

<!--more-->

首先创建HttpPost对象

HttpPost post=new HttpPost("http://veikr.com/myupload/upload.php");

创建File

File file=new File("/mnt/sdcard/info.txt");

创建multiPart实体

MultiPartEntity entity=new MultiPartEntity();

把参数和文件都装进去

entity.addPart("name",new StringBody("veikr.com"));

entity.addPart("file",new FileBody(file));

然后发送请求

HttpClient client=new DefaultHttpclient();

HttpResponse response=client.execute(post);

请求完成，就可以得到返回的结果了

response.getStatusLine().getStatusCode()

response.getEntity().getInputStream();

这里有个实用的方法

EntityUtils.toString(response.getEntity());可以直接把返回的结果转换为字符串

&nbsp;

OK，完工，很简单的。

大家可以自己装个xampp用php写个服务端，上传文件很好写，几句话就够了，可以到<a href="http://www.w3school.com.cn/php/index.asp" target="_blank">http://www.w3school.com.cn/</a> 看看教程

或者也可以直接用我写好的

地址是：http://veikr.com/myupload/upload.php

另附上<a title="android上传文件的同时并传递参数(php服务端源码)" href="http://veikr.com/201110/android_uploadfile_parameter_php.html" target="_blank">php端的代码</a>

参数：name

文件：file

只能上传512K以下的文件。没写其他的验证，不要把我的服务器搞挂就行了。。。

下面粘上全部代码，源码包下面有下载。

&nbsp;
```package zzp.t.uploadfile;

import java.io.File;
import java.io.IOException;
import org.apache.http.HttpResponse;
import org.apache.http.ParseException;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.mime.MultipartEntity;
import org.apache.http.entity.mime.content.FileBody;
import org.apache.http.entity.mime.content.StringBody;
import org.apache.http.impl.client.DefaultHttpClient;
import org.apache.http.util.EntityUtils;

import android.app.Activity;
import android.app.AlertDialog;
import android.app.ProgressDialog;
import android.os.AsyncTask;
import android.os.Bundle;
import android.widget.Toast;

public class MainActivity extends Activity {
	/** Called when the activity is first created. */
	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);
		final ProgressDialog dlg = new ProgressDialog(this);
		dlg.setMessage("上传中...");
		dlg.show();
		new AsyncTask&lt;Void, Void, HttpResponse&gt;() {
			@Override
			protected HttpResponse doInBackground(Void... params) {
				try {
					HttpPost post = new HttpPost(
							"http://veikr.com/myupload/upload.php");
					File file = new File("/mnt/sdcard/infor.txt");
					MultipartEntity multipart = new MultipartEntity();
					multipart.addPart("name", new StringBody("veikr.com"));
					multipart.addPart("file", new FileBody(file));
					HttpClient client = new DefaultHttpClient();
					post.setEntity(multipart);
					HttpResponse response = client.execute(post);
					return response;
				} catch (Exception e) {
					e.printStackTrace();
					return null;
				}
			}

			@Override
			protected void onPostExecute(HttpResponse result) {
				dlg.dismiss();
				if (result != null) {
					try {
						new AlertDialog.Builder(MainActivity.this)
								.setMessage(
										EntityUtils.toString(result.getEntity()))
								.create().show();
					} catch (ParseException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					} catch (IOException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				} else {
					Toast.makeText(MainActivity.this, "异常啊异常。。。", 0).show();
				}
			}
		}.execute();
	}
}```
<a href="http://veikr.com/assets/wp-content/uploads/2011/09/TestUploadFile.zip">源码包下载TestUploadFile</a>