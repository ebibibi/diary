---
title: "胡田昌彦の更新情報を集約して見られるebisuda.comを作りました"
date: 2021-09-16
categories: 
  - "tech"
  - "thinking"
tags: 
  - "rss"
  - "wordpress"
  - "youtube"
---

胡田マニアの方には常識だと思いますが、私はebisuda.netというドメインの下に複数のホスト名で複数のブログを作成しています。例えば以下のものとか。

[https://cloud.ebisuda.net/](https://cloud.ebisuda.net/)

[https://windowsadmin.ebisuda.net/](https://windowsadmin.ebisuda.net/)

この日記ブログ自体も独立しています。

[https://diary.ebisuda.net/](https://diary.ebisuda.net/)

これらは1つのWordpressでマルチサイト構成にしているわけではなく、本当に独立したものになってます。昔勉強もかねてこのような構成にしたのですが、今にして思えば失敗だったなという気もします…（笑

とはいえ、せっかくなので、サイト群の整理をしつつ、トップのhttps://ebisuda.net自体もWordpressで作り直してみました。壮大な無駄な感じがしますが。よければご笑覧ください。

[https://ebisuda.net/](https://ebisuda.net/)

で、せっかくなので、すべてのサイト群のRSSを集約して表示可能にしてみました。ついでにYoutubeチャンネルも。

プラグインとして下記を利用しました。

[https://wordpress.org/plugins/feedzy-rss-feeds/](https://wordpress.org/plugins/feedzy-rss-feeds/)

Youtubeの動画もRSSを吐いてますね。以前調べたときにはRSSは出力してくれなかったはずなのですが知らないうちにシステムの仕様が変わったのかも？とりあえず下記フォーマットでRSS取得できました。

```
https://www.youtube.com/feeds/videos.xml?channel_id=xxxxxxxxxxxxxx
```

で、あれこれやって、一応サイトのお引越しと整理があらかた終わってきました。なんだかすごく懐かしい感じでここの所ブログのメンテナンスをしています。ずいぶん長いことはなれていたので、かなりリハビリが必要ですね。
