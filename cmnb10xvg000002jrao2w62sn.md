---
title: "Memoraでエージェントに永続メモリを付ける"
datePublished: Sun Mar 29 2026 00:34:15 GMT+0000 (Coordinated Universal Time)
cuid: cmnb10xvg000002jrao2w62sn
slug: memora-agent-memory-20260329
tags: ai, memory, rag, mcp

---

> Source: github memora

エージェントに「忘れない力」を持たせる軽量 MCP サーバーが **Memora**。会話ログや知識を永続化し、セマンティック検索・知識グラフ・RAG チャット・重複排除までまとめて提供します。

## できること

- **永続ストレージ**: SQLite ベース。Cloudflare D1 / S3(R2) に暗号化付きで同期も可能。バックアップ/リストア対応。
- **検索**: FTS + ベクトル検索（OpenAI / sentence-transformers / TF-IDF）。タグ・日付・AND/OR/NOT で絞り込み、類似リンクを自動生成。
- **重複排除 & マージ**: LLM で類似メモを検出・比較し、まとめる。
- **知識グラフ可視化**: Mermaid でリンク表示、`--graph-port` でローカルグラフ、Pages/D1 で Cloud Graph も可。
- **チャット統合**: RAG チャットパネルが検索/作成/更新/削除ツールを呼び、メモを対話操作。
- **インサイト**: タグ統計、トレンド、ステイル検出、アクション履歴の時系列ビュー。

## セットアップ

### インストール
```bash
pip install git+https://github.com/agentic-box/memora.git
# オフライン埋め込みを使うなら（約2GB）
pip install "memora[local]" @ git+https://github.com/agentic-box/memora.git
```

### MCP サーバーとして登録（例: Claude Code）
`.mcp.json` に:
```json
{
  "mcpServers": {
    "memora": {
      "command": "memora-server",
      "args": [],
      "env": {
        "MEMORA_DB_PATH": "~/.local/share/memora/memories.db",
        "MEMORA_ALLOW_ANY_TAG": "1",
        "MEMORA_GRAPH_PORT": "8765"
      }
    }
  }
}
```

Cloudflare D1 でクラウド DB を使うなら:
```json
"env": {
  "MEMORA_STORAGE_URI": "d1://<account-id>/<database-id>",
  "CLOUDFLARE_API_TOKEN": "<token>",
  "MEMORA_ALLOW_ANY_TAG": "1"
}
```
（D1 時は `--no-graph` 推奨。可視化は Cloud Graph を利用）

Codex CLI でも `config.toml` に同様に追加可能。

## モデルと環境変数のポイント

- `MEMORA_EMBEDDING_MODEL`: `openai`(既定) / `sentence-transformers` / `tfidf`
- `OPENAI_API_KEY` / `OPENAI_BASE_URL`: 埋め込み・LLM 用（OpenRouter/Azure も可）
- `MEMORA_LLM_MODEL`: 重複比較モデル（既定: `gpt-4o-mini`）
- `CHAT_MODEL`: チャットパネル用（既定: `deepseek/deepseek-chat` → fallback は `MEMORA_LLM_MODEL`）
- `MEMORA_STORAGE_URI`: `d1://` or `s3://` でクラウド同期。`MEMORA_CLOUD_ENCRYPT=true` で暗号化アップロード。

## 使い方の流れ

1. MCP を有効化してエージェントを起動  
2. チャットでメモを追加すると SQLite/D1/S3 に永続化  
3. `semantic-search` ツールで検索、`link` でノード関連付け  
4. LLM dedup を走らせて重複を整理  
5. 必要なら `--graph-port 8765` でローカルグラフをブラウザ表示

## 注意点

- クラウド同期では API トークンやストレージ URI を誤って共有しないこと。  
- オフライン埋め込みモデルは容量が大きい（~2GB）。軽く試すなら `openai` 既定のままが手軽。  
- `MEMORA_ALLOW_ANY_TAG` を有効にすると自由度は上がるが、タグ設計を緩めすぎると検索品質が落ちるので運用方針に合わせて調整。

## まとめ

Memora を MCP に追加するだけで、エージェントに永続メモリ・検索・グラフ・重複整理が一気に加わります。まずはローカル SQLite + 既定の OpenAI 埋め込みで軽く試し、必要に応じて D1 や R2 へ同期を広げるのがおすすめです。