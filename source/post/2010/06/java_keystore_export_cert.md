```toml
title = "java中从keystore里导出证书"
slug = "java_keystore_export_cert"
desc = ""
date = "2010-06-25 10:07:01"
author = "admin"
tags = ["certificate","java","keystore","导出","证书","证书库"]
```

本文概要：在java中从证书库(keystore)文件中直接导出证书文件(.cer)<br/><br/>方法：<br/>1.读取keystore文件<br/>2.使用keystore的getCertificate方法从证书库中读取出证书<br/>3.使用一个writer类，将证书的encoded经过base64编码后存入文件<br/><br/>[code=java]<br/>package cert;<br/><br/>import java.io.FileInputStre


<!--more-->

本文概要：在java中从证书库(keystore)文件中直接导出证书文件(.cer)

方法：
1.读取keystore文件
2.使用keystore的getCertificate方法从证书库中读取出证书
3.使用一个writer类，将证书的encoded经过base64编码后存入文件

[java]
package cert;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.OutputStreamWriter;
import java.io.Writer;
import java.security.KeyStore;
import java.security.cert.Certificate;
import java.util.Enumeration;
import sun.misc.BASE64Encoder;
public class StoreCert {
	public static void main(String[] args) throws Exception {
		String ks_pwd=&quot;ujjickeeqg&quot;;
		KeyStore ks=KeyStore.getInstance(&quot;JKS&quot;);
		FileInputStream ks_fis=new FileInputStream(&quot;mykeystore.ks&quot;);
		ks.load(ks_fis,ks_pwd.toCharArray());
		Enumeration&lt;String&gt; aliases=ks.aliases();
		while(aliases.hasMoreElements()){
			String alias=aliases.nextElement();
			Certificate cert=ks.getCertificate(alias);
			byte[] encoded=cert.getEncoded();
			Writer writer=new OutputStreamWriter( new FileOutputStream(alias+&quot;.cer&quot;));
			writer.write( new BASE64Encoder().encode(encoded));
			writer.close();
			System.out.println(&quot;导出&quot;+alias+&quot;证书成功&quot;);
		}
	}
}
[/java]