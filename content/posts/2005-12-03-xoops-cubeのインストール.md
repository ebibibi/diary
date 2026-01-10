---
title: "<a href=\"#navigator\">&uarr;</a>Xoops Cubeのインストール  <a href=\"http://s23spps2/modules/bwiki/index.php?XOOPS#ve3c893a\" title=\"ve3c893a\">&dagger;</a>"
date: 2005-12-03
tags: 
  - "未分類"
---

- Zip形式の最新版をダウンロード
    - [http://prdownloads.sourceforge.jp/xoops/17126/xoops-2.0.13a-JP.zip](http://prdownloads.sourceforge.jp/xoops/17126/xoops-2.0.13a-JP.zip)

- C:\\Program Files\\Apache Group\\Apache2\\htdocsのテストページ群をすべて削除

- Xoopsインストール方法に従って、C:\\Program Files\\Apache Group\\Apache2\\htdocsにダウンロードしたファイルを展開した、htmlフォルダの中身を移動。
    - [http://jp.xoops.org/modules/documents/index.php?id=1](http://jp.xoops.org/modules/documents/index.php?id=1)

- [http://s23spps2/index.php](http://s23spps2/index.php)にアクセスするもInternalServerError...(残念)。以下のエラーが記録されている。
    
    ```
    [Fri Nov 25 15:14:20 2005] [error] [client 172.16.1.76] C:/Program Files/Apache Group/Apache2/htdocs/index.php is not executable; ensure interpreted scripts have "#!" first line
    [Fri Nov 25 15:14:20 2005] [error] [client 172.16.1.76] (9)Bad file descriptor: don't know how to spawn child process: C:/Program Files/Apache Group/Apache2/htdocs/index.php
    ```
    
    index.phpの先頭には<?phpとかかれており、#!c:\\php\\php.exeのようには書かれていない。これを書かないで動作させる方法はないのか？ 参考：[http://dev.rakusui.jp/diary/?date=20050509#p02](http://dev.rakusui.jp/diary/?date=20050509#p02) 以下の設定でOKだった。
- Apacheのコンフィグファイルに以下を追加
    - AddType application/x-httpd-php .php .phtml
    - Action application/x-httpd-php "/php/php.exe"
    - ScriptAlias /php/ "C:/php/"

エラーが解消したところで気を取り直してインストールを続行します。
