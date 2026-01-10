---
title: "[moss][css] SharePoint 2007, master pageとcssの関係"
date: 2008-06-12
tags: 
  - "sharepoint"
---

- [CleverWorkarounds ≫ SharePoint Branding - How CSS works with master pages - Part 1](http://www.cleverworkarounds.com/2007/10/08/sharepoint-branding-how-css-works-with-master-pages-part-1/)

素晴らしい説明がなされています(MOSSの仕様が"素晴らしい"とも言う)。以下そこからの抜粋です。

#### SharePoint:CssLinkとSharePoint:CssRegistration

SharePoint:CssLink, SharePoint:CssRegistrationタグにて実際のCSSへのリンクタグが生成されるがこれに癖があるとのことです。

- /\_layouts/1033/styles/core.css?rev=xxxxxxxxというCSSファイルは常に読み込まれる
    - これによって、自分で定義したスタイルが上書きされてしまう
- SharePoint:CssRegistrationは常に**アルファベット順で**CSSファイルを並べる
    
    - core.cssよりもアルファベット順で遅いファイル名にしないとスタイルが上書きされてしまう

##### 具体例

以下のコードが・・・

```
<head runat=“server”>
```

```
[snip]
```

```
<Sharepoint:CssLink runat=“server” />
```

```
<!?Styles used for positioning, font and spacing definitions?>
```

```
<SharePoint:CssRegistration name=“&lt;% $SPUrl:~SiteCollection/Style Library/zz1_black.css%&gt;” runat=“server”/>
```

```
<SharePoint:CssRegistration name=“&lt;% $SPUrl:~sitecollection/Style Library/~language/Core Styles/controls.css %&gt;” runat=“server”/>
```

```
<SharePoint:CssRegistration name=“&lt;% $SPUrl:~SiteCollection/Style Library/~language/Core Styles/Band.css%&gt;” runat=“server”/>
```

```
[snip]
```

```
</head>
```

こうなる

```
<head>
```

```
[snip]
```

```
<link rel=”stylesheet” type=”text/css” href=”/sites/nopub/Style%20Library/en-US/Core%20Styles/Band.css”/>
```

```
<link rel=”stylesheet” type=”text/css” href=”/sites/nopub/Style%20Library/en-US/Core%20Styles/controls.css”/>
```

```
<link rel=”stylesheet” type=”text/css” href=”/sites/nopub/Style%20Library/zz1_black.css”/>
```

```
<link rel=”stylesheet” type=”text/css” href=”/_layouts/1033/styles/core.css?rev=5msmprmeONfN6lJ3wtbAlA%3D%3D”/>
```

```
[snip]
```

```
</head> 
```

#### APPLICATION.MASTER

APPLICATION.MASTERではCSSファイルの指定がなされていないので、テーマを変更してもきちんとすべてのサイトに反映されない。

#### 自分で調べてわかったつもりのこと

以下は自分が今日ちょっといじってわかったつもりになっていることです。(間違いがあるかもしれません。)

- SharePoint:CssLinkタグで展開されるのは、SharePointDesignerで該当のマスターページを開いたときに、リンクされているCSSファイル。リンクの追加、削除はSharePointDesignerから。
- 上記はウソではないがさらに追加で、マスターページを使っているページにリンクされているCSSファイルも展開される。同じマスターページを使っていても、リンクされているCSSファイルはページによって異なる。
- CSSファイルのリンクはスタイルとして実際に使っていると外せない模様。なので、よけいなファイルはリンクさせないこと。
- 最後の手段として、SharePointとしては正しくないけれども、マスターページからCSS関連のタグ自体を削除してしまって、自分でCSSへのリンクタグを書いてしまえば、このあたりに悩まずにすむ
    - でも、きっとそうすると、ブラウザでの設定を行ってもうまく動かなかったり、SharePointデザイナーでスタイル編集しても思い通りにいかなくなったりするはず。でもわかってやるならありなのでは。

いやぁ。相変わらずすごいなMOSSは。
