```toml
title = "得到所有音乐"
slug = "android_get_all_music"
desc = ""
date = "2011-09-07 11:42:29"
author = "admin"
tags = ["contentprovider","contentresolver","音乐"]
```

在做android音乐播放器吗？还在扫描目录吗？

不需要啦，直接可以通过系统接口得到手机内的所有音乐哦。

而且会帮你解析好id3歌曲信息

<!--more-->contentProvider是个好东西，有什么需要和其他程序共享的，都可以借助这个实现

音乐也不例外

手机开机时会有提示正在扫描媒体，然后扫描完成后还会发送一个media_scanner_finished广播来通知你

然后就可以直接查询到所有音乐信息了，使用contentResolver实现

很简单很简单，但我之前网上找了好久都没找到，这次无意中发现一段代码，拿出来共享一下

直接贴代码了。
<pre class="brush:java">		class Music {
			String title, art, album;
			long length;

			public String toString() {
				return "{title:" + title + ",art:" + art + ",album:" + album
						+ ",length:" + length + "}";
			}
		}

		List&lt;Music&gt; list = new ArrayList&lt;Music&gt;();

		Context ctx = getContext();
		ContentResolver cr = ctx.getContentResolver();
		Cursor c = cr.query(MediaStore.Audio.Media.EXTERNAL_CONTENT_URI, null,
				null, null, MediaStore.Audio.Media.DEFAULT_SORT_ORDER);
		while (c.moveToNext()) {
			Music music = new Music();
			music.title = c.getString(c
					.getColumnIndex(MediaStore.Audio.AudioColumns.TITLE));
			music.art = c.getString(c
					.getColumnIndex(MediaStore.Audio.AudioColumns.ARTIST));
			music.album = c.getString(c
					.getColumnIndex(MediaStore.Audio.AudioColumns.ALBUM));
			music.length = c.getLong(c
					.getColumnIndex(MediaStore.MediaColumns.SIZE));
			list.add(music);
		}
		for (Music m : list) {
			System.out.println(m);
		}</pre>
好了，全部完工。