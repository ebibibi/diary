---
title: "[vista] Windows Vistaの高速化を期待して"
date: 2008-04-01
categories: 
  - "windows"
---

先日の日記([Windows Vistaのデスクトップサーチの対象は必要最小限で！Google Desktopの方がお勧めかも。](http://ebi.dyndns.biz/diary/20080330.html#p01))でWindows Searchを無効化して、Google Desktopを導入したことを書きましたが、「こんなのもあるよ〜」と教えてもらったので実際に試してみました。

- [Windows VistaのHDDガリガリ病を治す ≪ YakiButa Tech Blog.](http://yakitech.wordpress.com/2007/12/27/windows-vista%E3%81%AEhdd%E3%82%AC%E3%83%AA%E3%82%AC%E3%83%AA%E7%97%85%E3%82%92%E6%B2%BB%E3%81%99/)
- [中道左派で行こう: VistaではHDDへのアクセスが激増。ずっと回り続ける。でもメモリ不足でスワップしているわけではありません](http://www.center-left.com/blog/archives/2007/02/vistahdd.html)
- [BLOG/2007/10-18/Vista の HDD アクセスが異常なので改善。 - Release Candidate 2](http://rc-2.net/home/index.php?BLOG%2F2007%2F10-18%2FVista%20%E3%81%AE%20HDD%20%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E3%81%8C%E7%95%B0%E5%B8%B8%E3%81%AA%E3%81%AE%E3%81%A7%E6%94%B9%E5%96%84%E3%80%82)

具体的には以下のように変更したことになります。

- SP1の適用
- Windows Searchの無効化とその代わりにGoogle Desktopの導入
- 自動復元ポイントの無効化

- 今まで一度も復元ポイントの機能を使ったことが無いので。

- デフラグのスケジュール化の無効化

- デフラグは別途AusLogic DiskDefragを使っているので([窓の杜 - Auslogics Disk Defrag](http://www.forest.impress.co.jp/lib/sys/hardcust/defrag/addefrag.html))

- Superfetchの無効化

- メモリ1.5GBの環境では逆に遅くなっているようなので

- ReadyBoostの無効化

- 実際に2GBのUSBメモリを使ってReadyBoostを使っていて効果を実感できた時期もありましたが、USBメモリなくしちゃったので（T-T

もともと高速化のための機能なので、本当に無効化してしまっていいのか?という気もしますが、明らかにHDDの性能がボトルネックになっているような場合にはかなり有効なようです。私が使っているのはThinkPadX60ですが、体感速度はかなり向上しました。

Vista関連の高速化の話だと他にも以下のような記事があるようです。

- [Windows Vistaの高速化＆カスタマイズ](http://www.v-win.net/)
- [Byozine|^^|: 糞重いVistaを超高速化させる10の手段](http://byokan-sunday.haru.gs/2007/08/vista10.html)
- [せうの日記:Vistaを快適に使うには](http://ch00288.kitaguni.tv/e384554.html)

何を行うにしてもその変更を適用する環境によって結果は異なるので、設定変更の意味とメリット、デメリットを理解した上で実際に試して、自分のPCにとって一番有効な設定を模索しないといけないですね。
