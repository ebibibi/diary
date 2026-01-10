---
title: "[plugin] litebox.rbがIEでうまく動かなかった原因を教えてもらっちゃいました!"
date: 2008-04-01
tags: 
  - "tdiary"
---

- [ebi's diary - Lightbox系ライブラリのまとめ - Lightbox系ライブラリのまとめ , Liteboxプラグイン導入](http://ebi.dyndns.biz/diary/20071229.html#p02)
- [ebi's diary - tdiaryへのWindows Live Writerでの投稿テスト , tdiaryへのWindows Live Writerでの画像投稿テスト , 課題。 , 叱ってもらえる..](http://ebi.dyndns.biz/diary/20080315.html#p02)
- [ebi's diary - litebox.rbが動かなかった理由と新たな問題(原因は間違いなく私)](http://ebi.dyndns.biz/diary/20080320.html)

以前からlitebox.rbプラグインがうまく動かなくて、仕方なくワークアラウンドを行っていましたが、プラグイン作者のはしもとさんが親切にも原因を調査してくださいました。はしもとさんありがとうございます!以下、その教えてもらった内容をです。

### 直接の原因

以下が問題が起こせる(たぶん)最小のHTMLです。記述されているjavascriptはlitebox.rbがadd\_footer\_procを使って出力しているものです。

```
   1: <html>
```

```
   2: <head>
```

```
   3: <script type="text/javascript" src="http://ebi.dyndns.biz/litebox/js/prototype.lite.js"></script>
```

```
   4: <script type="text/javascript" src="http://ebi.dyndns.biz/litebox/js/moo.fx.js"></script>
```

```
   5: <script type="text/javascript" src="http://ebi.dyndns.biz/litebox/js/litebox.js"></script>
```

```
   6: <head>
```

```
   7: <body>
```

```
   8: <div class="content">
```

```
   9:             <script type="text/javascript">
```

```
  10:             <!--
```

```
  11:             (function(){
```

```
  12:                 var anchors = document.getElementsByTagName( 'a' );
```

```
  13:                 
```

```
  14:                 for ( var i = 0; i < anchors.length; i++ ){
```

```
  15:                     var anchor = anchors[i];
```

```
  16:                     var rel    = anchor.getAttribute( 'rel' );
```

```
  17:                     var href   = anchor.getAttribute( 'href' );
```

```
  18:                     
```

```
  19:                     if( ( rel == null || rel == '' ) && href && href.match( /\.(?:jpe?g|gif|png)$/i ) ) {
```

```
  20:                         rel = 'lightbox';
```

```
  21:                         
```

```
  22:                         if( href.match( /\/(\d{8})_\d+\.\w+$/i ) ) {
```

```
  23:                             rel += '[' + RegExp.$1 + ']';
```

```
  24:                             
```

```
  25:                             var imgs = anchor.getElementsByTagName( 'img' );
```

```
  26:                             for( var j = 0; j < imgs.length; ++j ) {
```

```
  27:                                 var title = imgs[j].getAttribute( 'title' );
```

```
  28:                                 
```

```
  29:                                 if( title != null ) {
```

```
  30:                                     anchor.setAttribute( 'title', title );
```

```
  31:                                     break;
```

```
  32:                                 }
```

```
  33:                             }
```

```
  34:                         }
```

```
  35:                         
```

```
  36:                         anchor.setAttribute( 'rel', rel );
```

```
  37:                     }
```

```
  38:                 }
```

```
  39:             })();
```

```
  40:             
```

```
  41:             fileLoadingImage = 'http://ebi.dyndns.biz/litebox/images/loading.gif';
```

```
  42:             fileBottomNavCloseImage = 'http://ebi.dyndns.biz/litebox/images/closelabel.gif';
```

```
  43:             initLightbox();
```

```
  44:             // -->
```

```
  45:             </script>
```

```
  46: </div>
```

```
  47: </body>
```

```
  48: </html>
```

つまり、<div class="content">〜</div>というdivタグの中にlitebox.rbの吐き出すjavascriptが入っており、このようになっているとIEではエラーが発生してしまうようなのです。

以下のようにinitlitebox()をbodyタグに記述するようにすると、エラーは起きません。

```
   1: <html>
```

```
   2: <head>
```

```
   3: <script type="text/javascript" src="http://ebi.dyndns.biz/litebox/js/prototype.lite.js"></script>
```

```
   4: <script type="text/javascript" src="http://ebi.dyndns.biz/litebox/js/moo.fx.js"></script>
```

```
   5: <script type="text/javascript" src="http://ebi.dyndns.biz/litebox/js/litebox.js"></script>
```

```
   6: <head>
```

```
   7: <body initLightbox();>
```

```
   8: <div class="content">
```

```
   9:             <script type="text/javascript">
```

```
  10:             <!--
```

```
  11:             (function(){
```

```
  12:                 var anchors = document.getElementsByTagName( 'a' );
```

```
  13:                 
```

```
  14:                 for ( var i = 0; i < anchors.length; i++ ){
```

```
  15:                     var anchor = anchors[i];
```

```
  16:                     var rel    = anchor.getAttribute( 'rel' );
```

```
  17:                     var href   = anchor.getAttribute( 'href' );
```

```
  18:                     
```

```
  19:                     if( ( rel == null || rel == '' ) && href && href.match( /\.(?:jpe?g|gif|png)$/i ) ) {
```

```
  20:                         rel = 'lightbox';
```

```
  21:                         
```

```
  22:                         if( href.match( /\/(\d{8})_\d+\.\w+$/i ) ) {
```

```
  23:                             rel += '[' + RegExp.$1 + ']';
```

```
  24:                             
```

```
  25:                             var imgs = anchor.getElementsByTagName( 'img' );
```

```
  26:                             for( var j = 0; j < imgs.length; ++j ) {
```

```
  27:                                 var title = imgs[j].getAttribute( 'title' );
```

```
  28:                                 
```

```
  29:                                 if( title != null ) {
```

```
  30:                                     anchor.setAttribute( 'title', title );
```

```
  31:                                     break;
```

```
  32:                                 }
```

```
  33:                             }
```

```
  34:                         }
```

```
  35:                         
```

```
  36:                         anchor.setAttribute( 'rel', rel );
```

```
  37:                     }
```

```
  38:                 }
```

```
  39:             })();
```

```
  40:             
```

```
  41:             fileLoadingImage = 'http://ebi.dyndns.biz/litebox/images/loading.gif';
```

```
  42:             fileBottomNavCloseImage = 'http://ebi.dyndns.biz/litebox/images/closelabel.gif';
```

```
  43:             // -->
```

```
  44:             </script>
```

```
  45: </div>
```

```
  46: </body>
```

```
  47: </html>
```

<div class="content">〜</div>は通常のtdiaryでは存在していないタグで、私の場合、自分でサイトのデザインを好き勝手にいじりたくてtdiary/skel内のファイルを直接編集しているためにこのようになっています。

はしもとさんからはさらに以下のコメントをいただきました。

> litebox.rb で initLightbox(); の実行をwindow.onload = initLightbox;のようにonloadイベントハンドラで実行させるようにしていればこのエラーは起こらなかったのですが、このようにしなかったのは、
> 
> - window.onload での実行は画像などすべてのコンテンツの読み込みが終わった後なので、実行タイミングが遅すぎて画像の多いページなどでは困る場合があること。
> - onloadイベントハンドラへの設定の仕方に注意しないと、他にonloadイベントハンドラに何かを設定するプラグインがあった場合、どちらかの設定が消えてしまう可能性があること。（litebox.rbで注意しても、他のプラグインが注意していないと上書きされて消えてしまう）
> 
> などの理由からです。
> 
> litebox.rb 以外でもJavaScriptを使うプラグインで似たようなエラーになる可能性を考えて、<div class="content">〜</div> の閉じ</div>の位置を add\_footer\_proc が埋め込む場所より前にした方がいいかもしれませんね。

なるほど、勉強になります。これでもまだ「initLigthbox()の中では何が行われていて、どこがエラーの原因になるのか」など分かっていない部分もありますが、それはおいおいもしも時間があれば、ということにしようと思います。

このサイトに関してはデザイン自体を見直すかJavascriptでrel属性を追加するのみにするかちょっと考えようと思います。
