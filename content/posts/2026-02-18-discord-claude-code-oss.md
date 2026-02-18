---
title: DiscordからClaude Codeを使える仕組みをOSSとして公開した
date: 2026-02-18T14:31:00Z
draft: false
tags: [claude-code, discord, oss, github-actions, ci-cd]
categories:
    - tech
---

業務でClaude Codeをフル活用する中で、「これがあったら便利だよな」と思いついた仕組みを、そのまま作って公開するまでやってしまいました。

## 作ったもの

**claude-code-discord-bridge** というOSSです。

これを使うと：

- **DiscordのチャンネルからClaude Codeに指示を送れる**
- **GitHub ActionsのCI/CDでも、従量課金のAPIキーを使わずにClaude Codeを動かせる**

今まで「GitHub ActionsでClaude Codeを使いたい」となると、Anthropic APIキーを発行して従量課金で使う必要がありました。でも、Claude Codeのサブスクリプション（Maxプラン等）を契約していれば、APIキーなしでCLIとして動かせます。

このブリッジはそのCLIをDiscordのWebhook経由でつなぐ仕組みで、CI/CDパイプラインからDiscord Bot経由でClaude Codeを呼び出せるようになります。

## 思いつきから公開まで

今日の午後、「あったら便利じゃないか？」と思いつき、そのまま実装しました。

- CLI層のE2Eテスト
- セキュリティ修正
- OSS品質向上（ドキュメント整備）
- リポジトリ名のリネーム（`claude-discord` → `claude-code-discord-bridge`）
- CI/CDの自動化（重複PR防止・自動マージ）
- Discordへの情報リッチ化

こういう「思いついた瞬間に作る」体験ができるのが、Claude Codeとの作業の楽しいところだと思っています。

そしてこのOSSのおかげで、Discordから気軽に指示を飛ばしながら仕事が進められるようになりました。業務の快適さが一段上がった感覚があります。

## 他にも色々やった日

今日はそれ以外にも：

- YouTube動画を公開
- 会社の某プロジェクトのE2Eテストを12本から30本に拡充してパイプラインも整備
- 会社の某プロジェクトのCI/CD認証周りを改善

濃い1日になりました。
