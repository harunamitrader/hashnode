---
title: "notebooklm-pyでNotebookLMをフル自動化する"
datePublished: Sun Mar 29 2026 03:39:40 GMT+0000 (Coordinated Universal Time)
cuid: cmnb7nedq000902l2bxpq438d
slug: notebooklm-py-20260329
tags: ai, python, cli, notebooklm

---

> Source: github notebooklm-py

**notebooklm-py** は NotebookLM を Python / CLI / エージェントから操作する非公式ライブラリ＆スキル。Web UI では触れない機能（バッチDL、PPTX/CSV/JSONエクスポート、マインドマップ抽出など）までプログラムで扱えます。

## 主な機能

- ノートブック: 作成・一覧・リネーム・削除、共有リンクと権限管理。  
- ソース追加: URL / YouTube / PDF / テキスト / Word / 音声 / 動画 / 画像 / Google Drive / 貼り付けテキスト。ガイド/全文取得も可。  
- リサーチ: Web/Drive の fast/deep モード＋自動インポート。  
- チャット: 質問履歴とカスタムペルソナ。  
- コンテンツ生成: オーディオ/動画概要、スライドデッキ、インフォグラフィック、クイズ、フラッシュカード、レポート、データテーブル、マインドマップ。  
- エクスポート: MP3/MP4/PDF/PPTX/PNG/CSV/JSON/Markdown/HTML でダウンロード。クイズ/カード/マインドマップの構造化出力やバッチDLに対応。

## 使い方（CLI）

```bash
pip install "notebooklm-py[browser]"
playwright install chromium   # 初回認証用
notebooklm login              # ブラウザでサインイン

notebooklm create "My Research"
notebooklm use <notebook_id>
notebooklm source add "https://example.com/article"
notebooklm source add ./paper.pdf
notebooklm ask "要点をまとめて"
notebooklm generate audio "ポッドキャスト風で" --wait
notebooklm download audio ./podcast.mp3
```

その他: `notebooklm generate slide-deck / quiz / flashcards / infographic / mind-map / data-table`、`notebooklm auth check --test`、`notebooklm skill status` など。

## Python (async) で使う

```python
from notebooklm import NotebookLMClient
import asyncio

async def main():
    async with await NotebookLMClient.from_storage() as client:
        nb = await client.notebooks.create("Research")
        await client.sources.add_url(nb.id, "https://example.com", wait=True)
        ans = await client.chat.ask(nb.id, "Summarize it")
        print(ans.answer)
        status = await client.artifacts.generate_quiz(nb.id)
        await client.artifacts.wait_for_completion(nb.id, status.task_id)
        await client.artifacts.download_quiz(nb.id, "quiz.json", output_format=\"json\")

asyncio.run(main())
```

## エージェント連携

- Claude Code / Codex / OpenClaw 用の SKILL と AGENTS.md を同梱。`npx skills add` や `notebooklm skill install` で組み込める。  
- エージェントから自然文で「NotebookLM にソースを追加してクイズを作成→JSONでDL」といったワークフローを実行可能。

## 注意点

- **非公式 & 未公開 API 依存**: Google が内部エンドポイントを変更すると壊れる可能性あり。  
- レート制限や利用規約の遵守は自己責任。  
- 安定性が必要なら PyPI リリース版を使用し、main ブランチは検証環境で。

## まとめ

notebooklm-py を使えば NotebookLM のインポート、リサーチ、チャット、生成、ダウンロードをすべてコードから制御できます。まずは `pip install "notebooklm-py[browser]"` でログインし、`notebooklm generate ...` と `download` のペアを一つ動かしてフローを体験してみてください。