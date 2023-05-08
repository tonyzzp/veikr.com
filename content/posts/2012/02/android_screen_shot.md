```toml
title = "ANDROID应用内截图的代码实现"
slug = "android_screen_shot"
desc = ""
date = "2012-02-19 16:31:18"
author = "admin"
tags = ["android","screen shot","截图"]
```

方法一：

View view= getWindow().getDecorView();

Bitmap bmp = Bitmap.createBitmap(480, 800, Bitmap.Config.ARGB_8888);

view.draw(new Canvas(b));

bmp就是截取的图片了，可通过bmp.compress(CompressFormat.PNG, 100, new FileOutputStream(file));把图片保存为文件。

&nbsp;

方法二：

getWindow().getDecorView().setDrawingCacheEnabled(true);

bmp=getWindow().getDecorView().getDrawingCache();

&nbsp;

但这样得到的图片是包含状态栏和标题栏的，如果想把状态栏和标题栏去掉，可把得到的图片顶部一部分剪裁掉。

1、得到状态栏高度

Rect rect = new Rect();

view.getWindowVisibleDisplayFrame(rect);

int statusBarHeight = rect.top;

System.out.println("状态栏高度：" + statusBarHeight);

&nbsp;

2、得到标题栏高度

int wintop = getWindow().findViewById(android.R.id.content).getTop();

int titleBarHeight = wintop - statusBarHeight;

System.out.println("标题栏高度:" + titleBarHeight);

&nbsp;

&nbsp;

注：这样得到的截图是不会包含dialog和popupwindow的，你必须单独得到popupwindow的截图，然后再和背景截图合到一起。

另外，截图的相关代码是不能放到oncreate中的，因为这时候getDectorView()得到的是null

&nbsp;

&nbsp;

把两个bitmap合到一起的方法很简单。

Bitmap bmpall=Biatmap.createBitmap(width,height,Config.ARGB_8888);

Canvas canvas=new Canvas(bmpall);

canvas.drawBitmap(bmp1,x,y,paint);

canvas.drawBitmap(bmp2,x,y,paint);

得到的bmpall就是合在一起的图片了。

&nbsp;

ps:按理说也getWindow.findViewById(android.R.id.content)得到的view就是不包含状态栏和标题栏的view，但这个我还没有试过。