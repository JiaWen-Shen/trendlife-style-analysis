# TrendLife Style Analysis

MKT 社群風格 swipe survey 的分析結果 + 設計師協作意見。

- 受訪者以 `R1`–`R8` 代稱去識別化，真名對照表只存在內部私有 repo（不在此站）。
- 頁面設計判斷維度可留「設計師意見」，經 GitHub Actions（`repository_dispatch` →
  `record-opinion.yml`）append 進 `opinions.json`，約 1 分鐘後 reload 可見。
- 送出意見需通關語驗證（3 位協作設計師共用），伺服器端驗證，錯誤直接 reject 不寫入。

## 部署

`main` push 觸發 `deploy.yml`：把 `index.html` / `materials.html` 內的
`__DISPATCH_TOKEN__` placeholder 換成 repo secret `DISPATCH_TOKEN`，部署到 GitHub Pages
（`build_type=workflow`）。

## Secrets（repo settings → Secrets and variables → Actions）

- `DISPATCH_TOKEN` — fine-grained PAT，只授本 repo 的 `Contents: Read and write` +
  `Actions: Read and write`（讓前端能觸發 `repository_dispatch`），短 TTL、用完可撤銷。
- `OPINION_PASSPHRASE` — 3 位協作設計師共用的通關語，驗證送出的意見合法。

來源資料 / 生成器：內部私有 repo `2026-ME-support`（不公開）。
