---
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 8%
---
# Adobe Experience League – 承認済みメタデータフィールドのリファレンス

*Adobe ExL オーサリングガイドから取得（2026年2月クロール） + ブループリントのリポジトリ分析 – learn.en*

&#x200B;---

## メタデータ階層

メタデータのカスケードをこの順序で作成します（記事は目次を上書きし、目次はリポジトリを上書きします）。
1. 記事の前面（最優先）
2. ユーザーガイドのTOC.md
3. metadata.mdをリポジトリルート（最優先度）に設定します。

&#x200B;---

## 記事レベルのフィールド

### 必須

| フィールド | 説明 | 形式/制約 |
|-------|-------------|----------------------|
| `title` | SEO ページのタイトル： 検索結果に表示されます。 | 最大60文字、タイトルケース、製品名に`[!DNL Product]`を使用、意図しない限りH1を正確に複製しない |
| `description` | 検索エンジンとExL レコメンデーションに関するMetaの説明。 | 150～160文字。理想的には「方法を学ぶ」を開始します。 または「詳細を見る…」です。見つからない場合やnullの場合、検証が失敗します。 |
| `exl-id` | システムに割り当てられた一意のID。 コンテンツの追跡に使用されます。 | UUID形式（例：`70573eb9-cd69-4fe6-b2ae-dae81665a308`）、**ファイルのコピー時に削除** – 自動割り当て、ファイル間で重複しない |

### 強く推奨

| フィールド | 説明 | 有効な値 |
|-------|-------------|--------------|
| `solution` | 記事がカバーしているAdobe製品。 ExL検索/フィルタリングおよびコンテンツレコメンデーションに使用されます。 | カンマ区切り、大文字と小文字を区別、承認済み列挙に一致させる必要があります（以下の有効なソリューション値を参照）。 |

### オプション – 共通

| フィールド | 説明 | 有効な値/メモ |
|-------|-------------|----------------------|
| `kt` | 従来のナレッジ記事のJIRA番号。 分析トラッキングに使用します。 | 整数（例：`7207`）、空白で使用可能、`null`で使用可能 |
| `thumbnail` | レコメンデーション/分析のためのサムネイル画像リファレンス。 | ファイル名文字列または`null`または空白 |
| `version` | 製品バージョンフィルター： 主にAEMとCampaignのブループリントに使用されます。 | E.g. `Campaign v8`、`Campaign v8 Client Console`；はversion.ymlと一致する必要があります |
| `doc-type` | リポジトリ/分析で使用されるコンテンツ分類。 | `blueprint`、`overview-page`、`Video`、`Tutorial`、`Troubleshooting` （小文字を優先） |
| `feature` | ExL ページで「Topics」として表示されるトピックタグ。 | 記事ごとに1-2、タイトルケース、feature.ymlに一致する必要があります。コンマ区切り |
| `feature-set` | 機能の検証用の親アプリケーション。 | feature.yml値と一致する必要があります |
| `role` | ターゲットオーディエンスの役割： ExLで「作成済み」と表示されます。 | `Admin`, `Architect`, `Data Architect`, `Data Engineer`, `Developer`, `Leader`, `User` |
| `level` | ユーザーエクスペリエンスレベル： ExLで「作成済み」と表示されます。 | `Beginner`、`Intermediate`、`Experienced` （タイトルケース） |
| `topic` | 検索/フィルタリング用のクロスプロダクトトピック。 | タイトルケース；topic.ymlに一致する必要があります；コンマ区切り |
| `type` | ガイド分類： | `Documentation` （既定値）、`Tutorial`、`Troubleshooting` |
| `last-substantial-update` | 「新機能」ウィジェットでコンテンツを表示します。 | 形式：`YYYY-MM-DD` |
| `hide` | すべての検索およびレコメンデーションからページを除外します。また、インデックスをnoに設定します。 | `yes`または`no` |
| `hidefromtoc` | 目次ナビゲーションから削除されますが、ページには直接リンク経由でアクセスできます。 | `yes`または`no` |
| `index` | ページを外部検索/サイトマップに表示するかどうかを制御します。 | `yes`/`no`または`y`/`n`、デフォルト：`no` （インデックス付き） |
| `recommendations` | 「この機能に関する詳細なヘルプ」ウィジェットの動作を制御します。 | `noDisplay` （ウィジェットの表示を禁止）、`noCatalog` （レコメンデーションプールから除外） |
| `internal` | ページをAdobeの内部専用としてマークします。 内部リンクのフラグ付けを防止します。 | `yes` |
| `short-description` | ExL ランディングページの詳細な説明。 省略した場合は`description`を使用します。 | 1文、最大20語 |
| `activity` | ページ使用状況の分類： | `understand`、`implement`、`troubleshoot` （小文字） |
| `sub-product` | 製品サブコンポーネント： 有効な列挙に関しては、ソリューションチームと連携してください。 | 小文字。例：`search`、`assets`、`sites` |
| `team` | 分析チームへの割り当て： | E.g. `TM` |
| `landing-page-name` | パンくずリストのランディングページへのリンク。 | E.g. `experience-manager` |
| `landing-page-breadcrumb-title` | ランディングページリンク用のパンくずテキスト。 | E.g. `AEM` |
| `auto-video-transcripts` | デフォルトでビデオトランスクリプトを有効にします。 | `true` |
| `badgeType` | コンテンツステータスのバッジ。 | Varies （例：`informative`、`positive`） |
| `badgePremium` | プレミアムバッジインジケーター： | Adobe バッジ仕様 |
| `badgeLabel` | バッジラベルテキスト。 | 短い文字列 |
| `source-git-url` | Source リポジトリ URL。 | 完全なGitHub URL |
| `cloud` | 記事レベルでのクラウドカテゴリの上書き。 | タイトルケース；cloud.ymlに一致する必要があります |

&#x200B;---

## TOC.md フィールド

| フィールド | 説明 | 備考 |
|-------|-------------|-------|
| `user-guide-title` | ExL パンくずリストとランディングページに表示されるガイド名。 | 目次ファイルに必要 |
| `breadcrumb-title` | user-guide-titleが長すぎる場合、パンくずリストのガイド名を短くします。 | オプション |
| `user-guide-description` | ExL ランディングページのガイド概要。 | 1文、最大20語まで推奨 |
| `product` | ガイドを読む。 単一の値のみ。 | product.ymlに一致する必要があります（有効な製品値を参照） |
| `mini-toc-levels` | 右ナビゲーションのミニ目次に表示される見出しレベルの数。 | 整数1～6、デフォルトは2 |
| `role` | ガイドのデフォルトのオーディエンス役割。 | 記事`role`と同じ値です。コンマ区切りです |
| `index` | ガイドにインデックスが付いているかどうか。 | `yes`/`no` |

&#x200B;---

## リポジトレベルのmetadata.md フィールド

| フィールド | 備考 |
|-------|-------|
| `cloud` | リポジトリ内のすべての記事のデフォルトクラウドカテゴリ |
| `solution` | すべての記事のデフォルトソリューション |
| `product` | 分析トラッキング用の既定の製品 |
| `type` | デフォルトのガイドタイプ |
| `doc-type` | デフォルトのドキュメントタイプ |
| `mini-toc-levels` | デフォルトのミニ目次レベル |
| `git-repo` | GitHub リポジトリ URL。「このページを編集」および「問題をログ」ボタンを有効にします。 |
| `index` | デフォルトのインデックス設定 |

&#x200B;---

## 有効なソリューション値（大文字と小文字を区別）

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

## 有効な製品値（`product` フィールドの場合 – 分析トラッキング）

完全なリストについては、システムプロンプトを参照してください。 キー値：
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

## 主要な検証ルール

1. コピーしたファイル内に同じUUIDを持つ`exl-id`を残さないでください。削除して、システムに新しいUUIDを割り当てさせます。
2. 空白/null `thumbnail`および`kt`は許容されます。これらはレガシーフィールドです。
3. `solution`値は、承認済みの列挙と完全に一致する必要があります。大文字と小文字を区別します。
4. `description`検証は、見つからないかnullの場合に失敗します。常に意味のある値を指定してください。
5. コロン、角括弧、または先頭の特殊文字が含まれている場合は、`title`個の値を引用符で囲みます。
6. 複数の`solution`値は、1つの文字列値内でコンマ区切りされます。
7. `product`は単一の値のみです（分析トラッキング用）。コンマ区切りの値は使用しないでください。
8. 新しい列挙値をリクエストするには、「コンテンツタグ付け」コンポーネントを使用してUGP JIRA チケットをファイルします。
