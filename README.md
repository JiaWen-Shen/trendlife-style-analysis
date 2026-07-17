# TrendLife Style Analysis

MKT 社群風格 swipe survey 的分析結果 + 設計師協作意見（單頁，含素材附錄）。

- 受訪者以 `R1`–`R8` 代稱去識別化，真名對照表只存在內部私有 repo（不在此站）。
- 「設計手法 — 共識與分歧」13 張卡各自可留「設計師意見」，經 GitHub Actions
  （`repository_dispatch` → `record-opinion.yml`）append 進 `opinions.json`，約 1 分鐘後 reload 可見。
- 送出意見不需通關語，任何人開頁面都可直接填名字送出（主要填的人跟看的人是同一組小範圍協作）。
- 全站卡碼／引用連結都指向同頁底部的「素材附錄」（`#material-cNN`），不是獨立頁面。

## 部署

`main` push 觸發 `deploy.yml`：把 `index.html` 內的 `__DISPATCH_TOKEN__` placeholder 換成 repo
secret `DISPATCH_TOKEN`，部署到 GitHub Pages（`build_type=workflow`）。

## Secrets（repo settings → Secrets and variables → Actions）

- `DISPATCH_TOKEN` — fine-grained PAT，只授本 repo 的 `Contents: Read and write` +
  `Actions: Read and write`（讓前端能觸發 `repository_dispatch`），短 TTL、用完可撤銷。

來源資料 / 生成器：內部私有 repo `2026-ME-support`（不公開）。
