```toml
title = "读取apk程序包的内容"
slug = "resolve_apk_file_reource"
desc = ""
date = "2012-02-21 13:39:53"
author = "admin"
tags = ["android","apk文件","applicationinfo","packageinfo","packagemanager","图标","读取"]
```

一、对于已安装应用，只需要getPackageManager().getInstalledPacked(int flags)即可得到PackageInfo.
<div>packageInfo.applicationInto中可以得到所有信息。</div>
<div>注：区别系统应用和用户应用：applicationInfo.flags &amp; ApplicationInfo.FLAG_SYSTEM</div>
<div></div>
<div>二、对于未安装应用(apk文件)</div>
<div>使用packageManager.getPackageArchiveInfo(String filePath,int flags)，只能得到部分信息。</div>
<div>所有int形式的资源(label,icon等)都是无法得到的，需要使用反射机制用到隐藏接口</div>
<div></div>
<div>方法如下：</div>
<div></div>
<div>
<pre class="brush:java">Resources res=getResources();
AssetManager asm=new AssetManager();//隐藏api
asm.addAssetPath(String apkfilePath);//隐藏api
res=new Resources(asm,res.getDisplayMetrics(),res.getConfiguration());//隐藏api</pre>
</div>
<div></div>
<div>然后使用res.getString(int resId)   res.getDrawable(int resId)即可得到apk文件内部的资源。(此处资源id可通过上面的公开方法得到)</div>
<div>关键点就在于assetManager.addAssetPath(String apkfilePath)此方法。</div>
<div></div>
<div>现在要做的就是使用反射机制实现上面的隐藏api。</div>
<div>具体反射实现代码如下：</div>
<div></div>
<div>
<div>
<pre class="brush:java">Class asm_cls = Class.forName("android.content.res.AssetManager");
Object asm_obj = asm_cls.getDeclaredConstructor((Class[]) null).newInstance((Class[]) null);
asm_obj.getClass()	.getDeclaredMethod("addAssetPath", new Class[] { String.class })
				.invoke(asm_obj, new Object[] { filePath });
Resources res=getResources();
res = Resources.class.getDeclaredConstructor(
				new Class[] { asm_obj.getClass(),
		                res.getDisplayMetrics().getClass(),
		                res.getConfiguration().getClass() })
    .newInstance(new Object[] { asm_obj, 
                                                    res.getDisplayMetrics(),
						    res.getConfiguration() });
return res;</pre>
</div>
<div></div>
</div>
<div></div>
<div></div>
<div>res.getString(applicaiontInfo.labelRes);</div>
<div>res.getDrawable(applicationInfo.icon);</div>