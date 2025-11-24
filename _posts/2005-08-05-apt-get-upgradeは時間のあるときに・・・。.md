---
title: "apt-get upgradeは時間のあるときに・・・。"
date: 2005-08-05
tags: 
  - "hiki"
---

何気なくapt-get upgradeしたら、hikiが動かなくなりました。結局、hikiのバージョンアップにあわせてhikiconfig.rbの中の変数を$hogeから@hogeに書き換えて、cacheファイルの参照がおかしくなってしまっていたので、直接config.rbを書き換えてむりくり対応して、rubyのバージョンアップにあわせてWorldWritableなディレクトリのパーミッションを変更したら動くようになりました。やられた。。 次のバージョンアップでも必ず手対応がひつようだのぅ・・・。
