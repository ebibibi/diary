---
title: "[vbscript][work] Windows VistaでのWSH(VBScript)の管理者権限への昇格方法"
date: 2008-08-13
tags: 
  - "vista"
---

Windows Vistaになってからクライアントでちょっとレジストリを書き換えたい・・・なんていう場合でもユーザーアカウント制御(UAC)のブロックに阻まれて困っていました。XP以前と同じように普通にWScript.ShellのRegWriteで書き込もうとしても失敗してしまいます。管理者権限を持っているアカウントで実行してもダメなんです。たとえば以下のようなコードですね。

```
   1: Set WshShell=WScript.CreateObject("WScript.Shell")
```

```
   2: WshShell.RegWrite "HKLM\SOFTWARE\Test\value", "test", "REG_SZ"
```

どうすれば良いのかと悩んだ末に妥協案として考えたのがregedit.exeを使う方法です。あらかじめ読み込ませたいregファイルを用意しておき、スクリプト中でregedit.exeを呼ぶことでレジストリへの書き込みが一応成功します。ただし、UACが有効な環境ですので、プロンプトが出ます。

これ自体は当たり前なのですが、以下のような点で困りものです。

- あらかじめファイルを用意せずに動的に値を決定するような場合、regファイルをスクリプト内でつど作成する必要がある。
- レジストリに書き込みに行く度に毎回ユーザーがクリックしなければならない。
- 単純にめんどくさい・・・。

できればユーザーの権限昇格のクリックは1度にしたい・・・そんな方法は無いものかと調べていたら以下のブログで紹介されていました。

- [目から鱗 w/SQLite » Vistaにおいて、VBScriptスクリプト中で管理者権限に移行する方法](http://kandk.cafe.coocan.jp/nucleus/index.php?itemid=639&catid=3)

```
do while WScript.Arguments.Count=0 and WScript.Version>=5.7
```

```
  'Check if Vista
```

```
  Set wmi = GetObject("winmgmts:" & "{impersonationLevel=impersonate}!\\.\root\cimv2")
```

```
  Set os = wmi.ExecQuery ("SELECT * FROM Win32_OperatingSystem")
```

```
  For Each value in os
```

```
    if left(value.Version,3)<6.0 then exit do 'Exit if not Vista
```

```
  Next
```

```
  'Run this script as admin.
```

```
  Set sha=CreateObject("Shell.Application")
```

```
  sha.ShellExecute "wscript.exe",""""+WScript.ScriptFullName+""" vista","","runas"
```

```
  WScript.Quit
```

```
loop
```

Shell.ApplicationオブジェクトのShellExecuteメソッドで実現可能ということです。

実際に試してみたところ、きちんと昇格でき、レジストリへの書き込みもうまくいきました。昇格の確認画面が出てきます。

昇格後はXP以前と同じようにWScript.ShellのRegWriteでレジストリへの書き込みが実施できます。

これはすばらしい、詳しく知りたい!ということでMSの公式ドキュメントを探しているのですが見つかりません。書くべきとしては以下の場所だと思うのですが。

- [ShellExecute Method (IShellDispatch2)](http://msdn.microsoft.com/en-us/library/bb774148.aspx)

もうちょっと探したところ以下のブログに記述がありました。

- [Utility Spotlight: Script Elevation PowerToys for Windows Vista](http://technet.microsoft.com/en-us/magazine/cc162321.aspx)

> The first annoyance was that there was no method to elevate an application from the command line or from the Run dialog box. So after asking around within Microsoft, I came across a sample script from John Stephens (a Software Design Engineer at Microsoft) that provided the information I needed. It turns out that if you pass the verb "runas" to either the ShellExecute API or to its COM equivalent, the ShellExecute method of Shell.Application, the application launched will prompt for　elevation (see the sidebar for details).

MSが公式に公開している手法ではないということでしょうか??

いずれにせよこれでVista用にもスクリプトが普通に書けるようになった気がします。ちょっと幸せな気分になりました。
