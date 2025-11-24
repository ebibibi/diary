---
title: "flush privileges;"
date: 2005-12-03
tags: 
  - "未分類"
---

これでもまだDBに接続できないとのエラーが出てセットアップできない。 原因不明。

Apacheのログを見ると以下のエラーが表示されている。

```
 File 'c:\mysql\share\charsets\?.conf' not found (Errcode: 2)
 Character set '#33' is not a compiled character set and is not specified in the 'c:\mysql\share\charsets\Index' file
```

特に現在のエラーとは関係ないようだけれども気持ちがわるいので 以下のサイトを参考にしてC:\\mysqlにファイルを配置する。 [http://64.233.167.104/search?q=cache:jIJ9uteyhCMJ:xoops.smej.com/modules/newbb/viewtopic.php%3Fpost\_id%3D103%26topic\_id%3D26%26forum%3D1+%22mysql%5Cshare%5Ccharsets%5C%3F.conf%27%22&hl=ja&lr=lang\_ja](http://64.233.167.104/search?q=cache:jIJ9uteyhCMJ:xoops.smej.com/modules/newbb/viewtopic.php%3Fpost_id%3D103%26topic_id%3D26%26forum%3D1+%22mysql%5Cshare%5Ccharsets%5C%3F.conf%27%22&hl=ja&lr=lang_ja) 配置後もエラーは消えない・・・。なぜ? Webを検索しても拉致があかないので、ソースを追いかけてみるとmysqldatabase.phpにて以下のようにコネクトしていた。

```
$this->conn = @mysql_connect(XOOPS_DB_HOST, XOOPS_DB_USER, XOOPS_DB_PASS);
```
