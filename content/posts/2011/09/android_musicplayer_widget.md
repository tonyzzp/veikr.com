```toml
title = "Android音乐播放widget的简单事例(附源代码)"
slug = "android_musicplayer_widget"
desc = ""
date = "2011-09-03 17:57:17"
author = "admin"
tags = ["android","appwidget","mediaplayer","service","源代码","音乐播放"]
```

本文将做一个音乐播放的appWidget。通过本文您将学会：

1.制作简单的appWidget

2.service、broadcast

3.service与appWidget的交互

4.通过第三方库来读取mp3文件的id3标签(歌曲名、歌手名、专辑名等)

<a href="http://veikr.com/wp-content/uploads/2011/09/musicWidget.png"><img class="aligncenter size-full wp-image-238" title="音乐播放器的AppWidget" src="http://veikr.com/wp-content/uploads/2011/09/device.png" alt="音乐播放器的AppWidget效果图" width="480" height="230" /></a>

<!--more-->开始工作吧。

一、widget的layout文件

普通的layout文件，同样存入在layout文件夹下
<pre class="brush:xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="fill_parent" android:layout_height="fill_parent"
	android:orientation="vertical"&gt;
	&lt;TextView android:text="TextView" android:id="@+id/textView1"
		android:textSize="25px" android:layout_height="wrap_content"
		android:layout_width="match_parent" android:gravity="center"&gt;&lt;/TextView&gt;
	&lt;LinearLayout android:id="@+id/linearLayout1"
		android:layout_height="wrap_content" android:layout_width="match_parent"
		android:layout_below="@id/textView1" android:gravity="center"&gt;
		&lt;ImageView android:src="@drawable/previous"
			android:layout_height="wrap_content" android:layout_width="wrap_content"
			android:layout_weight="1.0" android:id="@+id/previous" /&gt;
		&lt;ImageView android:src="@drawable/play"
			android:layout_height="wrap_content" android:layout_width="wrap_content"
			android:layout_weight="1.0" android:id="@+id/play" /&gt;
		&lt;ImageView android:src="@drawable/next"
			android:layout_height="wrap_content" android:layout_width="wrap_content"
			android:layout_weight="1.0" android:id="@+id/next" /&gt;
	&lt;/LinearLayout&gt;
&lt;/RelativeLayout&gt;</pre>
二、widget的配置文件

右键-new-androi xml file，选择appWidget provider，输入文件名，即可。

此文件会存在于xml文件夹下
<pre class="brush:xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;appwidget-provider xmlns:android="http://schemas.android.com/apk/res/android"
	android:minWidth="320px" android:updatePeriodMillis="3600000"
	android:initialLayout="@layout/widget" android:minHeight="150px"&gt;
&lt;/appwidget-provider&gt;</pre>
属性很简单， 就不用解释了

&nbsp;
三、写appWidgetProvider类，这个类实现widget的更新与事件监听
class MusicProvider extends AppWidgetProvider.
appwidgetprovider其实是broadcastreceiver的。
此类下的主要方法onReceive,onUpdate,onEnable,onDisable,onDeleted。
onEnable方法在第一个widget被添加到桌面时调用，我们在这里启动音乐播放服务(后面再写)
onDisable方法在全部widget删除后调用，我们在这里关闭服务
onUpdate方法里我们对widget的各控件设置监听
onReceiver方法其实就是broadCastReceiver里的onReceiver，在收到广播时我们更新widget(比如显示歌名)
<pre class="brush:java">package zzp.musicwidget;

import android.app.PendingIntent;
import android.appwidget.AppWidgetManager;
import android.appwidget.AppWidgetProvider;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.widget.RemoteViews;
import zzp.musicwidget.R;

public class MusicWidgetProvider extends AppWidgetProvider {

@Override
public void onReceive(Context context, Intent intent) {
super.onReceive(context, intent);
System.out.println("provider receive:" + intent);
String action = intent.getAction();
RemoteViews views = new RemoteViews(context.getPackageName(),
R.layout.widget);
if (action.equals("zzp.musicwidget.widget.play")) {
views.setImageViewResource(R.id.play, R.drawable.pause);
} else if (action.equals("zzp.musicwidget.widget.pause")) {
views.setImageViewResource(R.id.play, R.drawable.play);
} else if (action.equals("zzp.musicwidget.widget.title")) {
views.setTextViewText(R.id.textView1,
intent.getStringExtra(Intent.EXTRA_TEXT));
}

// 改变完成后，请一定要记住调用updateAppWidget方法，否则改变不会生效
AppWidgetManager mgr = AppWidgetManager.getInstance(context);
mgr.updateAppWidget(new ComponentName(context,
MusicWidgetProvider.class), views);
}

@Override
public void onUpdate(Context context, AppWidgetManager appWidgetManager,
int[] appWidgetIds) {
super.onUpdate(context, appWidgetManager, appWidgetIds);

// 在这里给widget里的控件添加监听事件
RemoteViews views = new RemoteViews(context.getPackageName(),
R.layout.widget);
Intent inext = new Intent("zzp.musicwidget.next");
PendingIntent pnext = PendingIntent.getBroadcast(context, 0, inext, 0);
Intent iprevious = new Intent("zzp.musicwidget.previous");
PendingIntent pprevious = PendingIntent.getBroadcast(context, 0,
iprevious, 0);
Intent iplay = new Intent("zzp.musicwidget.playorpause");
PendingIntent pplay = PendingIntent.getBroadcast(context, 0, iplay, 0);
views.setOnClickPendingIntent(R.id.next, pnext);
views.setOnClickPendingIntent(R.id.play, pplay);
views.setOnClickPendingIntent(R.id.previous, pprevious);
// 不要忘记updateAppWidget
AppWidgetManager mgr = AppWidgetManager.getInstance(context);
mgr.updateAppWidget(new ComponentName(context,
MusicWidgetProvider.class), views);
}

@Override
public void onEnabled(Context context) {
super.onEnabled(context);
Intent intent = new Intent(context, MusicService.class);
context.startService(intent);
}

@Override
public void onDisabled(Context context) {
// 当widget删除时，停止musicService
super.onDisabled(context);
Intent intent = new Intent(context, MusicService.class);
context.stopService(intent);
}
}</pre>
在onUpdate中对控件设置了监听，当点击按钮(播放、下一曲、上一曲)后发送广播。而我们的service中会接收这些广播，然后执行相应的操作。
service中的的某些操作(播放、暂停、换歌)执行后，也会发送广播，这时appWidgetProvider收到广播后调widget界面(显示歌名、变换图标)

&nbsp;
四、音乐播放的service
这个类中接收widgetProvider发送的广播，然后进行相关操作(播放、暂停、下一曲、上一曲)
<pre class="brush:java">package zzp.musicwidget;

import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

import org.farng.mp3.MP3File;
import org.farng.mp3.TagException;
import org.farng.mp3.id3.AbstractID3v2;
import org.farng.mp3.id3.ID3v1;
import zzp.musicwidget.R;

import android.app.Service;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.media.MediaPlayer;
import android.os.IBinder;

public class MusicService extends Service {
private MediaPlayer player;
private List&lt;String&gt; data;
private int location = 0;
private BroadcastReceiver receiver;

@Override
public void onCreate() {
// TODO Auto-generated method stub
super.onCreate();
System.out.println("music service create");
}

@Override
public void onStart(Intent intent, int startId) {
super.onStart(intent, startId);
System.out.println("music service onbind");
player = new MediaPlayer();
data = new ArrayList&lt;String&gt;();
System.out.println("开始加载音乐");
File file = new File("/mnt/sdcard/veikrmusic");
File[] files = file.listFiles();
for (File f : files) {
if (f.isFile() &amp;&amp; f.getName().endsWith(".mp3")) {
data.add(f.getAbsolutePath());
}
}
System.out.println("音乐加载ok:" + data.size());

try {
player.setDataSource(data.get(location));
player.prepare();
} catch (IllegalArgumentException e1) {
// TODO Auto-generated catch block
e1.printStackTrace();
} catch (IllegalStateException e1) {
// TODO Auto-generated catch block
e1.printStackTrace();
} catch (IOException e1) {
// TODO Auto-generated catch block
e1.printStackTrace();
}
receiver = new BroadcastReceiver() {
@Override
public void onReceive(Context context, Intent intent) {
System.out.println("service receive:" + intent);
String action = intent.getAction();
if (action.equals("zzp.musicwidget.playorpause")) {
if (!player.isPlaying()) {
try {
player.start();
sendPlay();
} catch (IllegalStateException e) {
// TODO Auto-generated catch block
e.printStackTrace();
}
} else {
player.pause();
sendPause();
}
} else if (action.equals("zzp.musicwidget.next")) {
playNext();
} else if (action.equals("zzp.musicwidget.previous")) {
playPrevious();
}
}
};

IntentFilter filter = new IntentFilter();
filter.addAction("zzp.musicwidget.next");
filter.addAction("zzp.musicwidget.playorpause");
filter.addAction("zzp.musicwidget.previous");
registerReceiver(receiver, filter);
}

public void playNext() {
if (location &lt; data.size() - 1) {
location++;
} else if (location == data.size() - 1) {
location = 0;
}
play();
}

public void playPrevious() {
if (location == 0) {
location = data.size() - 1;
} else if (location &gt; 0) {
location--;
}
play();
}

public void play() {
System.out.println("播放第" + location + "首");
try {
// player.release();
// player = null;
// player = new MediaPlayer();
player.reset();
player.setDataSource(data.get(location));
player.prepare();
player.start();
sendPlay();
} catch (IllegalArgumentException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (IllegalStateException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (IOException e) {
// TODO Auto-generated catch block
e.printStackTrace();
}
}

@Override
public void onDestroy() {
unregisterReceiver(receiver);
super.onDestroy();
}

@Override
public IBinder onBind(Intent intent) {
return null;
}

/**
* 发送播放通知，以便widget改变图标样式
*/
public void sendPlay() {
Intent play = new Intent("zzp.musicwidget.widget.play");
sendBroadcast(play);
try {
sendTitle();
} catch (Exception e) {

}
}

public void sendPause() {
Intent play = new Intent("zzp.musicwidget.widget.pause");
sendBroadcast(play);
}

/**
* 发送歌曲标题到widget
*/
public void sendTitle() {
String filepath = data.get(location);
System.out.println(filepath);
MP3File mp3 = null;
try {
mp3 = new MP3File(filepath);
} catch (IOException e) {
// TODO Auto-generated catch block
e.printStackTrace();
} catch (TagException e) {
// TODO Auto-generated catch block
e.printStackTrace();
}
AbstractID3v2 id3v2 = mp3.getID3v2Tag();
ID3v1 id3v1 = null;
if (id3v2 == null) {
id3v1 = mp3.getID3v1Tag();
}
String title = "";
if (id3v2 != null) {
title = id3v2.getLeadArtist() + " - " + id3v2.getSongTitle();
} else if (id3v1 != null) {
title = id3v1.getLeadArtist() + " - " + id3v1.getSongTitle();
}
Intent i = new Intent("zzp.musicwidget.widget.title");
i.putExtra(Intent.EXTRA_TEXT, title);
sendBroadcast(i);
}
}</pre>
onStart中初始化音乐(音乐文件放在/sdcard/veikrmusic目录下，必须为mp3)，注册广播接收器，以便接收widget发送的命令
接收到widget发送的广播后进行相关操作，操作完成后再发送广播通知widget更新界面
这里面用到了一个第三方库来解析mp3文件的id3标签，文章末尾附下载

&nbsp;

五、代码都写好了，剩下的就是配置了
<pre class="brush:xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="zzp.musicwidget" android:versionCode="1" android:versionName="1.0"&gt;
&lt;uses-sdk android:minSdkVersion="7" /&gt;
&lt;uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"&gt;&lt;/uses-permission&gt;
&lt;application android:icon="@drawable/icon" android:label="@string/app_name"&gt;
&lt;receiver android:name="MusicWidgetProvider"&gt;
&lt;intent-filter&gt;
&lt;action android:name="android.appwidget.action.APPWIDGET_UPDATE"&gt;&lt;/action&gt;
&lt;action android:name="zzp.musicwidget.widget.play"&gt;&lt;/action&gt;
&lt;action android:name="zzp.musicwidget.widget.pause"&gt;&lt;/action&gt;
&lt;action android:name="zzp.musicwidget.widget.title"&gt;&lt;/action&gt;
&lt;/intent-filter&gt;
&lt;meta-data android:resource="@xml/widget" android:name="android.appwidget.provider"&gt;&lt;/meta-data&gt;
&lt;/receiver&gt;
&lt;service android:name="MusicService"&gt;&lt;/service&gt;
&lt;/application&gt;
&lt;/manifest&gt;</pre>
OK！大功告成
算不上什么教程，都是在粘源代码，大家都指教，高手莫笑。

ps:好几个月没写博客了
前几天刚刚换了个空间，原来那个太太太垃圾了。速度慢的要命，三天两头上不去，客服垃圾，挤一句说一句。。
经常改IP，也不通知你，等网站上不去了再问客服，他们才说换IP了。。。
另外，本来有phpAdmin的，后来突然就没了。。。冰山互联。。。大家一定一定不要用！！！！

下载：

<a href="http://veikr.com/wp-content/uploads/2011/09/MusicWidget.apk_.zip">MusicWidget.apk 安装包</a>

<a href="http://veikr.com/wp-content/uploads/2011/09/MusicWidget.zip">MusicWidget.zip 源码</a>