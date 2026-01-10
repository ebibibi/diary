---
title: "mysql_connect関数に注目して自分でPHPを書いてテストしてみる。"
date: 2005-12-03
tags: 
  - "未分類"
---

とりあえずmysql\_connectを単純に使うと以下のように怒られた。

```
mysql_connect(): Client does not support authentication protoco
l requested by server; consider upgrading MySQL client in ...
```

エラーメッセージでググッてみると以下のページが見つかる。 [http://64.233.167.104/search?q=cache:6VcrFxAe6koJ:www.atmarkit.co.jp/bbs/phpBB/viewtopic.php%3Ftopic%3D16165%26forum%3D26%263+%22mysql\_connect():+Client+does+not+support+authentication%22&hl=ja&lr=lang\_ja](http://64.233.167.104/search?q=cache:6VcrFxAe6koJ:www.atmarkit.co.jp/bbs/phpBB/viewtopic.php%3Ftopic%3D16165%26forum%3D26%263+%22mysql_connect\(\):+Client+does+not+support+authentication%22&hl=ja&lr=lang_ja) どうやら、PHPとMySQLのバージョンとであまりうまくない組み合わせの模様。 PHPを5系にすることで対応することにする。
