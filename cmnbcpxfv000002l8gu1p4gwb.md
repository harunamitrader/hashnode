---
title: "AutoGen: マルチエージェント開発の定番フレームワーク"
datePublished: Sun Mar 29 2026 06:01:36 GMT+0000 (Coordinated Universal Time)
cuid: cmnbcpxfv000002l8gu1p4gwb
slug: autogen-20260329
tags: ai, devtools, agents

---

> Source: GitHub microsoft/autogen

## これは何か
AutoGen は Microsoft 製のオープンソース・マルチエージェント開発フレームワーク。Python/.NET 両対応で、メッセージパッシングからツール実行、分散ランタイムまでをレイヤー化して提供し、複数エージェントの協調タスクを素早く作れる。

## 何ができるのか
- 二者チャットやグループチャット、コード実行・ツール呼び出しを組み込んだワークフローをテンプレから構築。
- AutoGen Studio でノーコードにマルチエージェントのプロトタイプを作成・実行（デモ用途）。
- AutoGen Bench でエージェント挙動をベンチマークし、プロバイダ/プロンプト/ルールを比較。
- Magentic-One などのリファレンス実装や .NET/Python サンプル群から実運用の構成を学習。
- OpenAI/Azure/Anthropic/Ollama など多数の LLM クライアントを Extensions 経由で切替。

## どう動くのか
Core API がイベント駆動のエージェントとローカル/分散ランタイムを提供し、その上に高レベルの AgentChat API（2 Agent、GroupChat などのパターン）が載る。Extensions API で LLM クライアントやコード実行機能をプラグイン化。ノーコードで試す場合は `autogenstudio ui --port 8080 --appdir ./my-app` を起動し、サーバー上でワークフローを操作する。

## どんな人に向いているか
- まずはテンプレでマルチエージェントを素早く試したい開発者
- Python/.NET を跨いでエージェント基盤を統一したい企業チーム
- 評価（Bench）から本番実装までを一貫させたい MLOps / プラットフォームエンジニア

## 注意点
- AutoGen Studio はデモ/試作目的で、認証やセキュリティを自前で実装する必要がある。
- 多エージェント構成は無限ループや不要トークン消費が起こりやすいので、停止条件・ログ・予算管理を明示的に設定する。
- 各 LLM プロバイダの API キー/コスト/レート制限は利用者責任。機密データを扱う場合は送信先モデルを慎重に選ぶ。

## まとめ
AutoGen は「フレームワーク＋Studio＋Bench」で開発・試作・評価まで揃うエコシステム。まずは AgentChat のサンプルを動かし、必要に応じて Extensions で使うモデルやツールを差し替え、Bench で効果を計測する流れが手堅い。