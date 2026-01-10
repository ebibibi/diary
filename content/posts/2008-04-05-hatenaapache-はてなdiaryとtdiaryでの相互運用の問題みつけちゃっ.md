---
title: "[hatena][apache] はてなDiaryとtDiaryでの相互運用の問題みつけちゃった・・"
date: 2008-04-05
tags: 
  - "tdiary"
---

増田にトラックバックを飛ばしたら、増田側にはリンクが作成されましたが、そのリンクから正常にこちらのサイト(tdiary)にアクセスすることができませんでした。

[![image](images/image_thumb_3.png)](http://ebi.dyndns.biz/diary/images/DiarytDiary_B678/image_3.png)

どうやら、tdiaryのセクションに対して使われている「#」が益田側で生成されたリンク上で最終的に「%23」として扱われているのが原因のようです。この問題、どこかで以前読んだなーと思ったら、これでした。

- [高木浩光＠自宅の日記 - はてなブックマークを禁止する技術的方法, 追記, 追記2 （23日）](http://takagi-hiromitsu.jp/diary/20071222.html)

色々と難しい問題があるようですね。

でも、なんとか今の構成のままこちら側の対応で何とかしようと以下のようにRewriteRuleに書いてみました。

> RewriteRule ^/diary/(.\*)%23(.\*)$ /diary/$1#$2

・・・でもだめでした（T-T

誰か回避方法を知っている人がいたら教えてください・・・。
