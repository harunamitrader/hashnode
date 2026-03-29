---
title: "Magic Resumeでモダンなオンライン履歴書を作る"
datePublished: Sun Mar 29 2026 01:46:46 GMT+0000 (Coordinated Universal Time)
cuid: cmnb3m7a2000202js2n8o0mky
slug: magic-resume-online-cv-20260329
tags: resume, webapp, tailwind, tanstack

---

> Source: github magic-resume

**Magic Resume** は TanStack Start + Framer Motion で作られたオンライン履歴書エディタ。リアルタイムプレビュー、テーマ変更、PDF 書き出し、ダークモードなど、モダンな UI でサクッと CV を作れます。

## 主な機能

- リアルタイムプレビュー & スムーズなアニメーション（Framer Motion）
- テーマ/色/タイポのカスタム、ダークモード
- PDF エクスポート
- レスポンシブ設計（モバイルでも編集可）
- オートセーブ＋ローカルストレージ
- Tiptap ベースのリッチエディタ

## 技術スタック

TanStack Start, TypeScript, Framer Motion, Tiptap, Tailwind CSS, Zustand, shadcn/ui, Lucide Icons。

## セットアップ（ローカル）

```bash
git clone https://github.com/JOYCEQL/magic-resume.git
cd magic-resume
pnpm install
pnpm dev
# http://localhost:3000 で開く
```

ビルド: `pnpm build`

## Docker Compose で動かす

```bash
docker compose up -d
```
（プロジェクト同梱の compose をそのまま実行すればビルド＆起動します）

## ライセンスの注意

- Apache 2.0 だが **商用利用は別途ライセンス必須**。  
  - SaaS/PaaS として提供、企業内で営利目的に使う、改変したうえで有償提供する場合は要ライセンス。  
  - 個人の非商用利用（自分の履歴書作成・学習目的）は無料。

## 想定ユース

- 自分の履歴書を素早く整えたいエンジニア/デザイナー
- 既存テンプレをベースに色やレイアウトを微調整したい人
- アニメーション付きのモダンな CV を PDF で出したい人

## まとめ

Magic Resume は「軽くセットアップして、そのまま見栄えの良い履歴書を作る」ことに特化した OSS エディタです。まずは `pnpm dev` で立ち上げ、テーマをいじりつつ PDF 出力を試してみてください。商用で使いたい場合は別途ライセンスの取得をお忘れなく。