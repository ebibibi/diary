---
title: "wordpressの再インストールでプチはまり"
date: 2008-03-19
tags: 
  - "wordpress"
---

嫁のためにwordpressを再インストールしようとしてプチはまりをしました。いつものとおりGoogle先生に聞いてみたら、自分のサイトが上位に出てきてうれしいやら情けないやら(書いたという事実自体覚えてない!)。しかも自分のサイトを見ながら作業をしたら、わかりづらい記述があって2度げんなり・・・。

[![image](images/image_thumb.png)](http://ebi.dyndns.biz/diary/images/wordpress_12F2D/image.png)

- [ebi's diary - Debian etchへのwordpressの導入 , ntpサーバーの設定がうまくできない… , なぜかcourier-imapに接続できないのでパケットを見..](http://ebi.dyndns.biz/diary/20070716.html)

インストール手順以外で別途調べないとできなかったのはデータベースの削除作業。何度もやってる作業なのに覚えられない・・・。

- データベースの削除

- mysql -u ユーザー名 -p
- パスワード入力
- drop database wordpress;

### 日本語化

あとは嫁にはきっと英語の管理画面は気持ちが悪いだろうと思って日本語化。Wordpressって日本語化して使う方法が3パターンもあるんですね。ちょっと混乱しました。

- [WordPress | 日本語 ≫ 日本語版と ME 版について](http://ja.wordpress.org/wordpress-ja-and-me/)
- [Google ドキュメント - WordPress パッケージ比較](http://spreadsheets.google.com/pub?key=pmWPhdiErlxR74Iy0Y4OLBA)

結局debianを使っているので、apt-get upgradeでアップグレードがきちんとできる方法がよいと思い、日本語リソースのみの導入にしておきました。

- [WordPress | 日本語 ≫ 日本語リソースのインストール](http://ja.wordpress.org/install-ja/)

インストールはやっぱり簡単!Wordpressいいなぁ。でも、rubyをできるようになりたい私はやっぱりtdiaryがいいですけどね。
