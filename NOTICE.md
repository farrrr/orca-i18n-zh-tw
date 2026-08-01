# NOTICE — 來源標註與衍生關係

本專案是 [Orca](https://github.com/stablyai/orca) 的第三方**繁體中文（台灣）語言包外掛**，
與 Stably / Lovecast Inc. 無隸屬關係，亦非官方發行。

## 上游

| 項目 | 內容 |
|---|---|
| 專案 | [stablyai/orca](https://github.com/stablyai/orca) |
| 授權 | MIT |
| 著作權 | Copyright © 2026 Lovecast Inc. |
| 取用內容 | `src/renderer/src/i18n/locales/en.json`（英文文案，作為翻譯的 ground truth） |

MIT 授權全文與 Lovecast Inc. 著作權聲明保留於本專案 [`LICENSE`](./LICENSE)。

## 翻譯來源與衍生方法

本語言包的繁體中文內容並非直接取自任何既有譯本，而是依下列方法產生：

1. **英文原文（`en.json`）為唯一 ground truth。**
2. 未合併的社群 PR [stablyai/orca#8923](https://github.com/stablyai/orca/pull/8923)
   （作者 [@ansonlotiniat](https://github.com/ansonlotiniat)）所含的**人工審核簡體中文**，
   僅作為**產品語境的消歧參考**使用——用以判斷同一英文詞在不同畫面中的實際語意。
   該 PR 的簡體中文文案本身**不進入本專案任何發佈產物**。
3. 繁體中文文案依台灣用語規範**重新撰寫**，並受本專案術語表
   （[`glossary/glossary.json`](./glossary/glossary.json)）約束。
4. `en.json` 中原本就缺少簡中對應的條目，直接由英文翻譯。

> 說明：#8923 自述其 `zh-TW` 是「以 OpenCC `cn → tw` 由簡中確定性轉換而來，
> 並非針對台灣的獨立文案撰寫」。本專案**不採用**該轉換結果，僅取用其簡中所體現的產品語境判斷。

亦曾比對但**未採用**的譯本：
[#10604](https://github.com/stablyai/orca/pull/10604)（@innocarpe）、
[#7801](https://github.com/stablyai/orca/pull/7801)（@eviannaive）。
比對數據保留於 [`glossary/divergence-analysis.json`](./glossary/divergence-analysis.json)。

## 排除的內容

下列 `en.json` 條目**不包含**於本語言包：

- **214 條** `auto.components.settings.Plugin*` — Orca 平台保護的安全文案，
  外掛語言包一旦包含即整包驗證失敗（見 `plugin-language-pack-artifact.ts`）。
- **3 條** `*.styles.<hash>` — 純 CSS 字串（9,965 / 9,691 / 7,055 字元），
  其中兩條超過平台 8,192 字元上限；且此類內容翻譯無意義。

這些條目在 Orca 中會回退（fallback）為英文原文，屬預期行為。

## 回報與勘誤

翻譯問題請至本專案 GitHub Issues 回報。若原作者對來源標註方式有任何意見，
歡迎開 issue 聯繫，本專案樂意補列共同標註。
