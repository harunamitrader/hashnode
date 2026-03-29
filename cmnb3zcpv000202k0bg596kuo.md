---
title: "Supabase CLIでプロジェクト管理を一気通貫にする"
datePublished: Sun Mar 29 2026 01:57:00 GMT+0000 (Coordinated Universal Time)
cuid: cmnb3zcpv000202k0bg596kuo
slug: supabase-cli-20260329
tags: postgres, cli, supabase, edge-functions

---

> Source: github supabase/cli

Supabase をローカルでもクラウドでも効率よく回すための公式ツールが **Supabase CLI**。ローカル開発環境の起動、DBマイグレーション、Edge Functions の作成/デプロイ、スキーマから型生成、Management API 呼び出しまで一つで扱えます。

## できること

- ローカルで Supabase を起動 (`supabase start` など)  
- Postgres マイグレーション管理 (`supabase db migrate ...`)  
- Edge Functions の作成・デプロイ (`supabase functions deploy`)  
- DB スキーマから型生成 (`supabase gen types ...`)  
- Management API への認証付きリクエスト

## インストール

- **npm (dev 依存)**: `npm i -D supabase`  
  - yarn 4 は `NODE_OPTIONS=--no-experimental-fetch` を指定  
  - Bun <1.0.17 は trusted dependency 登録が必要  
- **Homebrew**: `brew install supabase/tap/supabase`（mac/Linux）  
- **Scoop**: `scoop bucket add supabase https://github.com/supabase/scoop-bucket.git` → `scoop install supabase`（Windows）  
- **Linux パッケージ**: Releases に `.deb/.rpm/.apk/.pkg.tar.zst` あり  
- **Go install**: `go install github.com/supabase/cli@latest`（パスに `supabase` を symlink）

## 初回セットアップ

```bash
supabase bootstrap
# もしくは npx supabase bootstrap
```
スターターテンプレからプロジェクト作成を対話で案内してくれます。

## 互換性メモ

- CLI のコマンド/フラグは semver 準拠。  
- ただし依存コンテナイメージ次第で schema/seed/generated types の互換性は完全ではないため、必要なら CLI バージョンを package.json で pin するのがおすすめ。

## ドキュメント

コマンド・設定リファレンス: https://supabase.com/docs/reference/cli/about

## まとめ

Supabase CLI を入れておけば、ローカル開発→マイグレーション→Edge Functions デプロイ→型生成まで同じツールで回せます。まずは `supabase bootstrap` を走らせ、既存プロジェクトなら `supabase db migrate` や `supabase functions deploy` を手元で試してみてください。