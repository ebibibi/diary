---
title: "[blogeditor][windowslivewriter] tdiaryで使うブログエディタを選ぶ"
date: 2008-03-16
tags: 
  - "tdiary"
---

![iStock_000003571686XSmall](images/2092694630_b3d8189829.jpg)

[Windows Live Writerでtdiaryに投稿できた](http://ebi.dyndns.biz/diary/20080315.html#p01)ので気を良くして他のブログエディタも見てみて、一番いいやつを選んでやろうという気になりました。今までまったく使っていなかったので何もわからずGoogleで調べてみました。

### xfy Blog Editor

- [xfy.com | 製品情報 : xfy Basic Edtion-xfy Blog Editor](http://www.xfy.com/jp/personal/blog/)

Just Systemのブログエディタ。色々とプラグインなどもあるようだし、かなりよさそうな感じです。多少重いという話もありますが、まずは試してみよう・・・とおもってダウンロードしてみたものの、残念ながらtdiaryでは使えませんでした・・・。残念。tdiaryに対応してくれたら使ったんですけどね・・・。

### ubicast Blogger

- [ubicast Blogger - リッチコンテンツ (動画・静止画・各種ファイル) 対応ブログ クライアント](http://www.ubicast.com/blogger/index.html)

次に試したのはubicast Blogger。とりあえずインストールしてみたけど、実行ファイルが見当たらない。なんじゃこりゃ？とおもったらVistaでは通常使えないもののようです。

- [パソコン日誌: ubicast Bloggerを Windows Vistaで使用する方法](http://shoppc.seesaa.net/article/38759890.html)

仕方がないので手元にあったWindows2000のPCに導入し、インストールディレクトリをVistaにコピー。その上でセットアップしました。が、カテゴリの取得でエラーが出てしまいます。

![image](images/image.png)

WireSharkでパケットを見る限りではきちんとtdiary的には正しい答えを返しているっぽいので(Windows Live WriterではOKだし)、ubicastの問題・・・かな?とにかく残念ながら今の私の環境では使えないようです・・・。

うーん。[xmlrpc.rbの解説のページ](http://docs.tdiary.org/ja/?xmlrpc.rb)にubicastのことが書かれているのに動かないとは・・・。もしかしてWindows Live Writerで動いているのはかなり幸運なことだったりしてしまうのかも・・・。

### BlogWrite

- [BlogWrite - Atom API, XML-RPC に対応した Blog(ブログ)投稿クライアント](http://www.witha.jp/BlogWrite/)

BlogWriteも試してみました。が、残念、やはり使えません。

![image](images/image_3.png)

### そもそも使えるものを探さないと・・・。

そもそも使えるものがなかなか見つかりません。もうちょっとブログエディタが比較されている場所はないものか・・・と探してみました。

- [ブログエディタソフト（PCにインストールするもの限定）をひたすら列挙してください。 ただし、以下の点について明記してください。 ・フリーかシェアか市販か。有料の場合.. - 人力検索はてな](http://q.hatena.ne.jp/1116997368)
- [Windows 環境で使える blogger API クライアント](http://www.na.rim.or.jp/~tsupo/program/blogTool/bloggerApiClient.html)

うーん。あんまりこれ以上試して見たくなるようなものが見つかりません。ということで終了。

### とりあえずWindows Live Writerでいきますか。

自分なりに色々試して見た結果、Windows Live Writerくらいしかまともに動かないので、これで行こうと思います。色々と「あんなものがあったらいいなー」「こんな機能がほしいなー」というものはありますが、まぁ、仕方がない。プラグインの開発もできるみたいだし、自分でもなにか作ってみれるといいなと思います。

一応めぼしい記事へのリンクを張っておきます。

- [Windows Live Writer Beta 日本語版登場、実際に使ってみました - GIGAZINE](http://gigazine.net/index.php?/news/comments/20070531_windows_live_writer_beta_jp/)
- [Windows Live Writer用プラグインいろいろ | caramel\*vanilla](http://caramel-tea.com/2006/09/live_writer_plugin2/)
- [POLAR BEAR BLOG: Windows Live Writer 用プラグイン、不完全レビュー](http://akihitok.typepad.jp/blog/2007/06/windows_live_wr_95da.html)
- [窓の杜 - 【特集】ブログ投稿ソフト「Windows Live Writer」用プラグイン特集](http://www.forest.impress.co.jp/article/2007/11/22/wlwplugins.html)
- [Windows Live Gallery - デベロッパー センター](http://gallery.live.com/devcenter.aspx)
- [Windows Live Writer SDK](http://msdn2.microsoft.com/en-us/library/aa738906.aspx)
