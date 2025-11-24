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
    

- \[mail function\]エントリを編集 \[mail function\] ; For Win32 only. SMTP = s2kexg1 smtp\_port = 25 ; For Win32 only. sendmail\_from = [s23spps2@jbs.co.jp](mailto:s23spps2@jbs.co.jp)

- extension=php\_mysqli.dllを追加
- C:\\Program Files\\Apache Group\\Apache2\\conf\\http.confを以下のように変更する。
    - LoadModule php4\_module C:/php/sapi/php4apache2.dllをLoad Module php5\_module C:\\php\\php5apache2.dllに変更
- php4の際にsystem32にコピーしたDLLを削除

記述を間違えると、Apache2がサービス開始中でハングアップしてしまうので、何度か再起動しながら設定・・・。(弱)
