---
title: "[plugin] litebox.rbが動かなかった理由と新たな問題(原因は間違いなく私)"
date: 2008-03-20
tags: 
  - "tdiary"
---

### このサイトとliteboxの不幸せな関係

以前litebox.rbを導入しようとしたけれどもうまくいかないという事を書きました。

- [ebi's diary - Lightbox系ライブラリのまとめ - Lightbox系ライブラリのまとめ , Liteboxプラグイン導入](http://ebi.dyndns.biz/diary/20071229.html#p02)

また、最近Windows Live Writerを使い始め、Windows Live Writerで挿入した画像にliteboxを適用するためにHTMLモードにしてタグを編集するという方法を取っています。

- [ebi's diary - tdiaryへのWindows Live Writerでの投稿テスト , tdiaryへのWindows Live Writerでの画像投稿テスト , 課題。 , 叱ってもらえる..](http://ebi.dyndns.biz/diary/20080315.html#p02)

でも、本当はプラグイン作者のはしもとさんにもコメントしてもらっている通り、tdiary用のプラグインとして存在しているlitebox.rbを導入してあげれば何も考慮しなくても画像へのリンクがあればすべてliteboxが適用されて幸せになれるのです。私も幸せになりたい・・・。

### litebox.rbが動作しなかった原因

litebox.rb導入を試した当初は以下のような状況でした。

- そもそもadd\_footer\_proc周りがうまく動いていないような感じ(他のプラグインでも動かないものがある)
- でも、add\_footer\_procを使っているプラグインでうまく動いているものもある
- 昔の日記(=tdiaryモード)で書いてあったエントリではadd\_footer\_procを使っているプラグインがうまく動いていた。最新の日記(=wikiモード)では動いていないけれども。
- litebox.rbプラグインではなく、手動にてliteboxを組み込むとうまく動いた

で、その後設置方法([Scrapcode@tDiary - Liteboxプラグイン , Lightboxプラグイン](http://www.scrapcode.net/tdiary/20080210.html))等を参考にして手順も再確認したのですが手順自体は問題がなさそうでした。

で、結局何が一番大きな原因だったのかというと・・・。

wikiモード関連のファイル(=wiki\_parser.rb, wiki\_style.rb)のバージョンが古いままでした・・・・。(情けない

debianを使っているので基本的にコマンド一発でバージョンアップできるはずなのですが、debian(というかlinuxの流儀)よくまだわかっていないときにtdiaryを導入したので色々と混乱してしまっているのが根本原因でした。これを期に直そうっと・・・。

あべこべなバージョンでもきちんと動作するtdiaryは逆にすごいなぁと思いますが・・・。

で、きちんとwikiモード関連のファイルをアップデートしたのですが、まだ問題が・・・。

### 新たな問題

何が起きたのかというと「Firefoxではうまく動作する」「IEではエラーが出てサイトを開けない」という挙動になってしまいました。

[![image](images/image_thumb.png)](http://ebi.dyndns.biz/diary/images/litebox.rb_F574/image.png) [![image](images/image_thumb_3.png)](http://ebi.dyndns.biz/diary/images/litebox.rb_F574/image_3.png)

はしもとさんのところの動作サンプルはIEでもきちんと表示できるので、**間違いなく**私の問題です。でも、それにしてもこんな挙動ははじめてみます。なんだろう？やっぱりJavascriptが悪さをしているのかな?

まずは、tdiary関連のディレクトリがぐちゃぐちゃになってしまっているのを直してから再トライしようかなと・・・。
