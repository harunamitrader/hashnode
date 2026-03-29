---
title: "Get Shit DoneでAIコーディングのコンテキストを整える"
datePublished: Sun Mar 29 2026 03:38:22 GMT+0000 (Coordinated Universal Time)
cuid: cmnb7lq3b000002jqf7l9gpfw
slug: gsd-meta-prompt-20260329
tags: ai, devtools, claude, prompting

---

> Source: github get-shit-done

**Get Shit Done (GSD)** は、Claude Code / Codex / Copilot / Cursor / Gemini CLI など各種エージェントに「メタプロンプト + コンテキスト設計」を一括で入れ込むツール。コンテキスト rot を防ぎ、仕様駆動で安定したコード生成を狙います。

## 何が嬉しい？

- インストーラがランタイム別に必要なスキル/プロンプトを配置し、最小コマンドで「要件抽出 → 実装 → 検証」まで回す設計。  
- サブエージェントオーケストレーション、XMLプロンプト、状態管理を裏で処理し、表側はシンプルなコマンドだけ。  
- 多言語 README（英/pt/zh/ja/ko）と Discord/X コミュニティあり。

## インストール

一番速い方法:
```bash
npx get-shit-done-cc@latest
```
対話でランタイム（claude/opencode/gemini/codex/copilot/cursor/windsurf/antigravity/all）と global / local を選択します。

非対話オプション例:
```bash
npx get-shit-done-cc --claude --global   # ~/.claude/ に導入
npx get-shit-done-cc --codex --local     # ./.codex/ に導入（スキル形式）
npx get-shit-done-cc --all --global      # 全ランタイム一括
npx get-shit-done-cc --sdk               # headless 実行用 gsd-sdk も導入
```

## 使い方の目安

- 導入後、各ランタイムでヘルプを確認  
  - Claude/Gemini: `/gsd:help`  
  - OpenCode: `/gsd-help`  
  - Codex: `$gsd-help`
- 「具体的にこう作りたい」という要件を投げると、GSD がコンテキストを整理し、分割されたプロンプトで実装を進める。

## 推奨設定

実行を止めずに回すなら:
```bash
claude --dangerously-skip-permissions
```
権限プロンプトを避けたい場合のみ使用。代替として `.claude/settings.json` に許可リストを書く方法も README に記載。

## 開発者モード

リポジトリをクローンしてカスタマイズ:
```bash
git clone https://github.com/gsd-build/get-shit-done.git
cd get-shit-done
node bin/install.js --claude --local   # ./.claude/ に入れて挙動を試す
```

## 注意点

- ローカルでの自動化が前提。外部データの利用規約は自分で遵守。  
- Codex/Antigravity などスキルベースの環境では SKILL.md が導入される。  
- MIT ライセンスだが、同梱・依存する外部サービスの規約は個別に確認を。

## まとめ

GSD は「AIに投げる前の段取り」を自動化するメタツールです。`npx get-shit-done-cc@latest` で導入し、`/gsd:help` を叩いてから実際の案件を投げてみると、コンテキストが崩れにくい開発フローを体験できます。