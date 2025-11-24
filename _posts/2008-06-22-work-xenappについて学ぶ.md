---
title: "[work] XenAppについて学ぶ"
date: 2008-06-22
tags: 
  - "xenapp"
---

昨日のWindows Server 2008に引き続き、今日はCitrixのソリューションをお勉強。

#### 名前が変わってるよという話。

「Metaframe　→　Citrix Presentation Server　→　Citrix XenApp」というように名前が変わっている模様です。

> シトリックスでは、従来のMetaFrameR製品から大きく飛躍した今回の最新版投入を機に、全ての製品名称を「CitrixR」ブランドと各製品の主機能を表す固有名称の組み合わせとする、製品名称に構造変更を行いました。  
> [_Citrix Systems Japan - Press Room - Press Releases_](http://www.citrix.co.jp/company/press/releases/20050526.html)
> 
> 2008年2月11日、シトリックスはPresentation Server製品名称をXenAppへ変更しました。XenAppという新名称は、アプリケーション仮想化に焦点を当てる核となる製品ということをより反映し、サーバー（XenServer）、アプリケーション（XenApp）、デスクトップ（XenDesktop）のエンドツーエンドの仮想化システムを顧客に提供するための重要性を強調するために決定しました。  
> [_Citrix XenAppについて | オンデマンドアクセスのシトリックス_](http://www.citrix.co.jp/products/cps.html)

#### アプリケーションの仮想化

- Presentation Server自体へのアプリケーション配信にも使える
- クライアントへのアプリケーション配信に使える
- オフラインでも使える

#### ICAプロトコル

- 使用帯域幅が20~30kbps/クライアント
- SpeedScreenテクノロジ
    - キーボード入力をバッファし、Server送信前に画面表示
    - SpeedScreenプログレッシブ表示によりマルチメディアデータも超高速表示
        - 動いている動画は解像度を落として転送。静止時には解像度を復元
- 暗号化

#### サーバーのロードバランシング

#### ヘルスアシスタント

- 常にサーバーの状況をチェックし、問題が発見されると自動的にサーバーを再起動する

#### パスワードポリシーコントロール

#### アプリケーションパフォーマンスモニタリング(状況の監視)

- デリバリーされるアプリケーションのパフォーマンスを可視化し、状態を詳細に分析する

#### SmartAuditor

- SmartAuditorセッション録画
    - ICAパケットを記録し、完全なユーザー操作を録画
- SmartAuditorプレーヤー(問題の再現)
- コンプライアンス対策、セキュリティ強化
- ユーザーサポート

#### SmartAccess(SSL VPN)

- いつでもどこでもどんなクライアントでもセキュアにアクセス可能

#### 場所やPCの安全度に応じたアクセス制御

- ユーザー、グループだけではなく、接続先サーバー、クライアントのIPアドレスなどに応じてセキュリティポリシーをセット可能

#### シングルサインオン

- Webやレガシーなクライアントサーバー型アプリケーションもプログラムの改変なしに一度のWindowsログオンでセキュアにアクセス可能

#### 余談

XenAppの情報を調べていたら、知ってる人が出てきてちょっと驚いた。この業界はやはり・・・・XXXXだなぁ。。。。

#### 参考資料

- [http://www.citrix.co.jp/products/pdf/CPS45FP1\_catalog.pdf](http://www.citrix.co.jp/products/pdf/CPS45FP1_catalog.pdf "http://www.citrix.co.jp/products/pdf/CPS45FP1_catalog.pdf")
- [Citrix Presentation Server 4.5 製品カタログ](http://www.citrix.co.jp/products/pdf/CPS45FP1_catalog.pdf)

#### 感想

どの程度の値段なのか良く知らないけど、機能的にはWindows Server 2008 + SoftGridでいいんじゃないの?という気がする。あとは実績による安定度、パフォーマンス、操作性あたりの問題か。
