```toml
title = "监听android的拨号事件(android secret code)"
slug = "android_secrect_code"
desc = ""
date = "2011-10-25 19:43:28"
author = "admin"
tags = ["android","android secret code","拨号盘","监听"]
```

这是个比较冷门的东西，简单的说就是当你在拨号盘输入*#*#xxxx#*#*的时候接到通知，然后可以进行相关操作。

首先能想到的应用就是私密类程序。比如你的程序是没有图标的，用户输入这些暗号后可以进行一些操作，或者进入软件界面。

原理很简单，其实也是一个broastcastReceiver而已，只是action并没有放到Intent的常量中，所以很少有人知道。

<!--more-->

还是直接贴代码来的直接。

<span style="color: #0000ff;">写一个广播接收器</span>
<pre>package zzp.test.calllistener;

import android.content.BroadcastReceiver;

import android.content.Context;

import android.content.Intent;

public class Listener extends BroadcastReceiver {

@Override

public void onReceive(Context context, Intent intent) {

Tool.showIntent(intent);

String pwd = intent.getData().getHost();

Intent i = new Intent(context, CalllistenerActivity.class);

i.putExtra("data", pwd);

i.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);

context.startActivity(i);

}

}</pre>
注：用户在拨号盘输入*#*#xxxx#*#*后会发送一个广播

action是android.provider.Telephony.SECRET_CODE

data是 android_secret_code://xxxx

所以我们把data取到后就可以得到用户输入的内容了

然后这里简单的把内容发到activity显示出来(具体怎么用就看你的了)

&nbsp;

<span style="color: #0000ff;">然后部署reciever就行了</span>
<pre>&lt;receiver android:name="Listener"&gt;
	&lt;intent-filter&gt;
		&lt;action android:name="android.provider.Telephony.SECRET_CODE" /&gt;
		&lt;data android:scheme="android_secret_code" /&gt;
	&lt;/intent-filter&gt;
&lt;/receiver&gt;</pre>
完成，这样你就可以在用户僌*#*#xxxx#*#*的时候收到广播了，
中间的XXXX也可以包含*或者#的

下面符上全部代码
<a href="http://veikr.com/wp-content/uploads/2011/10/calllistener.zip">源码下载</a>