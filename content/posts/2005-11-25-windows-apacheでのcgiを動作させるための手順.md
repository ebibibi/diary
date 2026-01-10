---
title: "[windows] ApacheでのCGIを動作させるための手順"
date: 2005-11-25
tags: 
  - "apache"
---

会社の検証機でWindowsにXoopsをインストールしようとしていてPHPがCGIとして動作せず、今までこのあたりをきちんと理解していなかったことを痛感。自分なりにまとめてみました。間違いが多く含まれている可能性がありますので、ご注意ください。

#### AddHandler + Option ExecCGIで実行させる方法

この方法が結構使われているようです。これは、まず、AddHandlerにてCGIとして扱う拡張子を指定し、CGIを実行する権限自体はOptionディレクティブにて許可する方法です。

また、このパターンにAliasScrptディレクティブも組み合わせて、CGIは/cgi-bin/ディレクトリ内においておき、そこで実行させるような方法も一般的なようです。

このパターンではshebang lineというものが重要な役割をはたします。これはスクリプトの一行目に記述されている「#!/usr/local/bin/perl」とかそういった感じのものです。これがきちんと設定されていないと、以下のようなエラーが記録されます。(今回これで苦しんだわけです。)

```
[Fri Nov 25 15:14:20 2005] [error] [client 172.16.1.76] C:/Program Files/Apache Group/Apache2/htdocs/index.php is not executable; ensure interpreted scripts have "#!" first line
[Fri Nov 25 15:14:20 2005] [error] [client 172.16.1.76] (9)Bad file descriptor: don't know how to spawn child process: C:/Program Files/Apache Group/Apache2/htdocs/index.php

```

Addhandlerでは「CGIだよ」と指定しているだけなので、具体的にPerlなのかRubyなのか・・・といったところまではわかりません。ですので、1行目にshebang lineというものが必要だ・・・というわけです。

ただし、Windows環境となるとちょっと事情が変わってきます。Apache2系ではもう設定できず、必ずshebang lineが有効になるようですが、Apache1系ではshebang lineを有効にするか、無効にするかの選択が出来るそうです。ではshebang lineを無効にした際にはどのようにして実行すべき環境を判別するのか?・・・そこで、Windowsのファイルの関連付けを使い、関連付けにしたがって動作環境を選択させることが出来るそうです。ある意味すごいアイディアですね。

さて、これで終わりではなく、さらにWindowsとUNIX環境の混在・・・となると困ったことがおきます。UNIX環境では「#!/usr/local/bin/perl」なのに、Windows環境では「#!c:\\perl\\perl.exe」だったりするわけです。 これを解消するにはいくつか方法があるようですが「毎回書き換える」、「Windows側にて上記のshebang lineを無効にする設定を行う」というものと、もっとすごいなとおもったのは「無理やりパスをあわせてしまう」というテクニックもあるそうです。

具体的には「c:\\usr\\local\\bin\\perl」を作ってしまえばOKということらしいです。拡張子も取ってしまうわけで、Windows上のファイルとしてはかなりいレギュラーな形ですが、これでもOKなのだそうです。

でも、ここで困ってしまうのが、「WindowsでApache2を使っている時に、提供されているスクリプトが全てshebang lineが付いていないものだった場合」です。これで今日は困りました・・・・。で、どうしたら大丈夫だったかというと、以下の方法です。

#### AddType + ActionでCGIを実行させる方法

一方Addhandlerを使わずに、AddTypeとActionディレクティブにてCGIを動作させることも出来るようです(Apache2だけ??)

こちらの場合には意味合いとしてストレートです。

以下のような感じに書けました(PHPの場合)。

```
AddType application/x-httpd-php .php .phtml
Action application/x-httpd-php "/php/php.exe"
ScriptAlias /php/ "C:/php/"

```

きちんと、拡張子ごとにどのようなファイルなのかを指定し、実行ファイルも指し示しているわけですね。

これで無事shebang lineが書かれていないスクリプトでも実行させることが出来ました（＾＾

さて、この文章には間違いが多数含まれています(予想)。是非指摘していただければと思います。また、このあたりをきちんとまとめて解説している文書などあれば教えてください！私は見つけられませんでした！(涙
