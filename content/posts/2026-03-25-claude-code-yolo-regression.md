---
title: Claude Codeのyoloモードが壊れてた話 — sensitive fileリグレッション調査記
date: 2026-03-25T12:30:00Z
draft: false
tags: [claude-code, debugging, oss]
categories:
    - tech
---

Claude Codeの`--dangerously-skip-permissions`（通称yoloモード）が、いつの間にか特定のファイルに対して効かなくなっていた。調査して原因を特定したので記録しておきます。

## 発端

Discordから自分のClaude Code環境（[ccdb](https://github.com/ebibibi/claude-code-discord-bridge)経由）に`.bashrc`の編集を頼んだら、「許可が必要です」と返ってきた。yoloモードで動かしてるのに。以前は何の問題もなく`.bashrc`を編集できていたので、何かが壊れたとしか思えない。

## 調査：2層構造の権限チェック

調べてみると、CLIの権限チェックが2つのレイヤーに分かれていることがわかった。

| レイヤー | 対象 | yoloフラグ |
|---------|------|-----------|
| ツール実行レベル | Bash / Edit / Write 等のツール呼び出し許可 | バイパスされる |
| ファイルレベル | `.bashrc`, `.claude/`, `.ssh/` 等の sensitive file への書き込み | **バイパスされない** |

つまり `--dangerously-skip-permissions` は第1層しか突破できず、第2層のsensitive fileチェックはyoloモードでも有効なままになっていた。

面白いのは、**Bashツール**（`echo >> ~/.bashrc`）にはこのファイルレベルチェックがないこと。同じセッションで同じファイルに対して、Editツールは失敗するがBashツールは成功する。

## 原因特定：v2.1.78のリグレッション

upstream の [issue #35895](https://github.com/anthropics/claude-code/issues/35895) で同じ問題が報告されていた。v2.1.78（2026-03-17リリース）でリグレッションとして混入し、最後に動いたバージョンはv2.1.77。`regression`ラベルと`has repro`ラベルが付いている。

ちなみにこのバグの副作用として、`-p`モード（SDK/非対話モード）ではpermission denialが返ってきてもユーザーが承認する手段がないため、モデルが無限リトライに入るという[別の問題](https://github.com/anthropics/claude-code/issues/37935)も報告されている。

## 対応方針

バージョンをv2.1.77に固定する手もあるが、最新版を使い続けたいので、ccdb側でワークアラウンドを実装する方針にした。Edit/Writeがsensitive fileでブロックされた場合に、Bashツールで同等の操作をフォールバックさせる仕組みを入れる予定。

upstreamが直ったらワークアラウンドは外す。

## 教訓

- 「yoloモード」だからといって本当に何でもできるわけではなかった
- CLIの権限チェックには可視化されていない層がある
- OSSの自分の環境を持っていると、こういうリグレッションの切り分けが自力でできるのは強い
