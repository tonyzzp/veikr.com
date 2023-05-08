```toml
title = "libgdx中异步从网络加载图片"
slug = "libgdx_load_texture_network_async"
description = ""
date = "2012-03-30 23:01:37"
author = "admin"
tags = ["android","libgdx","texture","游戏","网络"]
```

使用libgdx从网络中下载图片，并转换为texture画出来。其实并不复杂，只需要四步就可以了。

1、从网络中读取图片数据到byte[]

2、使用byte[]生成一个pixmap

3、将pixmap画到一张边长是2的N次幂的texture上

4、从texture构造textureRegion

<!--more-->

大概代码如下：

<span style="color: #339966;">一、从url读取byte[]</span>
```InputStream is=new URL(surl).openStream();
ByteArrayOutputStream out = new ByteArrayOutputStream();
int length = 0;
byte[] bytes = new byte[1024];
while ((length = is.read(bytes)) != -1) {
	out.write(bytes, 0, length);
}
is.close();
out.flush();
byte[] rtn = out.toByteArray();```
<span style="color: #339966;">二、使用byte[]生成一个pixmap</span>
```Pixmap pixmap = new Pixmap(bytes, 0, bytes.length);```
<span style="color: #339966;">三、将pixmap画到texture上</span>
```int width = pixmap.getWidth();
int height = pixmap.getHeight();
int preferWidth = MathUtils.nextPowerOfTwo(width);
int preferHeight = MathUtils.nextPowerOfTwo(height);
Texture texture = new Texture(preferWidth,preferHeight,pixmap.getFormat());
texture.draw(pixmap, 0, 0);
pixmap.dispose();```
<span style="color: #339966;">四、构造textureRegion</span>

&nbsp;
```TextureRegion region=new TextureRegioin(texture,0,0,width,heigth);```
大功告成！

&nbsp;

<span style="color: #ff0000;">但是，这里有一些小问题需要注意的。</span>

1、new Texture()这类方法必须放到绘制线程，但读取网络数据流你肯定不能放到绘制线程。

所以可行的办法是新启线程读取数据流，然后使用Gdx.app.postRunnable(new Runnable())来将构造texture的操作post到绘制线程去完成。

&nbsp;

2、另外一个小技巧，你肯定会想写一个工具类来从网络加载texture，但因为是异步的，所以是不能使用返回值的方式传回texture的。

所以必须这样。

&nbsp;
```
TextureRegion region=new TextureRegion(new Texture(1,1,Format.RGBA8888));
loadTextureRegionFromUrl(region,"http://sss.com/asdf.png");

public static void loadTextureRegionFromUrl(final TextureRegion region,
			final String url) {
if (region == null) {
	throw new NullPointerException("region不能为空");
}
new Thread() {
	@Override
	public void run() {
		try {
			final byte[] bytes = ReaderHelper.getBytesFromUrl(url);
			System.out.println(url + " 图片获取成功：" + bytes.length);
			Gdx.app.postRunnable(new Runnable() {
				@Override
				public void run() {
					Pixmap pixmap = new Pixmap(bytes, 0, bytes.length);
					int width = pixmap.getWidth();
					int height = pixmap.getHeight();
					int preferWidth = MathUtils.nextPowerOfTwo(width);
					int preferHeight = MathUtils.nextPowerOfTwo(height);
					Texture texture = new Texture(preferWidth,
							preferHeight, pixmap.getFormat());
					texture.draw(pixmap, 0, 0);
					pixmap.dispose();
					region.setTexture(texture);
					region.setRegion(0, 0, width, height);
					System.out.println(region.getRegionWidth());
					System.out.println(region.getRegionHeight());
					System.out.println(region.getTexture().getHeight());
				}
			});
		} catch (MalformedURLException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	};
}.start();
}```
&nbsp;

最后还有要注意的，<span style="color: #ff9900;">libgdx只支持jpb,png,bmp格式图片，gif什么的就不行了。</span>