---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---
# Adobe Experience League – 承認されたメタデータフィールドのリファレンス

*Adobe ExL オーサリングガイド（2026 年 2 月クロール）および blueprints-learn.en のリポジトリ分析をソース*

&#x200B;---

## メタデータ階層

メタデータは次の順序でカスケードされます（記事は目次をオーバーライドし、目次はリポジトリをオーバーライドします）。
1. 記事の最優先事項（最優先事項）
2. ユーザーガイドの目次
3. リポジトリルートの metadata.md （最優先度）

&#x200B;---

## 記事レベルのフィールド

### 必須

| フィールド | 説明 | 形式/制約 |
|-------|-------------|----------------------|
| `title` | SEO ページのタイトル。 検索結果に表示されます。 | 最大 60 文字。タイトルケース。製品名には `[!DNL Product]` を使用。意図しない限り、H1 を完全に複製しないでください |
| `description` | 検索エンジンと ExL の推奨事項に関するMetaの説明。 | 150～160 文字、理想的には「学ぶ方法」から始まる または「詳細情報」が表示されます（存在しない、または null の場合、検証は失敗します）。 |
| `exl-id` | システムが割り当てた一意の ID。 コンテンツのトラッキングに使用されます。 | UUID 形式（例：`70573eb9-cd69-4fe6-b2ae-dae81665a308`）、**ファイルをコピーする際に削除** – 自動的に割り当てられます。ファイル間で重複することはありません |

### 強くお勧めします

| フィールド | 説明 | 有効な値 |
|-------|-------------|--------------|
| `solution` | この記事で説明しているAdobe製品 ExL 検索/フィルタリングおよびコンテンツレコメンデーションに使用されます。 | コンマ区切り。大文字と小文字を区別。承認済み列挙に一致する必要があります（以下の有効なソリューション値を参照） |

### OPTIONAL – 共通

| フィールド | 説明 | 有効な値/メモ |
|-------|-------------|----------------------|
| `kt` | 従来のナレッジ記事の JIRA 番号。 Analytics のトラッキングに使用されます。 | 整数（例：`7207`）。空白を使用できます。`null` も使用できます |
| `thumbnail` | Recommendations/analytics のサムネール画像リファレンス。 | ファイル名文字列、`null` または空白 |
| `version` | 製品バージョンフィルター。 主にAEMおよび Campaign ブループリントに使用されます。 | E.g. `Campaign v8`, `Campaign v8 Client Console`; version.yml と一致する必要があります。 |
| `doc-type` | Repo/Analytics で使用されるコンテンツ分類。 | `blueprint`、`overview-page`、`Video`、`Tutorial`、`Troubleshooting` （小文字を優先） |
| `feature` | トピックタグが ExL ページで「トピック」として表示される。 | 記事ごとに 1 ～ 2、タイトルケース。feature.yml と一致する必要があります。コンマ区切り |
| `feature-set` | 機能の検証の親アプリケーションです。 | feature.yml 値と一致する必要があります |
| `role` | ターゲットオーディエンスの役割。 ExL で「作成対象」として表示されます。 | `Admin`, `Architect`, `Data Architect`, `Data Engineer`, `Developer`, `Leader`, `User` |
| `level` | ユーザーエクスペリエンスレベル。 ExL で「作成対象」として表示されます。 | `Beginner`、`Intermediate`、`Experienced` （タイトルケース） |
| `topic` | 検索/フィルタリングに関するクロスプロダクトトピック。 | タイトルケース。topic.yml と一致する必要があります。コンマ区切り |
| `type` | ガイド分類。 | `Documentation` （デフォルト）、`Tutorial`、`Troubleshooting` |
| `last-substantial-update` | 「新機能」ウィジェットのコンテンツをサーフェスします。 | 形式：`YYYY-MM-DD` |
| `hide` | すべての検索およびレコメンデーションからページを除外します。また、インデックスを「いいえ」に設定します。 | `yes` 以 `no` |
| `hidefromtoc` | 目次ナビゲーションからを削除しますが、直接リンクを使用してページに引き続きアクセスできます。 | `yes` 以 `no` |
| `index` | ページを外部検索/サイトマップに表示するかどうかを制御します。 | `yes`/`no` または `y`/`n`。デフォルト：`no` （インデックス付き） |
| `recommendations` | 「この機能に関するその他のヘルプ」ウィジェットの動作を制御します。 | `noDisplay` （ウィジェットの表示を禁止）、`noCatalog` （レコメンデーションプールから除外） |
| `internal` | ページをAdobe内部のみとしてマークします。 内部リンクのフラグの発生を防止します。 | `yes` |
| `short-description` | Exl ランディングページの短い説明。 省略した場合は `description` を使用します。 | 1 文、最大 20 語 |
| `activity` | ページ使用状況の分類。 | `understand`、`implement`、`troubleshoot` （小文字） |
| `sub-product` | 製品サブコンポーネント。 有効な列挙については、ソリューションチームにお問い合わせください。 | 小文字（例：`search`、`assets`、`sites`） |
| `team` | Analytics のチーム割り当て。 | E.g. `TM` |
| `landing-page-name` | パンくずリストのランディングページへのリンク。 | E.g. `experience-manager` |
| `landing-page-breadcrumb-title` | ランディングページリンクのパンくずテキスト。 | E.g. `AEM` |
| `auto-video-transcripts` | デフォルトでビデオトランスクリプトを有効にします。 | `true` |
| `badgeType` | コンテンツステータスのバッジ。 | 様々（`informative`、`positive` など） |
| `badgePremium` | Premium バッジ インジケーター。 | Adobeバッジ仕様あたり |
| `badgeLabel` | バッジのラベルテキスト。 | 短い文字列 |
| `source-git-url` | Source リポジトリ URL。 | 完全な GitHub URL |
| `cloud` | 記事レベルでのクラウドカテゴリの上書き。 | タイトルケース。cloud.yml と一致する必要があります。 |

&#x200B;---

## TOC.md フィールド

| フィールド | 説明 | 備考 |
|-------|-------------|-------|
| `user-guide-title` | ExL のパンくずリストおよびランディングページに表示されるガイド名。 | 目次ファイルに必要 |
| `breadcrumb-title` | ユーザーガイドタイトルが長すぎる場合に、パンくずリストのガイド名を短くする。 | オプション |
| `user-guide-description` | ExL ランディングページのガイドサマリー。 | 1 文、最大 20 単語を推奨 |
| `product` | ガイドの Analytics トラッキング。 単一値のみ。 | product.yml に一致する必要があります（有効な製品値を参照） |
| `mini-toc-levels` | 右ナビゲーションのミニ目次に表示される見出しレベルの数。 | 整数 1～6 （デフォルトは 2） |
| `role` | ガイドのデフォルトオーディエンスの役割。 | Article `role` と同じ値。コンマ区切り |
| `index` | ガイドにインデックスを付けるかどうかを指定します。 | `yes`/`no` |

&#x200B;---

## リポジトリレベルの metadata.md フィールド

| フィールド | 備考 |
|-------|-------|
| `cloud` | リポジトリ内のすべての記事のデフォルトのクラウドカテゴリ |
| `solution` | すべての記事に対応するデフォルトソリューション |
| `product` | 分析トラッキング用のデフォルト製品 |
| `type` | デフォルトのガイドタイプ |
| `doc-type` | デフォルトのドキュメントタイプ |
| `mini-toc-levels` | デフォルトのミニ目次レベル |
| `git-repo` | GitHub リポジトリ URL。「このページを編集」および「問題をログに記録」ボタンを有効にします |
| `index` | デフォルトのインデックス設定 |

&#x200B;---

## 有効なソリューションの値（大文字と小文字を区別）

このリポジトリで使用される一般的な値：
- `Experience Platform`
- `Real-Time Customer Data Platform`
- `Journey Optimizer`
- `Journey Optimizer B2B Edition`
- `Customer Journey Analytics`
- `Campaign`
- `Campaign v8`
- `Campaign Classic v7`
- `Campaign Standard`
- `Audience Manager`
- `Target`
- `Analytics`
- `Data Collection`
- `Commerce`
- `Marketo Engage`
- `Experience Cloud`
- `Journey Orchestration`

複数の値：コンマ区切り（例：`Real-Time Customer Data Platform, Campaign`）

&#x200B;---

## 有効な製品値（`product` のフィールドの場合：Analytics トラッキング）

完全なリストについては、システム プロンプトを参照してください。 キー値：
- `adobe experience platform` / `experience platform` / `aem`
- `adobe analytics` / `analytics` / `aa`
- `adobe journey optimizer` / `journey optimizer` / `jo`
- `adobe customer journey analytics` / `customer journey analytics` / `cja`
- `adobe real time customer data platform` / `real time cdp` / `rtcdp`
- `adobe marketo` / `marketo` / `amk`
- `adobe campaign` / `campaign` / `ac`
- `adobe target` / `target` / `at`

&#x200B;---

## 有効な役割の値

- `Admin`
- `Architect`
- `Data Architect`
- `Data Engineer`
- `Developer`
- `Leader`
- `User`

&#x200B;---

## キー検証ルール

1. コピーしたファイルに同じ UUID の `exl-id` を残さないでください。削除して、システムに新しい UUID を割り当てさせます。
2. 空白または null の `thumbnail` と `kt` を使用できます。これらは従来のフィールドです。
3. 値 `solution`、承認済みの列挙と完全に一致する必要があります（大文字と小文字が区別されます）。
4. `description` 検証は、見つからないか null の場合は失敗します。常に意味のある値を指定します。
5. コロン、角かっこ `title` 先頭の特殊文字が含まれている場合は、値を引用符で囲みます。
6. 複数の `solution` 値は、単一の文字列値でコンマ区切りです。
7. `product` は 1 つの値のみです（analytics のトラッキングの場合）。コンマ区切りの値は使用しないでください。
8. 新しい列挙値をリクエストするには、「コンテンツのタグ付け」コンポーネントを含む UGP JIRA チケットを提出します。
