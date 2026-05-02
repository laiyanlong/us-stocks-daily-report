# US Stocks Daily Report — Data

> Auto-generated daily reports + structured JSON for the **DappGo US Stocks** mobile app.

This repo contains only the **published outputs** of the analysis pipeline.
The engine itself is proprietary and lives in a separate private repo.

## Contents

```
reports/YYYY-MM-DD.md          每日美股策略報告 (markdown)
dashboard/data.json            App 與 dashboard 共用的結構化資料
dashboard/index.html           簡易公開瀏覽介面 (GitHub Pages)
schemas/                       JSON Schema 定義
```

## 資料來源

- 股價、新聞、財報日期、機構持股：[yfinance](https://github.com/ranaroussi/yfinance) (Yahoo Finance, free)
- 補充新聞：[Finnhub free tier](https://finnhub.io/)
- 重大公告：[SEC EDGAR](https://www.sec.gov/edgar) 8-K / 10-Q / 10-K filings
- 內部人交易：SEC Form 4
- AI 解讀：Google Gemini

## 涵蓋標的

50 檔，跨 11 GICS 板塊 + ETF（config-driven，未來可 PR `tickers.yaml` 擴充）：

| 板塊 | 代表股 |
|------|------|
| Technology | AAPL, MSFT, NVDA, AVGO, ORCL |
| Communication | GOOGL, META, NFLX, T, VZ |
| Consumer Discretionary | AMZN, TSLA, HD, MCD, NKE |
| Consumer Staples | WMT, PG, KO, COST |
| Financials | JPM, V, MA, BAC, WFC |
| Healthcare | UNH, JNJ, LLY, PFE, ABBV |
| Industrials | CAT, BA, HON, UPS |
| Energy | XOM, CVX |
| Utilities | NEE, DUK |
| Materials | LIN, FCX |
| Real Estate | AMT, PLD |
| ETF | SPY, QQQ, DIA, IWM |

## 排程

每個美股交易日（週一至週五）美東時間 18:30 / UTC 22:30（NYSE 16:00 收盤後 2.5 小時）由 GitHub Actions 自動產生。

## CDN 取用方式

App 透過 jsDelivr 公開 CDN 取資料：

```
https://cdn.jsdelivr.net/gh/laiyanlong/us-stocks-daily-report@main/dashboard/data.json
```

## 三 repo 協同

```
┌─ us-stocks-core (private) ──────────┐
│  Python 引擎 — 每日 GitHub Action   │
│  推送輸出 →                         │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│  us-stocks-daily-report (本 repo)   │
│  reports/*.md, dashboard/data.json, │
│  schemas/data.schema.json,          │
│  dashboard/index.html (GH Pages)    │
└──────────────┬──────────────────────┘
               │ jsDelivr CDN
┌──────────────▼──────────────────────┐
│  dappgo-us-stocks-app (private)     │
│  React Native + Expo 行動 App       │
└─────────────────────────────────────┘
```

| Repo | Visibility | 用途 |
|---|---|---|
| [us-stocks-core](https://github.com/laiyanlong/us-stocks-core) | private | 引擎 — 每日跑分析 |
| **us-stocks-daily-report** (本 repo) | public | 已發布報告 + JSON + 公開 viewer |
| [dappgo-us-stocks-app](https://github.com/laiyanlong/dappgo-us-stocks-app) | private | iOS/iPadOS/macOS 行動 App |

姐妹產品：
- **DappGo TW Stocks** ([tw-stocks-core](https://github.com/laiyanlong/tw-stocks-core) · [tw-stocks-daily-report](https://github.com/laiyanlong/tw-stocks-daily-report) · [dappgo-tw-stocks-app](https://github.com/laiyanlong/dappgo-tw-stocks-app))
- **DappGo Options** ([options-core](https://github.com/laiyanlong/options-core) · [options-daily-report](https://github.com/laiyanlong/options-daily-report) · [dappgo-options-app](https://github.com/laiyanlong/dappgo-options-app))

> **Schema 變動**請先在本 repo 更新 `schemas/data.schema.json`（CI 會擋住格式錯誤的 push），再依序部署 engine、app。

## 授權

報告內容採 [CC BY-NC 4.0](LICENSE) — 個人、研究、教學免費使用，不得商業利用未經授權。
