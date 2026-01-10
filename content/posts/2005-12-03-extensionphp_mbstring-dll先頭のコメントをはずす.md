---
title: "extension=php_mbstring.dll(先頭のコメントをはずす)"
date: 2005-12-03
tags: 
  - "未分類"
---

- \[mbstring\]エントリを以下のように編集
    
    ```
    output_handler = mb_output_handler
    mbstring.internal_encoding = EUC-JP
    mbstring.http_input = auto
    mbstring.http_output = SJIS
    ;mbstring.encoding_translation = Off
    mbstring.detect_order = auto
    mbstring.substitute_character = none;
    ```
    
- cgi.force\_redirectに関して以下のように変更。ただしセキュリティに関連する箇所のようだが内容をよく理解できていないので、追加で調査の必要あり。 ; cgi.force\_redirect = 1 cgi.force\_redirect = 0

- 以下の変更もサイトには書かれていたが該当のエントリは存在しなかった？？
    
    ```
    [mail function]
    SMTP = サーバーのアドレス
    sendmail_from = メール差出人のアドレス
    ```
    

- C:\\Program Files\\Apache Group\\Apache2\\conf\\http.confを以下のように変更する。
- 「LoadModule」が並んでいる部分の末尾に次の一行を書き加える。
    - LoadModule php4\_module C:/php/sapi/php4apache2.dll
- 「DirectoryIndex」という行に「index.php」を追加する。
    - DirectoryIndex index.html index.php
