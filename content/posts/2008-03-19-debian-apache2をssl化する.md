---
title: "[debian] apache2をssl化する"
date: 2008-03-19
tags: 
  - "apache"
---

前からやらなくちゃと思っていたけれどもやっていなかったサイトのSSL化。自分はいろいろとわかった上でやってるからいいけど、嫁にはSSLで管理させようと思い導入。

ぐぐったらここがわかりやすそうだったので参考に。

- [Apache/SSL(http)対応にする（Debian Etch編） - 俺の基地](http://yakinikunotare.boo.jp/orebase/index.php?Apache%2FSSL\(http\)%C2%D0%B1%FE%A4%CB%A4%B9%A4%EB%A1%CADebian%20Etch%CA%D4%A1%CB)

### はまったところ and 疑問点(まだ未解決)

- 生成された証明書がdemoCA/cacert.crtではなくてdemoCA/cacert.pemなんだけどこれでいいのか?
- apacheを起動すると"Address already in use: make\_sock: could not bind to address \[::\]:443"というエラーが。443はだれもつかんでないはずだし・・・おかしい。

- 一度443ではなくて4443番ポートに変えてみたら確かに443が使われていた
- 一度sites-enableから今回追加した設定を抜いてみたら、それでもまだ443が使われていた。どうやら以前設定したごみがある模様・・・。
- 検索したところ/etc/apache2/ports.confに記述があった。これは何者だ?
- [AquBlog: DebianでApache2 − ポート設定](http://www.aqunet.info/blog/archives/000045.html)
- うーん。Listen 80と書いてあっても80番はバッティングしていないし書かれているのが正しいのだろうと思う。でも、たしかにバッティングしちゃうし、ports.confからListen443を消せば443での待ちうけは無くなる・・・。どういうことだ?
- Listenの書き方とipv4, v6のあたりで色々と問題がある模様。とりあえずポートの待ちうけはできるようになったけど、結局動かない。
- 問題の切り分けの必要あり・・・。（T-T

- なんだか色々おかしいので、もう一度Webを検索。今度は以下を参考に
- [試験管のなかのコード :: Debian Etch で Apache2.2 + SSL](http://www.in-vitro.jp/blog/index.cgi/Linux/20070419_01.html)

- crt等は作れたと思うのだけれども、やはり443が使われているというエラーがでる。
- とりあえずports.conf側でListen443をコメントアウトして先に進める

- ローカルでの確認作業時に以下のエラーが出てしまう。

> /etc/apache2# openssl s\_client -connect localhost:https  
> CONNECTED(00000003)  
> 8585:error:140770FC:SSL routines:SSL23\_GET\_SERVER\_HELLO:unknown protocol:s23\_clnt.c:583:

- どうやら443番ポートでHTTPが動いてしまっていた模様。
- Virtual Hostタグの部分をIpアドレス:443に変更したらうまくいった。
- 一応動いたけど、firefoxでは接続できない。これは仕様かな。IEなら警告は出るけど接続できるし  
    [![image](images/image_thumb.png)](http://ebi.dyndns.biz/diary/images/apache2ssl_13E50/image.png)
- [IE6はHTTPS時に証明書の種類のチェックしない？ (やまかわのログ)](http://antas.jp/blog/yamakawa/2007/12/ie6https.html)　これかな？とも思うけど、きちんとopenssl.cnfのnsCertTypeはserverになってます・・・。
- [日記/2006 - りょうのぺえじ](http://www.fastriver.net/~ryo/pukiwiki.php?%C6%FC%B5%AD%2F2006)　ここに書かれているように

```
nsCertType                    = server,client
```

  
という設定も試してみましたが、残念。結果変わらず。

 まぁ、とりあえずパスワード自体の暗号化はできるようになったので、まぁ、今日のところはこれで良しとします。もう深夜3時15分だし・・・。
