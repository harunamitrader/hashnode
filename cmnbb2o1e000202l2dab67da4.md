---
title: "Continue: ソース管理型AIチェックで開発を自動化"
datePublished: Sun Mar 29 2026 05:15:32 GMT+0000 (Coordinated Universal Time)
cuid: cmnbb2o1e000202l2dab67da4
slug: continue-ai-20260329
tags: ai, ci, devtools

---

> Source: GitHub continuedev/continue

## これは何か
Continue は、リポジトリでバージョン管理する AI チェック／エージェントを IDE・CLI・CI から動かせるオープンソース基盤。`.continue/` 配下の markdown でチェック内容を定義し、PR ステータスチェックとして実行する。

## 何ができるのか
- PR 差分を AI がレビューし、セキュリティや入力バリデーション漏れを検出して修正案も提示（GitHub ステータスチェック連携）。
- Mission Control ダッシュボードでエージェント・タスク・ワークフローを管理し、GitHub/Slack/Sentry/Snyk などと連携して自動修正や通知を回せる。
- VS Code / JetBrains 拡張の Agent・Chat・Edit・Autocomplete モードで、エディタ内のコード編集・説明・生成を支援。
- CLI（TUI/ヘッドレス）で CI やサーバー上からリファクタやバッチ処理を実行。
- モデル・プロンプト・ルール・MCP ツールを組み合わせて独自の自動化エージェントを構築可能。

## どう動くのか
`.continue/checks/*.md` にチェックの説明とプロンプトを記述。PR 作成時に GitHub Actions が実行し、合否と修正提案をステータスチェックとして返す。`.continue/agents/` でエージェント、`.continue/rules/` でガイドラインを管理。CLI は `npm i -g @continuedev/cli` で導入し、TUI/ヘッドレス両対応。まずは https://continue.dev/check で手元の PR をクラウド実行して感触を掴める。

## どんな人に向いているか
- PR 品質を自動監査したいチーム開発者
- AI エージェントを IDE と CI に統合したいエンジニア
- Slack や監視ツールとつなげて反復作業を自動化したい SRE / プラットフォームチーム

## 注意点
- モデル/API キーの管理が前提。シークレットは .env や GitHub Secrets などに隔離する。
- チェック品質はプロンプト設計に依存するため、チームのコーディング規約をルール化して継続的にチューニングが必要。
- 自動修正を適用する前にセキュリティ影響や依存関係変更をレビューすること。
- 大規模リポジトリでは初回クローンとコンテキスト生成に時間がかかる。

## まとめ
ソース管理されたチェック定義とエージェントを、IDE・CLI・CI で一貫して動かせるのが Continue の強み。まずは `.continue/checks/` に 1 つチェックを置き、動作確認しながらルールとエージェントを拡張していくとスムーズ。