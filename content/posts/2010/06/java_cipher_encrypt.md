```toml
title = "java中使用cipher进行信息加密解密的简单教程"
slug = "java_cipher_encrypt"
description = ""
date = "2010-06-24 16:17:45"
author = "admin"
tags = ["cipher","java","加密","教程","解密"]
```

本文概要：使用java自带的cipher类进行简单的信息加密解密操作。<br/>[code=java]<br/>package encryptwithcer;<br/><br/>import java.security.Key;<br/><br/>import javax.crypto.Cipher;<br/>import javax.crypto.KeyGenerator;<br/><br/>public class EncryptExample {<br/>	public


<!--more-->

本文概要：使用java自带的cipher类进行简单的信息加密解密操作。

[java]
package encryptwithcer;
import java.security.Key;
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
public class EncryptExample {
	public static void main(String[] args) throws Exception {
		byte[] message = &quot;这是需要加密的信息&quot;.getBytes();
		System.out.println(&quot;加密前的信息：&quot;+new String(message));
		//得到加密用的KEY&lt;br/&gt;		KeyGenerator keyGen = KeyGenerator.getInstance(&quot;DES&quot;);
		Key key = keyGen.generateKey();
		System.out.println(&quot;得到key成功&quot;);
		//初始化加密器
		Cipher cipher = Cipher.getInstance(&quot;DES&quot;);
		cipher.init(Cipher.ENCRYPT_MODE, key);
		System.out.println(&quot;初始化加密器成功&quot;);
		//加密&lt;br/&gt;		byte[] encrypt_message = cipher.doFinal(message);
		System.out.println(&quot;加密成功&quot;);
		System.out.println(&quot;加密后的信息:&quot;+new String(encrypt_message));
		//解密&lt;br/&gt;		cipher.init(Cipher.DECRYPT_MODE, key);
&gt;		byte[] result = cipher.doFinal(encrypt_message);
		System.out.println(&quot;解密成功&quot;);
		System.out.println(&quot;解密后的信息:&quot;+new String(result));
	}
}
[/java]



<span style="color: red;">注：我搞这个的时候出过一个很奇怪的问题，不管原始信息有多长，加密后总是只有8个字节。弄了半天，后来终于知道了原因。
我写的是cipher.update(message);byte[] result=cipher.doFinal(); 所以会出错。
正确的做法应该是byte[] result=cipher.doFinal(message);
悲剧的是，我到现在还不知道update方法是干嘛的。。。</span>

&nbsp;