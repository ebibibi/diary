---
title: "tDiaryからWordpressへのデータ移行で参考にしたサイト"
date: 2017-01-02
categories: 
  - "tech"
---

tDiaryからWordpressにデータ移行する際には以下のサイトを参考にさせてもらいました。

- [さようならtDiary、こんにちはWordpress – kackyの投資生活](http://www.kacky-investment.net/2015/07/11/%E3%81%95%E3%82%88%E3%81%86%E3%81%AA%E3%82%89tdiary%E3%80%81%E3%81%93%E3%82%93%E3%81%AB%E3%81%A1%E3%81%AFwordpress/)

移行スクリプトも公開してくださっており、さらにtDiaryスタイルとWikiスタイルに両対応ということで大変助かりました。基本的にこここで公開されているスクリプトを使ってそのままデータを変換し、それをWordpress側からインポートすることでデータの移行ができました。

あとは、tdiaryとwordpressとでURLの構造が異なっている部分をmod\_rewriteで吸収したのですが、私のサイト群はwordpress自体が複数ブログ対応する前にあちこちを参考にしながら自分で魔改造した関係で.htaccessが凄いことになっているのでそのあたりの記述に苦労してしまいました。

mod\_rewriteあたりで参考にさせてもらったサイトは以下のあたりです。

- [mod\_rewriteの設定 - Qiita](http://qiita.com/rakuraku0615/items/997766468c38d7d9b093)
- [Apache module mod\_rewrite](http://net-newbie.com/trans/mod_rewrite.html)

mod\_rewriteでこねくり回しすぎるのは良くないんでしょうけど、どうしてもmod\_rewriteに逃げてしまいますね…。
