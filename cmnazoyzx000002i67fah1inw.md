---
title: "Claude Code Video ToolkitでAI動画制作を自動化する"
datePublished: Sat Mar 28 2026 23:56:57 GMT+0000 (Coordinated Universal Time)
cuid: cmnazoyzx000002i67fah1inw
slug: claude-code-video-toolkit-20260329-hn
tags: ai, video, remotion, claude

---

> Source: github claude-code-video-toolkit

Claude Code で「企画→デザイン→収録→音声→レンダリング」までこなすためのオールインワン環境が **Claude Code Video Toolkit** です。`/setup` と `/video` の 2 コマンドから始まり、テンプレート・スキル・GPU デプロイ手順・ブランド設定が一式揃っています。

## これで何ができる？

- **コマンドドリブンの動画制作**: `/setup` でクラウド GPU・ストレージ・ボイスを対話セットアップ → `/video` でテンプレから動画生成を開始。
- **スキルのパック**: Remotion、FFmpeg、ElevenLabs、Playwright 録画、Qwen Edit、ACE-Step 音楽、LT-X2 動画生成、RunPod/Modal デプロイなど。
- **テンプレ & サンプル**: `templates/` に sprint-review / product-demo ほか、`examples/` に完成動画と Remotion プロジェクト。
- **プロジェクト管理**: `project.json` でシーン・音声・進捗をトラッキングし、`CLAUDE.md` を自動更新して再開時のコンテキストを即座に共有。
- **Python & Docker ツール**: 音声・音楽・効果音・画像編集・アップスケール・redub まで `tools/` と `docker/` でレシピ完備。

## 主なコマンド（Claude Code 内）

- `/setup` : 初期セットアップ（GPU, ファイル転送, ボイス設定）
- `/video` : プロジェクト新規/再開、テンプレ選択
- `/scene-review` : Remotion Studio でシーンごとのレビュー
- `/design` : デザイン修正セッション
- `/brand` : ブランドプロファイル作成・編集（色/フォント/ボイス）
- `/template` : テンプレ一覧/作成
- `/skills` : インストール済みスキルの確認
- `/record-demo` : Playwright でブラウザ操作録画
- `/generate-voiceover` / `/redub` / `/voice-clone` : 音声生成・差し替え
- `/versions` : 依存バージョン確認

変更を反映する場合は Claude Code を再起動すれば読み込み直されます。

## セットアップ手順（最短ルート）

1. クローン  
   `git clone https://github.com/digitalsamba/claude-code-video-toolkit && cd claude-code-video-toolkit`
2. 音声/画像ツールが欲しいとき  
   `pip install -r tools/requirements.txt`
3. Claude Code をこのフォルダで開く  
   `claude` を起動しワークスペースを設定
4. Claude Code 内で  
   `/setup` → GPU・ストレージ・ボイスを対話設定  
   `/video` → テンプレを選び最初の動画を生成
5. すぐ成果物を見たい場合  
   `cd examples/hello-world && npm install && npm run render` （APIキー不要で MP4 出力）

要件: Node.js 18+、Claude Code。音声・動画加工には Python 3.9+ と FFmpeg があると便利。

## どんな動画に強い？

- **Sprint Review 系**: 進捗・デモをまとめるテンプレ（`templates/sprint-review*`）  
- **Product Demo**: ブランド色と CTA を効かせたプロダクト紹介（`templates/product-demo`）  
- **カスタム構成**: `/template` で自分用テンプレを定義し、ブランド設定を当てる

`examples/` / `projects/` には実プロジェクトと完成動画リンクが揃っているので、完成イメージを掴みやすいです。

## コストと無料枠

- Modal Starter 無料枠: $30/月（GPU 実行に使用可）
- Cloudflare R2: 10GB 無料 + egress 無料
- RunPod: 代替 GPU オプション
→ 月数本なら無料枠中心で十分テスト可能な設計。

## 注意点・運用ヒント

- Claude Code 前提の構成。スキル/コマンド更新時はエディタ再起動で反映。
- GPU とストレージのリージョンを合わせ、転送料を抑えるとコスト最適化しやすい。
- `brands/*` で色・フォント・ボイスを先に決めてから `/video` を流すと一貫したルックで出力できる。
- 重いシーンは Remotion で分割し、`project.json` のフェーズをこまめに進めるとリカバリが簡単。

## まとめ

Claude Code Video Toolkit は「Claude Code を動画制作の実戦ツールに変えるスターターパック」です。  
`/setup` と `/video` を走らせるだけで、GPU 準備からテンプレ適用、ブランド反映まで一気に体験できます。まずは hello-world をレンダリングするか、好きなテンプレで一本出力してワークフローの感触を掴んでみてください。