---
name: architecture-diagram-page-builder
description: Adobe Experience Platform ブループリントリポジトリ用の新しいアーキテクチャ図ページの作成をガイドします。 このスキルは、新しいトップレベルのアーキテクチャ図、統合アーキテクチャページ、またはアプリケーションアーキテクチャの概要を追加する際に使用します。 アーキテクチャページでは、トップレベルのAEPとアプリケーションアーキテクチャおよび主要な統合ポイントについて説明します。詳細なユースケースは含まれません（ユースケースのpattern-builderに属するもの）。 ワークフロー全体を処理します。ページ情報の収集、マークダウン ファイルの生成、正しいトピックフォルダーへの配置、TOC.mdの更新です。
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 2%

---


# アーキテクチャ図ページビルダー

このスキルでは、Adobe Experience Platform ブループリントリポジトリ用の新しいアーキテクチャ図ページの作成について説明します。 アーキテクチャ図ページでは、AEPとAdobeのアプリケーションがどのように連携するのか、それらのアプリケーション間の主要なデータフロー、ソリューションを設計する際に作成者が認識する必要のある統合ポイントなど、視覚的に重要な情報を提供します。

## 範囲

アーキテクチャ図ページは、**に焦点を当てた参照スタイルのページ**&#x200B;です。通常、マークダウンは40～100行で、次の内容を含みます。

- 各図の目的を簡潔に説明した1つ以上のアーキテクチャ図
- アーキテクチャがサポートするユースケースパターンへのリンク（アーキテクチャページはそのコンテンツを複製しません）
- 図に示す主要なデータフローと統合ポイントのリスト
- アプリケーションドメインの詳細については、Experience Leagueのリンクを参照してください

詳細なユースケースのコンテンツを提供する場所は&#x200B;**not**&#x200B;です。 KPI、ビジネス目標、戦術的なユースケースの例、ファンクションチェーン、ペルソナのストーリーは、代わりに`use-case-pattern-builder` スキルで生成されたユースケースパターンページに属しています。 完全なガードレールについては、`references/scope-guardrails.md`を参照してください。

## 開始する前に読む必要があります

テンプレートとルールについては、次の参照ファイルを参照してください。

- `references/diagram-template.md` - プレースホルダー値を含んだ完全なマークダウンテンプレート
- `references/toc-placement.md` — TOC.mdのサブセクション マッピング テーブルとエントリ形式
- `references/scope-guardrails.md` — アーキテクチャページに属するものとユースケースパターンページに属するもののルール

## フェーズ 1：情報収集

ファイルを生成する前に、必要なすべての情報を収集するようユーザーにインタビューします。 すべての必要な項目が提供されるか、明示的に延期されるまで、コンテンツ生成に進まないでください。

### 必要な情報

1. **ページタイトル** – 人間が読み取れるタイトル（例：`Adobe Journey Optimizer architecture diagrams`）。

2. **トピックフォルダー** — ページが存在する場所。 ダイアグラムのプライマリドメインに基づいて正確に1つを選択します。
   - `experience-platform/` — トップレベルのAEP、マルチアプリ、またはプラットフォームレベルの図
   - `customer-journeys/` — AJO、キャンペーン、ジャーニーオーケストレーション
   - `customer-journey-analytics/` — CJA アーキテクチャ
   - `audience-activation/` — RTCDP、オーディエンス、プロファイルのアクティベーション
   - `b2b/` — B2B固有のアーキテクチャ

3. **Filename** — ページタイトルから派生したケバブケース （例：`Journey Optimizer architecture` -> `journey-optimizer-architecture.md`）。 ユーザーに確認します。

4. **ページの目的** – 図の全体を表す1～2個の文章。 `description` フロントマターフィールドと冒頭の段落に使用されます。

5. **Adobe ソリューション** — ページの中心となるAdobe製品のコンマ区切りリスト。 `solution` フロントマターフィールドに使用されます。 例：`Experience Platform, Journey Optimizer, Customer Journey Analytics`。

6. **図** — 1つ以上の図。 各図について、次の情報を収集します。
   - **画像ファイル名** （例：`aep_data_flow.svg`） SVGが優先されます。PNGでも可能です。
   - **Section title** – 図のH2見出しになります（例：`Data flow diagram`、`Detailed architecture diagram`）。
   - **目的の説明** – 図が示す内容を説明する1～2個の文章。
   - **代替テキスト** – 短いアクセス可能な説明。

7. **サポートされているユースケースパターン** – このアーキテクチャで有効にする2 ～ 5個の既存パターン。

   **最初に候補者を推薦します。** パターンの入力を求める前に、`/help/blueprints/use-case-patterns/`をスキャンし、ページタイトル、ページの目的、上記で収集したAdobe ソリューションに基づいて、3～6個の可能性のある一致を提案します。 推奨事項ごとに、次の項目を提示します。
   - パターン名（リンクされたパスを含む）
   - なぜこのアーキテクチャに合うのか、一文で示す

   候補を番号付きショートリストとして表示し、（a）任意の候補を受け入れる、（b）任意の候補を却下する、（c）見逃したパターンを追加するようにユーザーに依頼します。 実際のファイルを指す提案のみを生成します。提案する前に確認するには手袋/読み取りします。 パターン名をハルシネーションしないでください。

   受け入れられるパターンごとに、カテゴリとファイル名をキャプチャします。 生成する前に、各ファイルが`/help/blueprints/use-case-patterns/{category}/{pattern-file}.md`に存在することを検証します。

8. **プライマリデータフロー/統合ポイント** – 図に表示されている主要なフローと統合の境界を説明する3 ～ 7個の箇条書き（例：`Real-time event ingestion from Web SDK to Edge Network`、`Profile synchronization between Experience Platform Hub and Edge`）。

9. **Experience League リンク** – 関連するExperience League ドキュメントへの3 ～ 6個のリンクを使用して、さらに詳しく読むことができます。 それぞれ`https://experienceleague.adobe.com/`で始まる必要があります。

   **最初に候補者を推薦します。** Adobeのソリューションとページの目的に基づいて、Experience Leagueに関する4～8の妥当な記事（例：各名前付きソリューションの標準的なランディングページや概要ページ、主要な統合ガイド、デプロイメント参照）を提案します。 推奨事項ごとに、次の項目を提示します。
   - 記事タイトル
   - URL
   - なぜそれがページに合うのか、1行の根拠

   URLを実際に取得していない限り、候補に&#x200B;**未確認**&#x200B;のマークを付けます。生成されたファイルにアクセスする前に、ユーザーが確認するか置換する必要があります。 ユーザーに、（a）同意するよう依頼し、（b）既存の検証済みのURLにURLを置き換え、（c）独自のURLを追加します。 見たことのないURLを作成してはいけません。不明な場合は、記事のタイトルを提案し、ユーザーがURLを入力できるようにします。

### オプション

- **関連コンテンツのコールアウト** — ページの上部付近に`>[!MORELIKETHIS]` ブロックとしてレンダリングされた単一リンク。 Experience Leagueに兄弟の統合または設定ガイドがある場合に役立ちます。

ユーザーが必要なアイテムをすべて提供しない場合は、続行する前に不足しているアイテムを要求してください。 図、パターン、またはリンクを作成しないでください。

## フェーズ 2：範囲チェック

生成する前に、ユーザーのダイアグラムの説明、データフローの箇条書き、下書きの表現を再度読みます。 `references/scope-guardrails.md`からガードレールを適用します。

計画されたコンテンツに次のいずれかが表示される場合は、そのセクションをユースケースパターンページにリダイレクトするようにユーザーに警告し、提案します（またはアーキテクチャページからトリミングします）。

- KPIまたは測定式
- ビジネス目標やビジネス影響のストーリー
- 戦術的なユースケース例（特定のパーソナライゼーションシナリオ、キャンペーンの例など）
- 関数チェーン （`A > B > C > D` スタイル）
- ペルソナ主導のstorytelling

計画されたコンテンツがアーキテクチャページスコープ（トップレベルのアーキテクチャ、システムデータフロー、統合ポイント、デプロイメントトポロジ、エッジとハブ）内に留まる場合は、ユーザーに確認し、フェーズ 3に進みます。

## フェーズ 3：コンテンツの生成

次の場所でページを生成：

```
/help/blueprints/{topic-folder}/{kebab-filename}.md
```

ソース テンプレートとして`references/diagram-template.md`を使用します。 すべてのプレースホルダー値を、収集した情報で入力します。 生成されるファイルには、次のものが含まれている必要があります。

1. **YAML frontmatter** — `title`、`description`、`solution`のみ。
   - **含まない`exl-id`** – 公開パイプラインが自動的に割り当てます。
   - **含めない** `product_v2`、`feature_v2`、`role_v2`、`topic_v2`、`TQID`、`kt`または`thumbnail` – これも自動入力されます。

2. **H1 heading** — ページタイトル。

3. **段落を開く** — ページ目的の入力から派生した1 ～ 2個の文章。

4. **オプションの`>[!MORELIKETHIS]` ブロック** — ユーザーが関連コンテンツのリンクを提供した場合のみ。

5. **図ごとに1つのH2 セクション** — ユーザーが提供した順序で。 各セクションには、次の内容が含まれます。
   - H2見出しとしてのセクションタイトル
   - 1-2図の目的を説明する文
   - 標準規則を使用して埋め込まれた画像：

     ```html
     <img src="assets/{filename}" alt="{Alt Text}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />
     ```

6. **`## Use case patterns supported`** – 箇条書きリスト。 各弾丸：

   ```
   - [{Pattern name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) -- {1-line note on why this architecture enables the pattern}
   ```

7. **`## Primary data flows and integration points`** — 3 ～ 7個のフロー/統合項目の箇条書きリスト。

8. **`## Further reading`** — Experience League リンクの箇条書きリスト：

   ```
   - [{Article title}]({Experience League URL})
   ```

本文と箇条書きのAdobe製品名には、既存のページの規則に一致する`[!DNL ...]`構文を使用します。

## フェーズ 4：相互参照の更新

**`/help/blueprints/TOC.md`**&#x200B;を更新して、新しいページをナビゲーションに追加します。 これは、更新する唯一の相互参照ページです。

完全なサブセクション マッピング テーブルとルールの`references/toc-placement.md`を読み取ります。 概要：

| トピックフォルダー | 目次サブセクション |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}` （アーキテクチャの概要のサブセクション） |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

エントリ形式（4 スペースインデント + `+`）:

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

ユーザーが別の位置を指定しない限り、新しいエントリを一致するサブセクションの最後の項目として追加します。 4 スペースのインデントを正確に保持 – 目次解析はそれに依存します。

## フェーズ 5：検証

すべてのファイルを作成して更新したら、次の点を確認し、エラーがあればユーザーに報告します。

1. **画像アセットの存在** – 各図について、`/help/blueprints/{topic-folder}/assets/{filename}`が存在することを確認します。 **見つからない場合は**&#x200B;に警告します。ブロックしないでください（ユーザーはダイアグラム設計と並行してオーサリングしている可能性があります）。 見つからないファイルの明確なリストを表示して、ユーザーが何を追加すべきかを把握できるようにします。

2. **ユースケースパターンリンク** — ファイル内のすべてのパターンリンクは、`/help/blueprints/use-case-patterns/`の下にある既存のマークダウンファイルを指しています。 `Read`またはグロブを使用して、各ターゲットが存在することを確認します。

3. **Experience League リンク** — `## Further reading` セクションのすべてのURLが`https://experienceleague.adobe.com/`で始まることをスポットチェックします。

4. **目次エントリの配置** – 新しいエントリは正しいサブセクション内にあり、4 スペースのインデントを使用し、パスは生成されたファイルの場所と正確に一致します。

5. **ファイル名** — ページのファイル名はkebab-caseで、TOC.mdで参照されているパスと一致します。

6. **Frontmatter completeness** — ページには`title`、`description`、`solution`が含まれます。 **not**&#x200B;には、`exl-id`、`product_v2`、`feature_v2`、`role_v2`、`topic_v2`、`TQID`、`kt`または`thumbnail`を含める必要があります。

タスクの完了を検討する前に、検証の問題を修正します。

## 備考

- Adobeの製品名には、既存のページの規則に従って、本文と箇条書きで常に`[!DNL ...]`構文を使用します。
- アーキテクチャ図は通常、SVG（鮮明さと拡大・縮小に適しています）ですが、ラスターソースのアートワークではPNGを使用できます。
- 埋め込まれたインラインスタイル文字列（`border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;`）と`class="modal-image"`が必要です。これらは、Experience League モーダル ズーム操作を有効にします。`<img>`
- ユーザーがまだ存在しない新しいトピックフォルダーのページを作成する場合は、TOC.mdに`+ Architecture Diagrams and Blueprints{#architecture-diagrams}`の下に新しいトップレベルサブセクションが必要であることを警告します。 ユーザーの明示的な承認とは別のステップとして処理する必要があります。
- アーキテクチャ図で&#x200B;*単一ユースケースのエンドツーエンド* （KPI、ビジネス目標、機能チェーン）を広く文書化している場合、ユーザーを`use-case-pattern-builder`にリダイレクトします。これはアーキテクチャページではありません。
