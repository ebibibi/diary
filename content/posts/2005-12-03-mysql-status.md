---
title: "<pre>mysql&gt; status"
date: 2005-12-03
tags: 
  - "未分類"
---

\-------------- mysql Ver 14.7 Distrib 4.1.15, for Win32 (ia32) Connection id: 2 Current database: Current user: root@localhost SSL: Not in use Using delimiter: ; Server version: 4.1.15-nt Protocol version: 10 Connection: localhost via TCP/IP Server characterset: sjis Db characterset: sjis Client characterset: sjis Conn. characterset: sjis TCP port: 3306 Uptime: 21 sec Threads: 1 Questions: 3 Slow queries: 0 Opens: 11 Flush tables: 1 Open tabl es: 5 Queries per second avg: 0.143 --------------

再度インポートにトライ

```
移行元：mysqldump -u root -p --default-character-set=binary xoopsdb > xoopsdb
移行先：nkf -s xoopsdb.sjis
移行先：C:\Program Files\MySQL\MySQL Server 4.1\bin>mysql xoopsdb < xoopsdb.sjis -u root -p --default-character-set=binary
```

...。これでもうまくいきませんでした。 本家で検索をしたところ4.1系では基本的に文字化けするとのこと・・・(ショック [http://xoopscube.jp/modules/xhnewbb/viewtopic.php?viewmode=flat&order=ASC&topic\_id=1048&forum=5](http://xoopscube.jp/modules/xhnewbb/viewtopic.php?viewmode=flat&order=ASC&topic_id=1048&forum=5)
