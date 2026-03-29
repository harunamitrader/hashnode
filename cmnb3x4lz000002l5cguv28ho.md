---
title: "ib_chartでIBKRのローカル株価チャートを作る"
datePublished: Sun Mar 29 2026 01:55:16 GMT+0000 (Coordinated Universal Time)
cuid: cmnb3x4lz000002l5cguv28ho
slug: ib-chart-ibkr-local-20260329
tags: charts, python, trading, ibkr

---

> Source: github ib_chart

**ib_chart** は IBKR（Interactive Brokers）のデータをローカルで可視化する軽量 Flask アプリ。シングル/マルチチャートのHTMLページとシンプルなAPIを用意し、スクリーナーや自作ダッシュボードから呼び出せます。

## 何ができる？

- シングルチャート: `ib_chart.html`  
- マルチチャート: `ib_multichart.html`（ウォッチリストやテーマバスケットに便利）
- API エンドポイント  
  - 日足: `GET /api/pricehistory?symbol=AAPL&period_str=1y&hist_source=local|ib`  
  - 1m/5m Intraday: `GET /api/intraday?...`  
  - リアルタイムストリーム: `GET /api/intraday/stream?...`  
  - `GET /api/quote`、`GET /api/eps-revenue`
- データソースは IBKR リアルタイム/ヒストリカル、またはローカルCSV日足(`IB_CHART_LOCAL_DAILY_DIR`)を選択。

## 必要なもの

- Python 3.10+（Windows OK）  
- IB Gateway または TWS（API 有効化）  
- ネットワークはローカル接続前提

## クイックスタート（Windows PowerShell）

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
python ib_server.py
```

ブラウザで  
`http://127.0.0.1:5001/` (UI)  
`/ib_chart.html` or `/ib_multichart.html`

## よく使う環境変数

- `IB_HOST` (既定 127.0.0.1)  
- `IB_PORT` (live 4001 / paper 4002 が多い)  
- `IB_CLIENT_ID` (他ツールとかぶるなら変える)  
- `IB_CHART_LOCAL_DAILY_DIR` ローカル日足CSVのパス

## スクリーナー連携パターン

- **1銘柄だけ開く**: `http://127.0.0.1:5001/ib_chart.html` を新規タブで開いてティッカー入力。  
- **複数銘柄を渡す**: `http://127.0.0.1:5001/ib_multichart.html?symbols=AAPL,MSFT,NVDA&tf=D` を URL で生成し、ボタンから開く。  
- **ダッシュボードに埋め込む**: 上記 URL を iframe に。AI アシスタントに「symbols クエリを動的生成して iframe を貼る」と伝えればノーコードで組み込み可能。

## トラブルシュート（定番）

- **接続失敗/データなし**: TWS/Gateway が動いているか、API 有効か、ポートが正しいかを確認（paper 4002/live 4001 が多い）。`IB_CLIENT_ID` の衝突にも注意。  
- **日足データなし**: `IB_CHART_LOCAL_DAILY_DIR` を設定するか、`hist_source=ib` を指定。  
- **EPS/Revenue が遅い**: 初回は外部ソース取得で数秒かかるがキャッシュされる。

## 安全上の注意

- ローカル利用前提。パブリック公開は推奨しない。  
- マーケットデータの利用規約は各プロバイダに従うこと。  
- MIT ライセンスだが、IBKR API の規約は別途遵守が必要。

## まとめ

ib_chart は「ローカルで動くチャート用マイクロサービス」。手元のスクリーナーやダッシュボードに URL/iframe で足すだけで、IBKR データのチャート表示と簡易 API を確保できます。まずはローカルで立ち上げ、`ib_multichart.html?symbols=...` を生成して使い勝手を試してみてください。