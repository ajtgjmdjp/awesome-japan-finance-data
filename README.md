# Awesome Japan Finance Data

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of open data sources, APIs, Python libraries, and MCP tools for Japanese financial and economic data.

Japan has rich public financial data from government agencies and regulators, but finding and accessing these sources can be challenging. This list aims to be a comprehensive guide for developers, researchers, and analysts working with Japanese financial data.

**Languages:** [English](#) | [日本語](README_ja.md)

---

## Contents

- [Corporate Disclosures](#corporate-disclosures)
- [Stock Market Data](#stock-market-data)
- [Government Statistics](#government-statistics)
- [Central Bank Data](#central-bank-data)
- [Financial News](#financial-news)
- [Benchmarks & Datasets](#benchmarks--datasets)
- [MCP Tools](#mcp-tools)
- [Related Awesome Lists](#related-awesome-lists)

---

## Corporate Disclosures

### EDINET (Electronic Disclosure for Investors' NETwork)

Japan's official electronic disclosure system operated by the Financial Services Agency (FSA). Equivalent to SEC EDGAR in the US.

| | |
|---|---|
| **URL** | https://disclosure.edinet-fsa.go.jp/ |
| **Data** | Annual/quarterly reports, securities reports (有価証券報告書), XBRL financial statements |
| **Coverage** | 5,000+ listed companies + funds |
| **Auth** | API key (free registration) |
| **Format** | REST API (JSON), XBRL, PDF |
| **Rate Limit** | Not officially published |
| **Terms** | Free for commercial & non-commercial use with attribution. Licensed under [PDL1.0](https://www.digital.go.jp/en/resources/open_data/public_data_license_v1.0). Scraping prohibited; API access allowed. |

**Python Libraries:**
- [edinet-mcp](https://github.com/ajtgjmdjp/edinet-mcp) - XBRL parser + MCP server with 161 normalized labels, 26 financial metrics, multi-company screening. [![PyPI](https://img.shields.io/pypi/v/edinet-mcp)](https://pypi.org/project/edinet-mcp/)
- [edinet_xbrl](https://github.com/BuffettCode/edinet_xbrl) - XBRL file downloader and parser. (136 stars)
- [edinet-tools](https://github.com/matthelmer/edinet-tools) - Python SDK for EDINET data. (26 stars)
- [edinet2dataset](https://github.com/SakanaAI/edinet2dataset) - Dataset construction tool using EDINET. (31 stars)

**API Reference:** https://disclosure.edinet-fsa.go.jp/api/v2

### TDNET (Timely Disclosure Network)

Real-time corporate disclosure system for listed companies on Japanese exchanges.

| | |
|---|---|
| **URL** | https://www.release.tdnet.info/inbs/I_main_00.html |
| **Data** | Earnings reports, M&A announcements, dividend changes, share buybacks |
| **Coverage** | All TSE-listed companies |
| **Auth** | None (public HTML) |
| **Format** | HTML (no official API) |
| **Terms** | Public information, no official API terms |

**Python Libraries:**
- [TimelyDisclosure](https://github.com/DesSecurities/TimelyDisclosure) - TDNET + Kabutan + PRTIMES notification bot. (3 stars)

### BuffettCode

Commercial API for Japanese corporate financial data.

| | |
|---|---|
| **URL** | https://www.buffett-code.com/ |
| **Data** | Financial statements, KPIs, peer comparisons |
| **Auth** | API key (paid plans) |
| **Format** | REST API (JSON) |

**Tools:**
- [buffett-code-mcp-server](https://github.com/BuffettCode/buffett-code-mcp-server) - MCP server for BuffettCode API. (1 star)

---

## Stock Market Data

### J-Quants API (JPX Official)

Official stock data API from Japan Exchange Group (JPX). The primary source for TSE stock prices.

| | |
|---|---|
| **URL** | https://jpx-jquants.com/ |
| **Data** | Daily OHLCV, financial summaries, earnings calendar, index data |
| **Coverage** | All TSE-listed stocks |
| **Auth** | API key (free registration) |
| **Pricing** | Free (5 req/min, 2yr data with 12-week delay) / Light ¥1,650/mo / Standard ¥3,300/mo / Premium ¥16,500/mo |
| **Format** | REST API (JSON) |

**Python Libraries:**
- [jquants-api-client](https://github.com/J-Quants/jquants-api-client-python) - Official Python client. Returns pandas DataFrames. Apache-2.0. (175 stars) [![PyPI](https://img.shields.io/pypi/v/jquants-api-client)](https://pypi.org/project/jquants-api-client/)
- [jquants-derivatives](https://pypi.org/project/jquants-derivatives/) - Derivatives data client.

> **Important Terms of Use:** J-Quants API is limited to individual personal use. Corporate use, third-party data distribution, and building apps that serve data are prohibited regardless of profit motive. See [利用規約](https://jpx-jquants.com/termsofservice).

### Yahoo Finance (via yfinance)

Global stock data including TSE-listed stocks. Use `.T` suffix for Japanese tickers (e.g., `7203.T` for Toyota).

| | |
|---|---|
| **URL** | https://finance.yahoo.co.jp/ |
| **Data** | Daily/intraday OHLCV, dividends, splits, company info |
| **Coverage** | TSE stocks (via `.T` suffix) |
| **Auth** | None |
| **Format** | Python library (scraping-based) |

**Python Libraries:**
- [yfinance](https://github.com/ranaroussi/yfinance) - Download market data from Yahoo Finance. Apache-2.0. (21,000+ stars)

> **Note:** yfinance is based on web scraping. Yahoo may rate-limit or block access. Check Yahoo's terms before commercial use.

### Stooq

Free historical stock data including Japanese stocks.

| | |
|---|---|
| **URL** | https://stooq.com/ |
| **Data** | Historical OHLCV |
| **Coverage** | Japanese stocks (`.JP` suffix) |
| **Auth** | None |
| **Format** | CSV download |

**Python Libraries:**
- Access via `pandas-datareader` with `data_source='stooq'`

---

## Government Statistics

### e-Stat (政府統計の総合窓口)

Japan's central portal for official government statistics from all ministries.

| | |
|---|---|
| **URL** | https://www.e-stat.go.jp/ |
| **Data** | Population, GDP, CPI, labor, trade, regional data |
| **Coverage** | 3,000+ statistical tables from all ministries |
| **Auth** | API key (free registration at https://www.e-stat.go.jp/api/) |
| **Format** | REST API (JSON/XML) |
| **Rate Limit** | 1 request/second |
| **Terms** | Government open data, free to use |

**Python Libraries:**
- [estat-mcp](https://github.com/ajtgjmdjp/estat-mcp) - MCP server with search, metadata, data retrieval, and Polars export. [![PyPI](https://img.shields.io/pypi/v/estat-mcp)](https://pypi.org/project/estat-mcp/)

**API Reference:** https://www.e-stat.go.jp/api/api-info

### FSA (Financial Services Agency)

Japanese financial regulator providing regulatory data and RSS feeds.

| | |
|---|---|
| **URL** | https://www.fsa.go.jp/ |
| **Data** | Regulatory announcements, enforcement actions |
| **Auth** | None |
| **Format** | RSS, HTML |

**RSS Feed:** https://www.fsa.go.jp/en/rss.html

---

## Central Bank Data

### Bank of Japan (BOJ) Statistical Data

Time-series statistics from Japan's central bank, available as flat file downloads.

| | |
|---|---|
| **URL** | https://www.stat-search.boj.or.jp/ |
| **Data** | CGPI (price indices), TANKAN (business surveys), Flow of Funds, Balance of Payments, BIS statistics, interest rates, money stock |
| **Coverage** | 16 dataset categories |
| **Auth** | None (public data) |
| **Format** | CSV in ZIP files (Shift_JIS encoding) |
| **Terms** | BOJ is a special corporation, not a government agency. Data is publicly available. |

**Python Libraries:**
- [BOJ](https://github.com/stefanangrick/BOJ) - R package for BOJ data. (CRAN)

**Data Catalog:** https://www.stat-search.boj.or.jp/info/dload_en.html

### FXMacroData

Macro and central-bank API with JPY coverage alongside other major FX
currencies.

| | |
|---|---|
| **URL** | https://fxmacrodata.com/api-data-docs |
| **Data** | JPY macro announcements, release calendar, central-bank context, FX sessions, and cross-currency macro datasets |
| **Coverage** | Japan plus global FX/macro coverage |
| **Auth** | API key for protected currencies/endpoints; public USD examples are available without an API key |
| **Format** | REST API (JSON), OpenAPI, MCP |

**API Reference:** https://api.fxmacrodata.com/openapi.json

---

## Financial News

### Free RSS Feeds (Verified Working)

| Source | URL | Language | Content |
|---|---|---|---|
| **Yahoo! News Japan - Business** | `https://news.yahoo.co.jp/rss/topics/business.xml` | Japanese | Business/economy headlines |
| **Reuters Japan - Business** | `https://assets.wor.jp/rss/rdf/reuters/business.rdf` | Japanese | Financial/market journalism |
| **NHK - Economy** | `https://www3.nhk.or.jp/rss/news/cat5.xml` | Japanese | CPI, BOJ, trade data coverage |
| **Toyokeizai Online** | `https://toyokeizai.net/list/feed/rss` | Japanese | Business analysis, corporate news |
| **Nikkei Asia** | `https://asia.nikkei.com/rss` | English | Asian business (inc. Japan) |

> **Note:** Nikkei (nikkei.com) has discontinued its Japanese RSS feeds. Bloomberg Japan has no public RSS or API.

### Commercial News APIs

| Provider | Pricing | Notes |
|---|---|---|
| **Nikkei** | Enterprise only | No public API. Scraping prohibited. |
| **Bloomberg** | Enterprise ($20,000+/yr) | B-PIPE terminal API |
| **QUICK** | Enterprise (negotiated) | Institutional data provider |
| **Reuters/LSEG** | Enterprise ($10,000+/yr) | Reuters Connect |

---

## Benchmarks & Datasets

- [jfinqa](https://github.com/ajtgjmdjp/jfinqa) - Japanese Financial Reasoning QA Benchmark. 1,000 questions from 68 companies' financial statements. [![PyPI](https://img.shields.io/pypi/v/jfinqa)](https://pypi.org/project/jfinqa/) [![HuggingFace](https://img.shields.io/badge/HF-dataset-yellow)](https://huggingface.co/datasets/ajtgjmdjp/jfinqa)
- [EDINET-Bench](https://github.com/SakanaAI/EDINET-Bench) - Evaluating LLM performance on Japanese financial tasks. (30 stars)
- [JPXTokyoStockExchangePrediction](https://github.com/J-Quants/JPXTokyoStockExchangePrediction) - JPX stock prediction competition datasets. (56 stars)

---

## MCP Tools

[MCP (Model Context Protocol)](https://modelcontextprotocol.io/) enables AI assistants to access external data sources. These MCP servers provide structured access to Japanese financial data:

| Tool | Data Source | Stars | Auth Required |
|---|---|---|---|
| [edinet-mcp](https://github.com/ajtgjmdjp/edinet-mcp) | EDINET (corporate disclosures) | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/edinet-mcp) | EDINET API key |
| [estat-mcp](https://github.com/ajtgjmdjp/estat-mcp) | e-Stat (government statistics) | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/estat-mcp) | e-Stat API key |
| [tdnet-disclosure-mcp](https://github.com/ajtgjmdjp/tdnet-disclosure-mcp) | TDNET (timely disclosures) | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/tdnet-disclosure-mcp) | None |
| [stockprice-mcp](https://github.com/ajtgjmdjp/stockprice-mcp) | Stock prices & FX (yfinance) | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/stockprice-mcp) | None |
| [FXMacroData MCP](https://mcp.fxmacrodata.com) | JPY and global FX macro events, announcements, and release calendars | N/A | API key for protected coverage |
| [buffett-code-mcp-server](https://github.com/BuffettCode/buffett-code-mcp-server) | BuffettCode (commercial) | ![Stars](https://img.shields.io/github/stars/BuffettCode/buffett-code-mcp-server) | BuffettCode API key |

**Combined stack:** edinet-mcp (filings) + tdnet-disclosure-mcp (disclosures) + estat-mcp (macro stats) + stockprice-mcp (prices) covers the major categories of Japanese financial data. FXMacroData MCP can add cross-currency macro event context for JPY and other FX markets.

---

## Related Awesome Lists

- [awesome-quant](https://github.com/wilsonfreitas/awesome-quant) - Quantitative finance libraries, packages, and resources
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - MCP servers for AI assistants
- [awesome-japanese-nlp-resources](https://github.com/taishi-i/awesome-japanese-nlp-resources) - Japanese NLP tools and datasets

---

## Contributing

Contributions welcome! Please read the [contributing guidelines](CONTRIBUTING.md) first.

If you know of a Japanese financial data source, API, or tool that's not listed here, please open an issue or submit a pull request.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is released under CC0. The linked projects have their own licenses.
