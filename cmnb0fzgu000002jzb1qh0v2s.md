---
title: "SiftlyでXブックマークをローカルAI整理"
datePublished: Sun Mar 29 2026 00:17:57 GMT+0000 (Coordinated Universal Time)
cuid: cmnb0fzgu000002jzb1qh0v2s
slug: siftly-ai-bookmarks-20260329
tags: ai, bookmarks, nextjs, claude

---

> Source: github Siftly

X（旧Twitter）のブックマークを、ローカル環境だけで AI 整理・検索できるのが **Siftly**。拡張機能やサブスク不要で、タグ付け／カテゴリ付け／可視化まで自動化します。

## 特徴まとめ

- **完全ローカル志向**: データは手元の SQLite に保存。外部送信は AI 推論リクエストのみ。
- **4段AIパイプライン**: Import → Entity Extraction → Vision Analysis → Semantic Tagging → Categorization。途中で止まっても再開可能。
- **検索と可視化**: FTS5 + Claude rerank で意味検索、インタラクティブな Mindmap、グリッド/リスト表示、カテゴリ・媒体・日付でフィルタ。
- **インポートが簡単**: ブックマークレット or ブラウザコンソールスクリプト。再インポート時は重複スキップ。
- **エクスポート**: メディアDL、CSV/JSON/ZIP 書き出し。

## セットアップ手順

### 最短: start.sh 1コマンド
```bash
git clone https://github.com/viperrcrypto/Siftly.git
cd Siftly
./start.sh
```
依存導入・DB初期化・Claude CLI 認証確認・`http://localhost:3000` オープンまで自動。

### Claude Code 派
```bash
git clone https://github.com/viperrcrypto/Siftly.git
claude Siftly/
```
`CLAUDE.md` を読んで CLI が自動案内・起動します。

### 手動
```bash
npm install
npx prisma generate
npx prisma migrate dev --name init
npx next dev
```

## AI 認証の優先順

1) **Claude Code CLI**（macOS）: サインイン済みなら自動検出・鍵不要  
2) アプリ内 Settings で API Key を貼る  
3) `ANTHROPIC_API_KEY` を `.env.local` に設定  
4) `ANTHROPIC_BASE_URL` で互換プロキシ指定  
設定状況は Settings 画面のバッジで確認できます。

## 4段パイプラインの中身

- **Entity Extraction**: ハッシュタグ/URL/@mention/100+ツール名を抽出（無料・APIコールなし）  
- **Vision Analysis**: 画像・GIF・動画サムネを OCR＋物体/シーン解析（30–40タグ）  
- **Semantic Tagging**: テキスト＋画像文脈から 25–35 タグ生成、感情/人物/企業名も抽出  
- **Categorization**: 1–3 カテゴリを信頼度付きで付与  
インクリメンタルに進むので、途中で落ちても再開が早いです。

## だれに向いているか

- X で大量にブクマするが、後から見返せず埋もれがちな人  
- ブラウザ拡張なし・クラウド不要でプライベートに整理したい人  
- Claude Code をすでに使っており、追加設定なしで AI 整理を回したい人

## 注意点

- Claude Code CLI なしの場合は Anthropic API Key が必要（特に Linux/Windows）。  
- 画像解析が多いと推論コストが増えるので、再解析は範囲を絞ると良い。  
- データはローカル SQLite。バックアップは `prisma` ディレクトリごと取っておくと安心。

## まとめ

Siftly は「X ブックマークをローカル AI で整理する」ことに振り切ったツールです。`./start.sh` を叩くだけで動くので、まずは手元のブクマをインポートして検索・Mindmap の体験を試してみてください。