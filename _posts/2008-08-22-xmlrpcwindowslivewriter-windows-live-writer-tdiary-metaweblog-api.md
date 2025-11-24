---
title: "[xmlrpc][windowslivewriter] Windows Live Writer + tdiary + Metaweblog API"
date: 2008-08-22
tags: 
  - "tdiary"
---

最近はtdiaryへの投稿にWindows Live Writerを使っているのですが、Windows Live Writerのバージョンが変わった(ベータ版から正式版になった)せいなのか、以下のことができなくなっちゃいました。

- カテゴリの取得、指定
- 既存の記事の取得

以前はどちらもできていた記憶があるのですが…。

[Windows Live Writerのページ](http://get.live.com/writer/overview?wa=wsignin1.0)には以下の記述が

> - ###### **さまざまなブログに対応**
>     
>     Writer を使うと、Windows Live スペース、SharePoint、Community Server 上のブログに記事を投稿できます。また、 Metaweblog API と RSD をともにサポートしている他のブログサービスの記事の編集、投稿にも利用できます。
>     
>     ※ご利用中のブログサービスの Metaweblog API および RSD の対応状況については、当該のブログサービスにご確認ください。
>     

tdiaryのxmlrpc.rbはMetaweblog APIおよびRSDに対応しているようです。

- [tDiaryドキュメント - xmlrpc.rb](http://docs.tdiary.org/ja/?xmlrpc.rb)

でも、実際にカテゴリの取得を行っている際のパケットを見てみると以下のようなやり取りが。

> POST [http://ebi.dyndns.biz/diary/xmlrpc.rb](http://ebi.dyndns.biz/diary/xmlrpc.rb) HTTP/1.0
> 
> Accept: \*/\*
> 
> Accept-Language: ja-JP, en-US, en, \*
> 
> User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.2; Windows Live Writer 1.0)
> 
> Content-Type: text/xml
> 
> Host: ebi.dyndns.biz
> 
> Content-Length: 377
> 
> <?xml version="1.0" encoding="euc-jp"?>
> 
> <methodCall>
> 
> <methodName>metaWeblog.getCategories</methodName>
> 
> <params>
> 
>   <param>
> 
>    <value>
> 
>     <string>ebi's diary</string>
> 
>    </value>
> 
>   </param>
> 
>   <param>
> 
>    <value>
> 
>     <string>ユーザー名</string>
> 
>    </value>
> 
>   </param>
> 
>   <param>
> 
>    <value>
> 
>     <string>パスワード</string>
> 
>    </value>
> 
>   </param>
> 
> </params>
> 
> </methodCall>
> 
> HTTP/1.1 200 OK
> 
> Via: ProxyServer 
> 
> Content-length: 310
> 
> Date: Fri, 22 Aug 2008 04:10:03 GMT
> 
> Content-Type: text/xml; charset=utf-8
> 
> Server: Apache/2.2.9 (Debian) PHP/5.2.6-2+b1 with Suhosin-Patch mod\_python/3.3.1 Python/2.4.4 mod\_ssl/2.2.9 OpenSSL/0.9.8g mod\_perl/2.0.3 Perl/v5.8.8
> 
> Keep-Alive: timeout=15, max=100
> 
> <?xml version="1.0" ?><methodResponse><fault><value><struct><member><name>faultCode</name><value><i4>1</i4></value></member><member><name>faultString</name><value><string>Method metaWeblog.getCategories missing or wrong number of parameters!</string></value></member></struct></value></fault></methodResponse>

"Method metaWeblog.getCategories missing or wrong number of parameters!"ということなので明らかにWindows Live Writer側とtdiary(xmlrpc.rb)側でミスマッチな感じです。両者が対応しているMetaweblog APIのバージョンが異なるのでしょうか?でも、リクエストにバージョンなんてないですけどね。

Windows Live Writer側のMetaweblog APIの認識は以下のドキュメントのものの模様。

- [MetaWeblog API リファレンス](http://msdn.microsoft.com/ja-jp/library/bb259697.aspx)

あとは、実際にxmlrpc.rbの内容を見てみて…ですかね。時間がとれたら自分で実装してみたいなぁと思います。
