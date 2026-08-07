# Orca 繁體中文（台灣）語言包

[Orca](https://github.com/stablyai/orca) 的第三方 `zh-TW` UI 語言包外掛。
以術語表治理、CI 驗證、與上游定期同步。

> **狀態：已對齊 Orca v1.4.176（110/110 批，涵蓋 11,967/11,969 條）、驗證通過（錯誤 0、警告 755 為棘輪化的規則債）** — v0.2.0 已發佈。

## 為什麼需要這個外掛

Orca 內建語系為 `en` / `zh` / `ko` / `ja` / `es`，**沒有 zh-TW**。
更關鍵的是 `src/shared/ui-locale.ts` 目前把 `zh-tw` / `zh-hk` / `zh-hant`
一律 fallback 到 **`en`**（而非簡體中文），因此台灣使用者實際看到的是全英文介面。

## 設計原則

| 原則 | 說明 |
|---|---|
| **英文為 ground truth** | 所有翻譯以 `en.json` 為準，簡體中文僅作產品語境的消歧參考，不作範本 |
| **術語表是核心資產** | `locales/zh-TW.json` 是可由 pipeline 重建的衍生物；[`glossary/`](./glossary/) 才是長期維護的對象 |
| **可重跑，不可手改** | 上游 `en.json` 約每週增減數百條，一次性譯本會迅速腐爛；一切經 pipeline 重生 |
| **fail-closed 驗證** | 五道 CI gate 任一失敗即擋下發佈 |

## 涵蓋範圍

| 項目 | 數量 |
|---|---|
| 上游 `en.json` 字串總數（v1.4.176） | 12,183 |
| 平台保護、不可翻譯（`auto.components.settings.Plugin*`） | −214 |
| source-identical（3 條純 CSS + 20 條 CLI 指令，寫入 en 原值不翻譯） | −23 |
| **本語言包待翻譯** | **11,946** |

受保護條目在 Orca 中會回退為英文（屬預期行為）；source-identical 條目則直接寫入英文原值——
CSS 與 CLI 指令翻譯後會失效或無法執行。發佈產物仍涵蓋 11,969 條。

## 目錄結構

```
orca-plugin.json          外掛 manifest
locales/zh-TW.json        唯一發佈產物（由 pipeline 產生，勿手改）

glossary/                 ★ 長期核心資產
  glossary.json             術語表（confirmed / provisional）
  blacklist.json            中國大陸慣用語黑名單（96 條）
  style-guide.md            翻譯風格規範
  ruling-queue.json         待實境裁決的一詞多義詞
  divergence-analysis.json  831 個分歧詞的來源比對數據
  decisions.log.jsonl       append-only 裁決記錄
  inbox/                    翻譯 session 回報的疑慮詞

pipeline/
  snapshots/                上游 en.json 快照與歷史
  refs/zh-8923.json         簡中語境參考（不發佈）
  prompts/ out/             翻譯 prompt 與各批輸出

scripts/
  analysis/                 本專案的資料分析腳本（可重跑）
  validate/                 五道 CI gate

docs/
  plan.md                             完整執行規劃
  plan-engineering-appendix.md        工程契約附錄
  decisions-brief.md                  事實基礎與 D1–D13 決策記錄
```

## 術語表現況

| 區塊 | 詞數 | 影響字串 |
|---|---|---|
| `confirmed`（硬約束） | 330 | — |
| `contextual`（provisional／disputed，軟約束） | 462 | — |
| `ruleCovered`（由 style-guide 通則涵蓋） | 45 | 2,336 |
| `phraseConsistency`（非術語，轉一致性檢查） | 39 | 48 |
| `pending` | 0 | — |

831 個分歧詞已全數納管，`pending` 為 0——翻譯 session 不會遇到無規範可循的詞。
其中 168 個詞附有例外 key 枚舉（共 204 條 key），標示該詞在特定畫面的不同語意。

`contextual` 中有 **13 個**高影響一詞多義詞標記 `needsContextReview`
（`open` / `review` / `active` / `link` / `source` / `view` / `preview` /
`ready` / `base` / `key` / `cursor` / `installed` / `enter`）——
正確譯法取決於實際 UI 呈現，翻譯時**必須連同完整上下文回報**後才定案。

其餘 `contextual` 詞條已有建議 `default`，翻譯時遵循即可，有異議則回報，
不可自行偏離（避免各批各行其是）。

## 安裝（尚未可用）

發佈後將透過 Orca 的 plugin marketplace 安裝：
在 Orca 設定中新增 marketplace source，指向本專案的 registry repo。

## 授權與來源

本專案採 MIT。衍生自 MIT 授權的 [stablyai/orca](https://github.com/stablyai/orca)
（© 2026 Lovecast Inc.），完整來源標註與衍生方法見 [`NOTICE.md`](./NOTICE.md)。

本專案與 Stably / Lovecast Inc. 無隸屬關係，非官方發行。
