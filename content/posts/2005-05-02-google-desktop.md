---
title: "Google Desktop"
date: 2005-05-02
tags: 
  - "pc"
---

PC内の情報の検索。Windows標準の検索やOutlook標準の検索(こっちは仕事でよく使う)がかなりいけてないので、[Google Desktop](http://desktop.google.com/)を試験的に導入してみています。「劇的に使い勝手が向上！」みたいなことになるといいなぁ。 ちょっと使ってみた感じでは、まさにgoogleのインターフェースとまったく同じもので、PC内の検索が行えててかなりいい感じです。電子メールのアイテムに関しても、検索結果から直接返信まで行えるなど、なかなか芸が細かい。 技術的には常駐プロセスが簡易Webサーバーになっているようで、netstat -anbしてみるとこんな感じ。

> TCP 127.0.0.1:4664 0.0.0.0:0 LISTENING GoogleDesktopIndex.exe\]

バグがあったら痛そうなプロセスですなぁ。。。頼みますよGoogleさん。
