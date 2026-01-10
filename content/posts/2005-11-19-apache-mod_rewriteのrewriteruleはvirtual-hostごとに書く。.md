---
title: "[apache] mod_rewriteのRewriteRuleはVirtual Hostごとに書く。"
date: 2005-11-19
tags: 
  - "debian"
---

Virtual Hostを使い出してからいままでずっとRewriteRuleがうまく動いていなかったようだ・・・。

```
＜Virtual Host xxx.xxx.xxx.xxx＞
....
RewriteEngine on
RewriteRule hogehogehoge
＜/Virtual Host＞

```

こんな感じでVirtual Hostタグの中にかく。・・・・まぁ、そりゃそうだよな・・・。
