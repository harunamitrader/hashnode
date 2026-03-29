---
title: "Skill Creatorでスキル開発を回す方法"
datePublished: Sun Mar 29 2026 01:58:06 GMT+0000 (Coordinated Universal Time)
cuid: cmnb40scy000402jsg46tcqoz
slug: skill-creator-guide-20260329
tags: ai, workflow, skills, eval

---

> Source: github anthropics/skills (skill-creator)

**Skill Creator** は「スキルを作るためのスキル」。SKILL.md の下書きから評価・改善・トリガー最適化まで、開発ループを型化しています。

## 開発ループの全体像

1. **意図を固める**: 何をできるようにしたいか、いつトリガーすべきか、出力形式は何か、テストをどうするかをユーザーとすり合わせ。  
2. **SKILL.md を書く**: frontmatter の name/description を「何をする・いつ使うか」を押し気味に記述。本文は500行以内に抑え、参照ファイルに分割。  
3. **テストケースを作る**: 現実的な 2–3 プロンプトを用意。with-skill と baseline を同時に走らせ、workspace/iteration-N に保存。  
4. **評価する**: assertions を `evals/evals.json` と各 `eval_metadata.json` に書き、grading → benchmark。`eval-viewer/generate_review.py` で人間レビューを行い feedback.json を集める。  
5. **改善する**: フィードバックとベンチマークを見て SKILL.md を調整。必要なら scripts/ に共通処理をまとめ、次の iteration を実行。  
6. **トリガー最適化**: should/should-not trigger の 20 件評価セットを作り、`run_loop` で description をチューニング。best_description を frontmatter に反映。  
7. **（任意）パッケージング**: `package_skill` で .skill を生成し配布。

## 書き方のポイント

- description は「何をするか」と「どんな文脈で必ず使うべきか」を明記して undertrigger を防ぐ。  
- 参照ファイルが大きい場合は目次を用意し、必要なときだけ読むよう誘導。  
- 指示はなるべく理由も添えて説明し、MUST 連発より「なぜ重要か」を伝える。

## テストと評価の運用

- with-skill と baseline は同じターンで並列実行し、timing/token を取りこぼさない。  
- assertions は客観的に判定できるものだけ。主観的な品質は人間レビューで見る。  
- `iteration-N/eval-*` ごとに outputs・grading・benchmark を整理し、差分を追いやすくする。

## 使いどころ

- 新しいワークフローをスキル化したいとき  
- 既存スキルの挙動を改善・トリガー精度を上げたいとき  
- 定量評価（pass rate / time / tokens）と人間レビューをセットで回したいとき

## まとめ

Skill Creator は「意図固め → SKILL.md → テスト → 評価 → 改善 → トリガー最適化」という筋道を踏めるように設計されています。まずは小さなテストケースから回し、feedback.json を取り込みつつ iteration を重ねると、再現性のあるスキル開発サイクルを作れます。