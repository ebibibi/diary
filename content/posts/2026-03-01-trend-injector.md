---
title: ニュースを読んでAIが英語動画のネタを作るシステムを実装した
date: 2026-03-01T14:49:46Z
draft: false
tags: [claude-code, ai, youtube, python]
categories:
    - tech
---

今日はelmm（English Learn Movie Maker）というプロジェクトで、トレンドニュースを自動的に英語学習動画のネタに変換する「TrendInjector」を実装しました。一日で3回バージョンアップするという密度の濃い開発でした。

## TrendInjectorとは

elmmは英語学習動画を全自動で生成してYouTubeに投稿するシステムです。これまでは動画のテーマが固定的で、バズりにくいという課題がありました。そこで「そのとき話題になっているニュースを動画ネタにしたらどうか」という発想で作ったのがTrendInjectorです。

## v1→v2→v3の進化

**v1（朝）**: はてなブックマーク・NHK・Yahoo Japan・Hacker Newsからトレンド記事を収集し、Gemini ProがLLM変換して英語学習テーマに落とし込む。毎晩22:00に自動実行。

**v2（昼）**: 「記事タイトルだけでは浅い」というフィードバックで、はてブのコメントとHNのコメントも取得するように拡張。`trend_note`が「タイトルの言い換え」から「なぜバズっているか・コメントの感情の要約」に進化しました。

> "A blog post titled 'No jobs for Rust' is resonating with developers. Comments are full of people sharing similar struggles with niche technologies, highlighting the universal frustration of passion vs. job market mismatch."

こういう解説文をLLMが生成し、動画の例文エージェントが文化的文脈のある英語例文を作れるようになりました。

**v3（夜）**: 「コメントだけでもまだ浅い。記事原文を全部渡せ」ということで、記事URLをHTTP fetchしてHTMLをテキスト変換、最大5000字を渡すように。ThreadPoolExecutorで6並列fetchして高速化。プロンプト総文字数が1万字から5.6万字に増えましたが、その分生成されるテーマの解像度が格段に上がりました。

「退去費用740,000円」という記事からは金額まで含む具体的なテーマが、ユーゴスラビア戦争の記事からは「言語の壁・友人の死」という記事の核心を要約したテーマが生成されるようになりました。

## おまけ: YouTube Live配信

今日は13時から3時間のYouTube Live配信もしました。Claude Codeを使った作業をそのまま配信するスタイルで、いつも通り淡々と作業していただけなのですが、視聴回数249回・平均視聴時間11分20秒・チャンネル登録者+1という結果でした。

「勉強になります」というコメントをいただいたりして、作業配信というコンテンツが少しずつ成立してきているような気がしています。

## 今日の感想

TrendInjectorは「AIがインターネットを読んで、別のAIが動画を作る」という多段AIパイプラインの一部になっています。v1の実装から数時間でv3まで進化したのは、フィードバックループが素直だったからだと思います。「もっとコンテキストを渡せ」という方向性がブレなかった。

明日はこのシステムが実際にどんな動画を生成するか、品質評価システムで採点してみる予定です。
