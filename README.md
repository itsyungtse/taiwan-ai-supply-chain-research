# 台灣供應鏈研究 — AI Agent Skills

> [English](README.en.md)

透過台灣公開資訊觀測站（MOPS）的月營收資料，追蹤 AI 算力供應鏈趨勢的 AI agent skill，採用 [Culpium 方法論](https://www.culpium.com/p/how-to-use-taiwan-monthly-data-to)。

## 功能

- 擷取台灣上市公司月營收資料（台積電、鴻海、廣達等）
- 套用分析規則：年增率（YoY）、一二月合併、滾動 12 個月、美元換算
- 將營收訊號對應至 4 個供應鏈層級（上游 → 中游 → 下游 → 資本支出）
- 輸出結構化研究報告，包含時間軸推論

## 資料來源

**公開資訊觀測站（MOPS）**：https://mops.twse.com.tw

所有台灣上市公司須在次月 10 日前公布月營收。

## 分析方法

基於 [Culpium 的台灣月營收分析指南](https://www.culpium.com/p/how-to-use-taiwan-monthly-data-to)：

1. **年增率（YoY）** — 一律與去年同期比較
2. **一二月合併** — 農曆新年在一、二月間浮動
3. **滾動 12 個月** — 消除季節性波動
4. **美元換算** — 排除台幣匯率干擾
5. **季節性認知** — 半導體 Q1 偏弱、消費電子 Q4 偏強