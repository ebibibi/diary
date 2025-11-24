---
title: "[verifier][windbg][debug] Verifier.exeでのDRIVER_CORRUPTED_EXPOOL(c5)を引き起こすドライバの調査方法(w2k)"
date: 2008-08-18
categories: 
  - "windows"
---

※以下に書いてあるのは、私の現段階での理解にもとづく手法です。あまり自信がありません。このあたり詳しい人がいたらコメント等頂けるとうれしいです。

DRIVER\_CORRUPTED\_EXPOOL(c5)のエラーに関しては、プール領域が不正なドライバによって意図せず書き換えられていることが原因の事がほとんどです。この場合ブルースクリーン発生時のダンプファイルを解析しても、問題が発生している場所にアクセスしたことはわかりますが、何が問題を引き起こしたのかという原因の特定には結び付きません。

> 0: kd> !analyze -v
> 
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
> 
> \* \*
> 
> \* Bugcheck Analysis \*
> 
> \* \*
> 
> \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
> 
> DRIVER\_CORRUPTED\_EXPOOL (c5)
> 
> An attempt was made to access a pageable (or completely invalid) address at an
> 
> interrupt request level (IRQL) that is too high. This is
> 
> caused by drivers that have corrupted the system pool. Run the driver
> 
> verifier against any new (or suspect) drivers, and if that doesn't turn up
> 
> the culprit, then use gflags to enable special pool.
> 
> Arguments:
> 
> Arg1: 00000000, memory referenced
> 
> Arg2: 00000002, IRQL
> 
> Arg3: 00000001, value 0 = read operation, 1 = write operation
> 
> Arg4: 8046c6e4, address which referenced memory

この場合Verifier.exeにてドライバの動作を検証し、問題のドライバを特定することが可能な場合があります。

#### Windows 2000でのVerifier.exeの設定方法

1. 問題が発生する端末にてverifier.exeを起動します。  
    [![clip_image002](images/clip_image002_thumb.jpg)](http://ebi.dyndns.biz/diary/images/Verifier.exeDRIVER_CORRUPTED_EXPOOLc5_FFB5/clip_image002.jpg)
2. 「Setting」タブにて以下のオプションを有効にします。  
    ・Special pool  
    ・Pool tracking  
    [![clip_image005](images/clip_image005_thumb.jpg)](http://ebi.dyndns.biz/diary/images/Verifier.exeDRIVER_CORRUPTED_EXPOOLc5_FFB5/clip_image005.jpg)
3. 同じく「Setting」タブにて、問題があることが疑われるドライバを個別にVerifyするように設定変更します。  
    [![clip_image009](images/clip_image009_thumb.jpg)](http://ebi.dyndns.biz/diary/images/Verifier.exeDRIVER_CORRUPTED_EXPOOLc5_FFB5/clip_image009.jpg)
4. 「Apply」を押したあと、「Exit」を押します。再起動に関する注意がでますので、「OK」を押します。  
    [![clip_image011](images/clip_image011_thumb.jpg)](http://ebi.dyndns.biz/diary/images/Verifier.exeDRIVER_CORRUPTED_EXPOOLc5_FFB5/clip_image011.jpg)
5. システムを再起動します。
6. 再起動後、再度verifier.exeを起動します。
7. 問題を再現させます。
8. 「Global Counters」タブにて状態を確認します。「Succeded」と「Succeeded ? special pool」の値が同じであり、「Failed」の値が0になっているのが正しい状態です。この状態でない場合には、Verify中のドライバに問題が発生したことになります。  
    [![clip_image013](images/clip_image013_thumb.jpg)](http://ebi.dyndns.biz/diary/images/Verifier.exeDRIVER_CORRUPTED_EXPOOLc5_FFB5/clip_image013.jpg)

#### 参考情報

- [エラー メッセージ : STOP 0x000000C5 DRIVER\_CORRUPTED\_EXPOOL](http://support.microsoft.com/kb/291810/ja)
- [Driver Verifier を使用して Windows ドライバをトラブルシューティングする方法](http://support.microsoft.com/kb/244617)
- [Special Pool 機能を使用してプールの破損箇所を特定する](http://support.microsoft.com/kb/188831/)
- [Special Pool](http://msdn.microsoft.com/en-us/library/ms792863.aspx)
- [Monitoring Global Counters](http://msdn.microsoft.com/en-us/library/ms792848.aspx)
