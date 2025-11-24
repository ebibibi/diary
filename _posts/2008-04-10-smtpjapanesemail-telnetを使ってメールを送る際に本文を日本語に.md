---
title: "[smtp][japanese][mail] telnetを使ってメールを送る際に本文を日本語にする簡単な方法"
date: 2008-04-10
tags: 
  - "tips"
---

> ちなみに本文を日本語でテストしようと思ったらどうしたらいいんすかね・・・？やってみたのですが届いたメールが文字化けしちゃって・・・。誰か知っていたら教えてください。
> 
> [_telnetを使ってメールのテストを行う方法 | IDEA\*IDEA_](http://www.ideaxidea.com/archives/2008/04/telnet.html)

というわけで、知っている話題だったので反応してみます。いくつかやり方はありますが、テスト目的ですし、一番簡単にやるのであれば本文をJISコード(ISO-2022-JP)でベタに書いてあげるので良いと思います。

それではどうやってJISコードを書いてあげればいいのか・・・?という話になりますが、一番簡単にやるにはtelnetのcodesetを変更してしまうのがいいと思います。Windows付属のtelnetであれば以下のようにできます。

1. コマンドプロンプトを起動
2. 「telnet」を実行
3. 「set codeset JIS Kanji」を実行

こうしておくだけで、漢字が自動的にJISコードに変換されて送信されます。これであとは本文に普通に漢字を書けば基本的にOKなのですが、ヘッダに以下を書いておくとさらに安心です。(参考：[FAQ for rt100i-users(users mailing-list) 'MailBody'](http://www.rtpro.yamaha.co.jp/RT/FAQ/Users/MailBody/wrong-kanji.html))

```
Mime-Version: 1.0
Content-Type: Text/Plain; charset=iso-2022-jp
Content-Transfer-Encoding: 7bit
```

というわけで、具体的には以下のようになります。

```
   1: telnet
```

```
   2: Microsoft Telnet> set codeset JIS Kanji
```

```
   3: エミュレーションの種類: VT100/漢字コードセット: JIS Kanji
```

```
   4: Microsoft Telnet> open ebi.dyndns.biz 25
```

```
   5: 220 ebi.dyndns.biz ESMTP Postfix (Debian/GNU)
```

```
   6: helo test
```

```
   7: 250 ebi.dyndns.biz
```

```
   8: mail from:hoge@hoge.com
```

```
   9: 250 2.1.0 Ok
```

```
  10: rcpt to:ebi@ebi.dyndns.biz
```

```
  11: 250 2.1.5 Ok
```

```
  12: data
```

```
  13: 354 End data with <CR><LF>.<CR><LF>
```

```
  14: Mime-Version: 1.0
```

```
  15: Content-Type: Text/Plain; charset=iso-2022-jp
```

```
  16: Content-Transfer-Encoding: 7bit
```

```
  17:  
```

```
  18: 漢字
```

```
  19:  
```

```
  20: .
```

```
  21: .
```

```
  22: 250 2.0.0 Ok: queued as 0ADB681C095
```

注意点ですが、Windowsのコマンドプロンプト内で漢字入力をONにするにはALT+半角/全角キーを押します。貼り付けでもOKですけれども。

これでテストしたところきちんと漢字で表示させる事ができました。

ただ、一番最後の<CR><LF>.<CR><LF>の部分がなぜかうまく1発で認識されなかったのが不思議です。漢字入力に関連して何か変なコードが紛れ込んでしまっている気もします・・・が今回は深追いしませんでした。

内容には間違いや正確ではない部分が含まれているかもしれません(含まれていると思います)。よければ指摘をお願いします。
