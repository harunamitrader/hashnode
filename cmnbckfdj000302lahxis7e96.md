---
title: "Open Interpreter: ローカルで動くコード実行LLM"
datePublished: Sun Mar 29 2026 05:57:20 GMT+0000 (Coordinated Universal Time)
cuid: cmnbckfdj000302lahxis7e96
slug: open-interpreter-llm-20260329
tags: ai, devtools, cli

---

> Source: GitHub OpenInterpreter/open-interpreter

## これは何か
Open Interpreter は、LLM にローカル環境でコード実行を任せられるオープンソースのターミナル/ライブラリ。`interpreter` コマンドで ChatGPT 風の対話をしながら Python・JavaScript・Shell などを実行し、結果をストリームで表示する。

## 何ができるのか
- 自然言語でデータ分析、ファイル操作、ブラウザ操作（Chrome コントロール）などを実行。
- Python API から `interpreter.chat()` を呼び出し、プログラム内でタスクを自動化。
- LiteLLM 経由で GPT-4 や Claude など多数のホストモデルを選択、`--local` でローカル LLM も利用可能。
- プロファイル・複数インスタンス・ストリーミング応答などの運用向け機能を備え、Colab や Docker でのデモも用意。

## どう動くのか
`pip install open-interpreter` の後、`interpreter` を起動すると LLM が提案したコード片を `exec()` で実行し、その入出力と進行ログを Markdown でターミナルに流す。モデル指定は `interpreter --model gpt-4o` のように切替、`interpreter --local` でローカル推論。既定では各コード実行前に承認を求め、`-y` や `auto_run=True` で自動実行に切り替え可能。

## どんな人に向いているか
- 手元で完結するコードインタープリタを欲しい個人開発者・研究者
- 社内閉域で LLM によるデータ処理や自動化を走らせたいチーム
- Python スクリプトを増やさずにブラウザ操作やファイル処理を行いたいノンエンジニア／アナリスト

## 注意点
- 任意コードをローカルで動かすため、`-y` や `auto_run` 使用時はファイル破壊・秘密情報漏洩・ネット送信に注意。
- モデル/API キーやコスト管理は利用者側の責任。プロバイダごとの制限（トークン上限、レイテンシ）も考慮する。
- コード実行権限は OS 権限に依存するため、危険コマンドは隔離環境（コンテナ/Colab）で試すのが安全。

## まとめ
ホスト型の「コードインタープリタ」と異なり、Open Interpreter はインターネットやファイルサイズの制限なくローカルで動かせる。まずは `pip install open-interpreter` → `interpreter` を試し、必要に応じてモデル設定や `profiles` で環境を分けると運用しやすい。