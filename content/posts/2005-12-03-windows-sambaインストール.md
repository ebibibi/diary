---
title: "[windows] sambaインストール"
date: 2005-12-03
tags: 
  - "debian"
---

(比較的)新しく構築したDebianマシンにもsambaをインストールしてWindowsネットワークに参加させる。

```
apt-get install samba

```

Webのインターフェースで設定を行いたいので、swatも導入。

```
apt-get install swat

```

swatの起動を行わせるように設定ファイルを変更。

```
emacs /etc/ineted.conf
swat steram tcp nowait.400 root /usr/sbin/tdpd /sr/sbin/swat
(行頭の##を削除)

```

inetedの再起動

```
/etc/init.d/inetd restart

```

これで、910番ポートでswatに接続できるようになる。 http://localhost:910で設定画面にアクセス！
