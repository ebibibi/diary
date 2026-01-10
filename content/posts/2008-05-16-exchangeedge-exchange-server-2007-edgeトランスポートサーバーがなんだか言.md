---
title: "[exchange][edge] Exchange Server 2007 - Edgeトランスポートサーバーがなんだか言うことを聞きません。"
date: 2008-05-16
categories: 
  - "work"
---

今日はExchange Server 2007の検証をしているところにお邪魔しました。いくつかはまったのでメモ。

#### HubからEdgeへのメール送信時のエラー"451 5.7.3 Cannot achieve Exchange Server authentication."

これはExchange Server認証がEdge側の受信コネクタで有効になっていないことが原因でした。エッジサブスクリプションを有効にしているので、EdgeサーバーもExchange組織内のExchangeサーバーとして認識してくれるようで、逆にExchange Server認証が有効にならないといけないようです。

#### エッジサブスクリプションで作成されたEdge to Hubのコネクタの宛先ホストが「--」になっていて届かない

エッジサブスクリプションを作成する段階で名前解決ができていなかったから・・・か？とりあえず手動で編集して検証作業を進めています。後で追試予定。

(追記)

ドキュメントに記述がありました。

> ##### Automatic inbound Send connector configuration
> 
> | Parameter | Value |
> | --- | --- |
> | Name | EdgeSync - Inbound to <_Site Name_\> |
> | Address Space | SMTP:--;1 |
> | Source Servers | Edge Subscription name |
> | Enabled | True |
> | DNS Routing Enabled | False |
> | Smart Hosts | \-- |
> 
> The **\--** placeholder in the address space for the inbound Send connector represents the authoritative and internal relay accepted domains for the Exchange organization and is the literal character displayed. Any messages that the Edge Transport server receives for authoritative and internal relay accepted domains are routed to this Send connector and relayed to the smart hosts.
> 
> The **\--** placeholder in the list of smart hosts represents all the Hub Transport servers that are located in the subscribed Active Directory site and is the literal character displayed. Hub Transport servers that are added to an Active Directory site after an Edge Subscription has been established do not participate in the EdgeSync synchronization process. However, they are automatically added to the list of smart hosts for the inbound Send connector. If more than one Hub Transport server is located in the subscribed Active Directory site, inbound connections will be load balanced across the smart hosts.
> 
> [White Paper: Edge Subscription and Synchronization](http://technet.microsoft.com/ja-jp/library/bb310755\(EXCHG.80\).aspx)

"and is the literal character displayed"という英文の意味がいまいち理解できないのですが、結局「--」と表示されているのが正常ということですよね??(ちがってたらだれか指摘をお願いします。。。)であるならば、メールが送信できなかったのがおかしいことになってしまいますねぇ。

さらに以下の記述も。

> You cannot modify the address space or list of smart hosts for the inbound Send connector.
> 
> [White Paper: Edge Subscription and Synchronization](http://technet.microsoft.com/ja-jp/library/bb310755\(EXCHG.80\).aspx)

cannot...と書いてありますが、修正もできちゃったし、一応まがりなりにもそれでうまく動作しているのですが・・・。

このあたりはやはりDNSまわりも含めて追加検証が必要なようです。

#### Edge to Hubのコネクタの宛先をFQDNにしてもDNSへのクエリに失敗する

EdgeのhostsファイルにFQDNを記述してあるのですが、DNSへクエリを実行してしまい、そして失敗してしまいます。IPアドレスでの指定にすると送信できるのでその他の問題は無いはずなのですが・・・?MSのドキュメントにhostsでOKと書いてあるのですが、それがうそなのかもしれません。おかしいなぁ・・。

(追記)

Exchange Server 2007のドキュメントによっては、EdgeサーバーはDMZにおかれるので、つまりNicを複数もちPublicのネットワークとInternalのネットワークの両方に足を出す、と書いてあるものがあります。なので、それぞれでDNSを構成しておけばよい、と。でも、そんな構成って普通とらないと思うんですよね。普通はDMZに1本足を出しておくだけだろうと。

で、そうなると、DMZからInternalネットワークにあるActiveDirectoryのDNSなんて参照させないほうが良いと思うので(FWに無駄な穴をあけるのいやだし。)DMZにあるEdgeサーバーはInternetの世界のDNSのみを参照させることになると思うんです。で、そうするとHubサーバーの名前解決ができるわけ無いので、この現象になってしまう・・・と。バグ、あるいは製品の設計ミスではないのかなぁ?

Internetの世界のDNSに勝手にad.localとかADで使っているものと同じゾーンをつくって、さらにそこにInternalで使っているprivateIPでAレコードとか書いてしまえばうまく動いちゃう気もするけど、そんな構成なんてありえないし・・・。

#### Edge to Hubの送信時に「認証できない」

HubからEdgeに送信するときにはExchange Server認証のチェックを入れてあげればOKだったのですが、Edge to Hubはそう簡単にはいかないようです。

調べた結果どうやらEdge to Hubに関してはExchange Server 認証ができない(!?)気がします。

仕方が無いので、Hub上でEdge専用の受信コネクタを作成することで回避しました。でも、これは本当なんでしょうか?そもそもExchange Server認証がどのような仕組みなのかがきちんと理解できていないので良く分からないのですが・・・。

仮説。Hub to Edgeに関してはエッジサブスクリプションでHubの情報がEdgeに取り込まれているので、きちんとExchange Server認証ができる。Edge to Hubに関してはエッジサブスクリプションはHub to Edgeの一方向の情報のやり取りのため、Hub上にEdgeの情報はなく、Exchange Server認証ができない。

うーん。でも、エッジサブスクリプションを構成するときに、Edgeで出力したファイルをHubに取り込んでるんだから、そのときに情報を入手すればいいじゃん?と思います。変だなぁ・・・。構成ミスかもしれない。

#### NDRの生成サーバーがHub・・・

一応メールの送受信ができるようになったので、外部からExchange組織の存在しないユーザー宛にメールを送ってみたところ・・・Hubまでリレーされたところでいないと判断されて、NDRが返ってきました。あれ、EdgeってADAMでユーザー情報も保持しているからHubまでリレーしなくてもEdge上でNDRを生成できるのが売りなんじゃなかったっけ?

#### Bugじゃないのか?と。

このあたりの挙動は、自分が悪いのではなくて製品が悪いのではないかと思ってしまいます。Bugじゃねーのか、と。時間がとれたらもうちょっと検証したいですね・・・。
