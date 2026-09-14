# HANDOFF — 作業時間ログ

## 現状
- `index.html` 単一ファイル。README記載の機能は実装済み
- 未着手・要検討
  - 年間集計（今は月単位のみ）
  - 案件に「固定額」を持たせて金額欄に反映する
  - 記録の一括入力（同じ案件で複数日）

## 構成（index.html 内）
- 状態 `state`：`{ projects[], entries[], rounding, roundMode, timer }`
  - `projects[]`：`{ id, name, client, rate, color, done }`
  - `entries[]`：`{ id, date:'YYYY-MM-DD', projectId, start:'HH:MM', end:'HH:MM', brk(分), note }`
  - `timer`：`null` または `{ projectId, startedAt(ms) }`
- 計算：`durMin(entry)` 実働分、`roundUp(min)` 丸め、`summarize(month)` が集計・明細をまとめて返す
- 描画：`renderToday / renderList / renderSum / renderProjects`、まとめて `renderAll()`
- Excel：`exportMonth(month)`。集計シートは案件セルを案件色で塗る

## 方針
- 色はパレット式（ブラウザ標準カラーピッカーは使わない）
- Excelは書式のみ・関数なし
- タイマー停止時は直接保存せず、手入力欄に流し込んで内容を書いてから保存する（内容の書き忘れ防止）
- 保存キーを変える場合は `load()` に移行処理を足す
