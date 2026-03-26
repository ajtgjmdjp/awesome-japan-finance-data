# Awesome Japan Finance Data

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

日本の金融・経済データに関するオープンデータソース、API、Pythonライブラリ、MCPツールのキュレーションリスト。

日本には政府機関や規制当局が提供する豊富な公開金融データがありますが、これらのソースを見つけてアクセスするのは容易ではありません。このリストは、日本の金融データを扱う開発者、研究者、アナリストのための包括的なガイドを目指しています。

**言語:** [English](README.md) | [日本語](#)

---

## 目次

- [企業開示](#企業開示)
- [株式市場データ](#株式市場データ)
- [政府統計](#政府統計)
- [中央銀行データ](#中央銀行データ)
- [金融ニュース](#金融ニュース)
- [ベンチマーク・データセット](#ベンチマークデータセット)
- [AIエージェント](#aiエージェント)
- [MCPツール](#mcpツール)
- [関連Awesomeリスト](#関連awesomeリスト)

---

## 企業開示

### EDINET（金融商品取引法に基づく有価証券報告書等の開示書類に関する電子開示システム）

金融庁が運営する日本の公式電子開示システム。米国のSEC EDGARに相当。

| | |
|---|---|
| **URL** | https://disclosure.edinet-fsa.go.jp/ |
| **データ** | 有価証券報告書、四半期報告書、XBRL財務諸表 |
| **カバレッジ** | 上場企業5,000社以上＋ファンド |
| **認証** | APIキー（無料登録） |
| **形式** | REST API (JSON), XBRL, PDF |
| **レート制限** | 公式には未公開 |
| **利用規約** | 商用・非商用問わず出典表記で利用可。[公共データ利用規約(PDL1.0)](https://www.digital.go.jp/en/resources/open_data/public_data_license_v1.0)準拠。スクレイピング禁止、API利用可 |

**Pythonライブラリ:**
- [edinet-mcp](https://github.com/ajtgjmdjp/edinet-mcp) - XBRLパーサー＋MCPサーバー。161の正規化ラベル、26の財務指標、複数企業スクリーニング対応。 [![PyPI](https://img.shields.io/pypi/v/edinet-mcp)](https://pypi.org/project/edinet-mcp/)
- [edinet_xbrl](https://github.com/BuffettCode/edinet_xbrl) - XBRLファイルのダウンロードとパース。(136 stars)
- [edinet-tools](https://github.com/matthelmer/edinet-tools) - EDINET Python SDK。(26 stars)
- [edinet2dataset](https://github.com/SakanaAI/edinet2dataset) - EDINETを使ったデータセット構築ツール。(31 stars)

**APIリファレンス:** https://disclosure.edinet-fsa.go.jp/api/v2

### TDNET（適時開示情報伝達システム）

日本の取引所上場企業のリアルタイム企業開示システム。

| | |
|---|---|
| **URL** | https://www.release.tdnet.info/inbs/I_main_00.html |
| **データ** | 決算短信、M&A発表、配当変更、自社株買い |
| **カバレッジ** | 全TSE上場企業 |
| **認証** | なし（公開HTML） |
| **形式** | HTML（公式APIなし） |
| **利用規約** | 公開情報、公式API利用規約なし |

**Pythonライブラリ:**
- [TimelyDisclosure](https://github.com/DesSecurities/TimelyDisclosure) - TDNET＋Kabutan＋PRTIMES通知ボット。(3 stars)

### EDINET DB

日本の上場企業の有報データを構造化して提供するプラットフォーム。JP GAAP・IFRS・US GAAPを統一スキーマに名寄せ。英語対応。

| | |
|---|---|
| **URL** | https://edinetdb.jp/（日本語）/ https://edinetdb.com/（英語） |
| **データ** | 名寄せ済み財務諸表（90項目）、有報全文テキスト（事業リスク、MD&A、経営方針等）、財務健全性スコア、AI企業サマリー、TDNet決算短信、大量保有報告書、販管費内訳 |
| **対象** | 上場企業3,800社超、FY2011〜2026（16年分） |
| **認証** | APIキー（Googleログインで無料発行） |
| **料金** | Free（100件/日）/ Pro ¥4,980/月（1,000件/日）/ Business ¥29,800/月（10,000件/日） |
| **形式** | REST API（JSON、16エンドポイント）、リモートMCPサーバー（17ツール、SSEトランスポート） |
| **利用規約** | 全プランで商用利用可。APIを使ったアプリ構築を明示的に許可。データベースの一括複製・再API化は禁止。[利用規約](https://edinetdb.jp/legal/terms)参照 |

**APIリファレンス:** https://edinetdb.jp/docs/api-reference

**MCPガイド:** https://edinetdb.jp/docs/mcp-guide

**メソドロジー:** https://edinetdb.jp/docs/methodology（名寄せロジック、スコアリングアルゴリズム、ガード条件を全公開）

### BuffettCode

日本企業財務データの商用API。

| | |
|---|---|
| **URL** | https://www.buffett-code.com/ |
| **データ** | 財務諸表、KPI、同業比較 |
| **認証** | APIキー（有料プラン） |
| **形式** | REST API (JSON) |

**ツール:**
- [buffett-code-mcp-server](https://github.com/BuffettCode/buffett-code-mcp-server) - BuffettCode APIのMCPサーバー。(1 star)

---

## 株式市場データ

### J-Quants API（JPX公式）

日本取引所グループ（JPX）の公式株式データAPI。TSE株価の一次ソース。

| | |
|---|---|
| **URL** | https://jpx-jquants.com/ |
| **データ** | 日次OHLCV、決算サマリー、決算発表カレンダー、指数データ |
| **カバレッジ** | 全TSE上場銘柄 |
| **認証** | APIキー（無料登録） |
| **料金** | Free（5 req/分、2年データ・12週遅延）/ Light ¥1,650/月 / Standard ¥3,300/月 / Premium ¥16,500/月 |
| **形式** | REST API (JSON) |

**Pythonライブラリ:**
- [jquants-api-client](https://github.com/J-Quants/jquants-api-client-python) - 公式Pythonクライアント。pandas DataFrame返却。Apache-2.0。(175 stars) [![PyPI](https://img.shields.io/pypi/v/jquants-api-client)](https://pypi.org/project/jquants-api-client/)
- [jquants-derivatives](https://pypi.org/project/jquants-derivatives/) - デリバティブデータクライアント。

> **利用規約に関する重要事項:** J-Quants APIは個人の私的利用に限定されています。法人利用、第三者へのデータ配信、データを利用したアプリの提供は、営利・非営利を問わず禁止されています。詳細は[利用規約](https://jpx-jquants.com/termsofservice)を参照してください。

### Yahoo Finance（yfinance経由）

TSE上場銘柄を含むグローバル株式データ。日本株は`.T`サフィックスを使用（例：トヨタは`7203.T`）。

| | |
|---|---|
| **URL** | https://finance.yahoo.co.jp/ |
| **データ** | 日次/日中OHLCV、配当、株式分割、企業情報 |
| **カバレッジ** | TSE銘柄（`.T`サフィックス経由） |
| **認証** | なし |
| **形式** | Pythonライブラリ（スクレイピングベース） |

**Pythonライブラリ:**
- [yfinance](https://github.com/ranaroussi/yfinance) - Yahoo Financeから市場データをダウンロード。Apache-2.0。(21,000+ stars)

> **注意:** yfinanceはウェブスクレイピングに基づいています。Yahooがレート制限やアクセスブロックを行う可能性があります。商用利用前にYahooの利用規約を確認してください。

### Stooq

日本株を含む無料ヒストリカルデータ。

| | |
|---|---|
| **URL** | https://stooq.com/ |
| **データ** | ヒストリカルOHLCV |
| **カバレッジ** | 日本株（`.JP`サフィックス） |
| **認証** | なし |
| **形式** | CSVダウンロード |

**Pythonライブラリ:**
- `pandas-datareader`で`data_source='stooq'`を指定してアクセス

---

## 政府統計

### e-Stat（政府統計の総合窓口）

全府省の政府統計を集約した日本の中央ポータル。

| | |
|---|---|
| **URL** | https://www.e-stat.go.jp/ |
| **データ** | 人口、GDP、CPI、労働、貿易、地域データ |
| **カバレッジ** | 全府省から3,000以上の統計表 |
| **認証** | APIキー（https://www.e-stat.go.jp/api/ で無料登録） |
| **形式** | REST API (JSON/XML) |
| **レート制限** | 1リクエスト/秒 |
| **利用規約** | 政府オープンデータ、利用自由 |

**Pythonライブラリ:**
- [estat-mcp](https://github.com/ajtgjmdjp/estat-mcp) - 検索、メタデータ、データ取得、Polarsエクスポート対応のMCPサーバー。 [![PyPI](https://img.shields.io/pypi/v/estat-mcp)](https://pypi.org/project/estat-mcp/)

**APIリファレンス:** https://www.e-stat.go.jp/api/api-info

### 金融庁（FSA）

金融規制データとRSSフィードを提供する日本の金融規制当局。

| | |
|---|---|
| **URL** | https://www.fsa.go.jp/ |
| **データ** | 規制に関する告知、処分事例 |
| **認証** | なし |
| **形式** | RSS, HTML |

**RSSフィード:** https://www.fsa.go.jp/en/rss.html

---

## 中央銀行データ

### 日本銀行（BOJ）統計データ

日本銀行が公開する時系列統計データ。フラットファイル形式でダウンロード可能。

| | |
|---|---|
| **URL** | https://www.stat-search.boj.or.jp/ |
| **データ** | CGPI（企業物価指数）、短観（企業短期経済観測調査）、資金循環、国際収支、BIS統計、金利、マネーストック |
| **カバレッジ** | 16のデータセットカテゴリ |
| **認証** | なし（公開データ） |
| **形式** | ZIP内CSV（Shift_JISエンコーディング） |
| **利用規約** | 日本銀行は特殊法人であり政府機関ではない。データは公開されている |

**Pythonライブラリ:**
- [boj-mcp](https://github.com/ajtgjmdjp/boj-mcp) - Shift_JIS自動変換とPolarsエクスポート対応のMCPサーバー。 [![PyPI](https://img.shields.io/pypi/v/boj-mcp)](https://pypi.org/project/boj-mcp/)
- [BOJ](https://github.com/stefanangrick/BOJ) - BOJデータ用Rパッケージ。(CRAN)

**データカタログ:** https://www.stat-search.boj.or.jp/info/dload_en.html

---

## 金融ニュース

### 無料RSSフィード（動作確認済み）

| ソース | URL | 言語 | 内容 |
|---|---|---|---|
| **Yahoo!ニュース - ビジネス** | `https://news.yahoo.co.jp/rss/topics/business.xml` | 日本語 | ビジネス・経済ヘッドライン |
| **ロイター日本 - ビジネス** | `https://assets.wor.jp/rss/rdf/reuters/business.rdf` | 日本語 | 金融・マーケット報道 |
| **NHK - 経済** | `https://www3.nhk.or.jp/rss/news/cat5.xml` | 日本語 | CPI、日銀、貿易データ関連 |
| **東洋経済オンライン** | `https://toyokeizai.net/list/feed/rss` | 日本語 | ビジネス分析、企業ニュース |
| **Nikkei Asia** | `https://asia.nikkei.com/rss` | 英語 | アジアビジネス（日本含む） |

**Pythonライブラリ:**
- [japan-news-mcp](https://github.com/ajtgjmdjp/japan-news-mcp) - 日本金融ニュースRSSフィード向けMCPサーバー（Yahoo, NHK, Reuters, 東洋経済）。APIキー不要。 [![PyPI](https://img.shields.io/pypi/v/japan-news-mcp)](https://pypi.org/project/japan-news-mcp/)

> **注意:** 日経新聞（nikkei.com）は日本語RSSフィードを廃止しました。Bloomberg Japanには公開RSS・APIがありません。

### 商用ニュースAPI

| プロバイダ | 料金 | 備考 |
|---|---|---|
| **日経** | エンタープライズのみ | 公開APIなし。スクレイピング禁止 |
| **Bloomberg** | エンタープライズ（$20,000+/年） | B-PIPEターミナルAPI |
| **QUICK** | エンタープライズ（個別交渉） | 機関投資家向けデータプロバイダ |
| **Reuters/LSEG** | エンタープライズ（$10,000+/年） | Reuters Connect |

---

## ベンチマーク・データセット

- [jfinqa](https://github.com/ajtgjmdjp/jfinqa) - 日本語金融推論QAベンチマーク。68社の財務諸表から1,000問。 [![PyPI](https://img.shields.io/pypi/v/jfinqa)](https://pypi.org/project/jfinqa/) [![HuggingFace](https://img.shields.io/badge/HF-dataset-yellow)](https://huggingface.co/datasets/ajtgjmdjp/jfinqa)
- [EDINET-Bench](https://github.com/SakanaAI/EDINET-Bench) - 日本の金融タスクにおけるLLM性能評価。(30 stars)
- [JPXTokyoStockExchangePrediction](https://github.com/J-Quants/JPXTokyoStockExchangePrediction) - JPX株価予測コンペティションデータセット。(56 stars)

---

## AIエージェント

日本株リサーチ向けの自律型AIエージェント。単なるAPIラッパーではなく、計画→複数データソース横断取得→検証→構造化レポート生成まで自律的に実行する。

- [dexter-jp](https://github.com/edinetdb/dexter-jp) - 日本株特化の自律型リサーチAIエージェント。EDINET DB + J-Quantsを使用。複数LLM対応（OpenAI, Anthropic, Google, Ollama）。DCFバリュエーション、企業スクリーニング（100+指標）、有報テキスト読解を内蔵。 ![Stars](https://img.shields.io/github/stars/edinetdb/dexter-jp)

---

## MCPツール

[MCP (Model Context Protocol)](https://modelcontextprotocol.io/)はAIアシスタントが外部データソースにアクセスすることを可能にします。以下のMCPサーバーは日本の金融データへの構造化されたアクセスを提供します：

| ツール | データソース | Stars | 認証 |
|---|---|---|---|
| [edinet-mcp](https://github.com/ajtgjmdjp/edinet-mcp) | EDINET（企業開示） | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/edinet-mcp) | EDINET APIキー |
| [estat-mcp](https://github.com/ajtgjmdjp/estat-mcp) | e-Stat（政府統計） | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/estat-mcp) | e-Stat APIキー |
| [boj-mcp](https://github.com/ajtgjmdjp/boj-mcp) | BOJ（中央銀行データ） | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/boj-mcp) | なし |
| [japan-news-mcp](https://github.com/ajtgjmdjp/japan-news-mcp) | 金融ニュース（RSSフィード） | ![Stars](https://img.shields.io/github/stars/ajtgjmdjp/japan-news-mcp) | なし |
| [EDINET DB MCP](https://edinetdb.jp/docs/mcp-guide) | EDINET DB（名寄せ済み財務、テキスト、スクリーニング） | — | EDINET DB APIキー（無料） |
| [buffett-code-mcp-server](https://github.com/BuffettCode/buffett-code-mcp-server) | BuffettCode（商用） | ![Stars](https://img.shields.io/github/stars/BuffettCode/buffett-code-mcp-server) | BuffettCode APIキー |

**統合スタック:** edinet-mcp（有価証券報告書）+ estat-mcp（マクロ統計）+ boj-mcp（金融政策データ）+ japan-news-mcp（ニュース）で、日本の金融データの4大カテゴリをカバーします。

---

## 関連Awesomeリスト

- [awesome-quant](https://github.com/wilsonfreitas/awesome-quant) - クオンツ金融のライブラリ、パッケージ、リソース
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - AIアシスタント向けMCPサーバー
- [awesome-japanese-nlp-resources](https://github.com/taishi-i/awesome-japanese-nlp-resources) - 日本語NLPツールとデータセット

---

## コントリビューション

コントリビューション歓迎です！まず[コントリビューションガイドライン](CONTRIBUTING.md)をお読みください。

ここに掲載されていない日本の金融データソース、API、ツールをご存知の方は、issueを開くかプルリクエストを送ってください。

## ライセンス

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

このリストはCC0でリリースされています。リンク先のプロジェクトにはそれぞれのライセンスがあります。
