```toml
title = "android中service的简单实现"
slug = "android_service"
desc = ""
date = "2012-06-10 15:56:43"
author = "admin"
tags = ["android","BinderProxy","ClassCastException","IBinder","service","服务"]
```

简单介绍下android中service的用法，其实我也没太研究明白，只是拿出来分享一下。

废话不多说，直接上代码比较好。

一、首先你需要有个类，继承自service。
<pre class="brush:java">package zzp.test.service;

import android.app.Service;
import android.content.Intent;
import android.os.Binder;
import android.os.IBinder;

public class PushService extends Service {

	public class PushBinder extends Binder {
		public void downLoadFile(final String url) {
			new Thread() {
				@Override
				public void run() {
					super.run();
					System.out.println("开始下载:" + url);
					try {
						Thread.sleep(5000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
					System.out.println("下载完成");
				}
			}.start();
		}
	}

	private final PushBinder binder = new PushBinder();

	@Override
	public IBinder onBind(Intent arg0) {
		// TODO Auto-generated method stub
		System.out.println("onBind");
		return binder;
	}

	@Override
	public void onCreate() {
		// TODO Auto-generated method stub
		super.onCreate();
		System.out.println("onCreate");
	}

	@Override
	public void onDestroy() {
		// TODO Auto-generated method stub
		super.onDestroy();
		System.out.println("onDestroy");
	}

	@Override
	public void onRebind(Intent intent) {
		// TODO Auto-generated method stub
		super.onRebind(intent);
		System.out.println("onRebind");
	}

	@Override
	public void onStart(Intent intent, int startId) {
		// TODO Auto-generated method stub
		super.onStart(intent, startId);
		System.out.println("onStart:" + startId);
	}

	@Override
	public boolean onUnbind(Intent intent) {
		// TODO Auto-generated method stub
		System.out.println("onUnbind");
		return super.onUnbind(intent);
	}
}</pre>
onCreate:在服务首次创建时调用。

onDestroy:在服务被销毁时调用。

onStart:当使用startService时调用此方法，如果是第一次调用，则会先调用onCreate来创建服务。在服务已经启动的情况下，每次使用startService方法都会调用onStart方法，但服务只会有一个，不会产生多个。(现已改为onStartCommand，onStart不再建议使用)。

onBind:使用bindService时调用此方法,返回一个IBinder，用来与服务进行交互。

onUnBind:使用unbindService时调用。unbindService只能在服务已经绑定状态才会能调用，否则将会抛异常。在一个activity中绑定了service,当activity退出时必须unbindService，否则也会有异常。

&nbsp;

主要就这几个方法了，这里简单说下service的生命周期。

1、当第一次调用startService或bindService(加入BIND_AUTO_CREATE  flag)时，服务会被创建，onCreate方法被调用。

2、每一次使用startService时onStart方法都会被调用，多次使用bindService，onBind方法只会调用一次。

3、使用stopService会停止服务，onDestroy方法被调用。使用unbindService也会停止服务，onunBind和onDestroy会被调用。但这里有个前提：如果你同时用了startService和bindService，那你必须同时调用unBindService和stopService，服务才会真正被停止。

&nbsp;

在service中onBind方法返回一个IBinder，用此来与服务进行通信交互。所以服务的一般用法是，在activity中先startServie来启用服务，然后使用bindService来获得IBinder，与服务交互。activity退出时必须调用unBindService,但服务还不会停止，当你不再服务此服务时，调用stopService来停止服务。

&nbsp;
<pre class="brush:java">package zzp.test.service;

import zzp.test.service.PushService.PushBinder;
import android.app.Activity;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;

public class TestServiceActivity extends Activity implements OnClickListener {

	Button start, stop, bind, unbind, download;
	ServiceConnection conn;
	PushBinder push;
	boolean binded = false;

	/** Called when the activity is first created. */
	@Override
	public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.main);

		start = (Button) findViewById(R.id.start);
		stop = (Button) findViewById(R.id.stop);
		bind = (Button) findViewById(R.id.bind);
		unbind = (Button) findViewById(R.id.unbind);
		download = (Button) findViewById(R.id.download);

		start.setOnClickListener(this);
		stop.setOnClickListener(this);
		bind.setOnClickListener(this);
		unbind.setOnClickListener(this);
		download.setOnClickListener(this);
		conn = new ServiceConnection() {

			@Override
			public void onServiceConnected(ComponentName name, IBinder service) {
				// TODO Auto-generated method stub
				System.out.println("onServiceConnected");
				binded = true;
				print(name);
				print(service.getClass().getName());
				push = (PushBinder) service;
			}

			@Override
			public void onServiceDisconnected(ComponentName name) {
				// TODO Auto-generated method stub
				System.out.println("onServiceDisconnected");
				binded = false;
				print(name);
			}

		};
	}

	@Override
	public void onClick(View v) {
		Intent intent = new Intent(this, PushService.class);
		switch (v.getId()) {
		case R.id.bind:
			boolean flag = bindService(intent, conn, Context.BIND_AUTO_CREATE);
			print(flag);
			break;
		case R.id.unbind:
			if (binded) {
				binded = false;
				unbindService(conn);
			}
			break;
		case R.id.start:
			startService(intent);
			break;
		case R.id.stop:
			stopService(intent);
			break;
		case R.id.download:
			push.downLoadFile("http://test.com/icon.png");
			break;
		}
	}

	@Override
	protected void onPause() {
		// TODO Auto-generated method stub
		super.onPause();
		if (isFinishing() &amp;&amp; binded) {
			unbindService(conn);
			binded = false;
		}
	}

	private void print(Object o) {
		if (o == null) {
			System.out.println("null");
		} else {
			System.out.println(o);
		}
	}
}</pre>
&nbsp;

另外，你需要在manifest中配置一下服务，这一句话就够了。
<pre class="brush:xml">&lt;service android:name="PushService"&gt;</pre>
&nbsp;

其实我还有些疑问，我这里的onServiceDisconnected从来没被调用过，onRebind也从来没被调用过，还不明白为什么，有知道的朋友麻烦指教一下。

&nbsp;

<span style="color: #ff0000;">注</span>：可能有人遇到过一个类似的异常：

java.lang.ClassCastException: android.os.BinderProxy

在onServiceConnected中对返回的IBinder进行强制类型转换出出现这个异常。解决办法很简单，去掉manifest中service配置中的process属性。使用此属性会将service放到一个单独的线程中，但会出现强制类型转换异常。