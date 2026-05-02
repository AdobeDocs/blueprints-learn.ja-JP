---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 7%

---
# ブループリント監査と推奨事項

この監査は、[評価のルーブリック ](rubric.md)を
[TOC.md](../help/blueprints/TOC.md) （76 ～ 133行目）の「アーキテクチャ図とブループリント」セクション
各ブループリントをユースケース **パターン**、アーキテクチャにするかどうかを推奨します
**図**、両方（**分割**）、または既存のパターンの&#x200B;**重複**&#x200B;としてフラグ付けされます。

これは監査のみです。コンテンツは移動されていません。 移行バックログ（バッチ A-D アクション）
提案がレビューされた後、別のフォローオンプランとして起草される。

## 概要

**監査済みドキュメントの合計数：** 43

| 推奨事項 | カウント | アクション |
| --- | --- | --- |
| パターン | 8 | 新しいユースケースパターンを作成します。元のパターンを図にトリミングします。 |
| 複製 | 9 | 既存のパターンは範囲をカバーし、図とクロスリンクにブループリントを簡素化します。 |
| Split | 2 | パターンコンテンツを抽出し、オリジナルをダイアグラムに減らし、両方をクロスリンクします。 |
| ダイアグラム | 16 | アーキテクチャ図は維持し、必要に応じてストーリーをトリミングします。 |
| ナビゲーション | 8 | セクションのランディングページ（overview.mdまたはリンクのみ）。移行後に再訪問します。 |

### コントロール母集団の較正

6 `experience-platform/`個のファイルすべてに対して、Pattern=0、Diagram=3→満場一致で&#x200B;**Diagram**が生成されました。
ルーブリックは校正されます。他のサブエリアの結果はスコアとして信頼できます。

### 新しいユースケースパターンカテゴリ：B2B アクティベーションとマーケティング

新しいカテゴリ `use-case-patterns/b2b/` （表示ラベル **B2B アクティベーションとマーケティング**、目次アンカー）
`{#b2b-patterns}`が提案されています）には、B2B固有のすべてのパターンが含まれます。 ラベルは既存の
[TOC.md](../help/blueprints/TOC.md)のアーキテクチャ図領域の「B2B アクティベーションとマーケティング」サブセクション、
2つのセクションの間に視覚的な対称性を与えます。

完全に入力されると、カテゴリには&#x200B;**7つのパターン**&#x200B;が含まれます。

| オリジン | アクション | ターゲットパス |
| --- | --- | --- |
| `use-case-patterns/audience-building-activation/b2b-audience-activation.md` | **既存のパターンを再配置** | `use-case-patterns/b2b/account-audience-activation.md` |
| `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` | **既存のパターンを再配置** | `use-case-patterns/b2b/buying-group-marketing.md` |
| `use-case-patterns/analysis/b2b-analytics.md` | **既存のパターンを再配置** | `use-case-patterns/b2b/account-analytics.md` |
| `b2b/b2b-journeys-with-marketo.md` | **新規オーサー** （監査パターン行） | `use-case-patterns/b2b/marketo-data-journeys.md` |
| `b2b/ajo-b2b-paid-media-controller.md` | **新規オーサー** （監査パターン行） | `use-case-patterns/b2b/paid-media-orchestration.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **新規オーサー** | `use-case-patterns/b2b/campaign-intake-and-creation.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **新規オーサー** | `use-case-patterns/b2b/campaign-review-and-approval.md` |

> **初期トランジション状態 – ライター調整ゲート。** 既存の「B2B アクティベーションとマーケティング」> [TOC.md](../help/blueprints/TOC.md) （95 ～ 106行目） **のarchitecture-diagrams エリアのサブセクションは変更されません> 移行中**。 各ブループリントの変換と既存のパターンの再配置には> コンテンツを移行する前に、所有ライターからサインオフします。 新しい`b2b/` ユースケースパターン> セクションは既存のブループリントセクションと共存しますが、移行はページごとに行われ、次は次のようになります。> 相互の関連付け：

転勤や新しいパターンがすべて着陸した場合：

- [TOC.md](../help/blueprints/TOC.md) `Use Case Patterns` セクションは次の値を取得します。 `B2B Activation & Marketing{#b2b-patterns}`
サブセクション（書き込み時にTBDを配置）。
- [use-case-patterns/overview.md](../help/blueprints/use-case-patterns/overview.md)はB2B カテゴリ テーブルを取得します。
- 再配置されたパターンは`audience-building-activation`から削除されます。
  `campaign-management-orchestration`および`analysis`の概要テーブル。古いURLは保持されます
[migration-redirects.csv](migration-redirects.csv)のリダイレクトを介して生き残っています。

### 重複の特定（9）

ブループリントスコープは、既存のユースケースパターンですでにカバーされています。 移行アクションは
**アーキテクチャ ダイアグラムを簡略化+ クロスリンク**。

| ブループリント | 既存パターン |
| --- | --- |
| `audience-activation/advertising-activation.md` | `use-case-patterns/audience-building-activation/audience-activation-to-destinations.md` |
| `audience-activation/segment-match.md` | `use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md` |
| `b2b/b2bactivation.md` | `use-case-patterns/audience-building-activation/b2b-audience-activation.md` |
| `b2b/b2b-buying-group-journeys.md` | `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` |
| `customer-journey-analytics/b2b-cja.md` | `use-case-patterns/analysis/b2b-analytics.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-journeys.md` | `use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-campaigns.md` | `use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md` |
| `customer-journeys/decision-management/decision-management-edge.md` | `use-case-patterns/personalization/offer-decisioning.md` |
| `customer-journeys/decision-management/decision-management-hub.md` | `use-case-patterns/personalization/offer-decisioning.md` |

> メモ：`decision-management-edge.md`と`decision-management-hub.md`は両方とも同じ場所にマップされます> 既存の`offer-decisioning.md` パターン。 両方のブループリントを単一の製品にまとめることを検討する> edge-vs-hub デプロイメントによる既存パターンの補強などをおこないます> バリエーション： ライターのレビュー用のフラグ。

### オーサリングするパターン（新規8件+ スプリットからの2件= 10件）

| Source blueprint | 提案されたカテゴリ | 提案されたパターンタイトル |
| --- | --- | --- |
| `audience-activation/customer-activity.md` | audience-building-activation | サポートとセールスのためのリアルタイムのプロファイル検索 |
| `audience-activation/data-science.md` | audience-building-activation | プロファイル強化のためのデータサイエンスモデル取得 |
| `audience-activation/real-time-lookup.md` | personalization | Web/Mobile PersonalizationのEdge プロファイルへのアクセス |
| `b2b/b2b-journeys-with-marketo.md` | **b2b** （新規） | Marketo Data IntegrationによるB2B アカウントジャーニー |
| `b2b/ajo-b2b-paid-media-controller.md` | **b2b** （新規） | ウォーターフォールのスプリットパスロジックによるB2B有料メディアオーケストレーション |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **b2b** （新規） | キャンペーンリクエスト受注と自動プログラム作成 |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **b2b** （新規） | キャンペーンアセットのレビューと承認のワークフロー |
| `customer-journeys/campaign-v8/campaign-v8-overview.md` | campaign-management-orchestration | Campaign v8 バッチオーケストレーションとトランザクションメッセージ |
| `audience-activation/rtcdp-target.md` *（分割）* | personalization | Adobe Targetによるリアルタイムのオーディエンス共有 |
| `customer-journeys/journey-optimizer/3rd-party-messaging.md` *（分割）* | campaign-management-orchestration | Journey Optimizerと3rd パーティのメッセージ統合 |

### 提案された新しいパターンカテゴリ

- **`b2b/`** （表示ラベル **B2B アクティベーションとマーケティング**） – 上記の専用セクションを参照してください。 を
Marketo + Workfront パターン （`intake-and-create`, `review-and-approve-blueprint`）がルーティングされます
`marketing-resource-management` カテゴリではなく、別のカテゴリを表すため、ここに
B2B マーケティング業務の実践。 新しいカテゴリは、合計7つのパターンを集計します：3再配置
ブループリントから新たに作成されたものが4つあります。

### 移行リダイレクト

この移行によって導入されたすべてのURLの変更により、行が規範的に追加されます
[`redirects.csv`](../redirects.csv) （リポジトリ ルートの形式：`source,dest`）。 確認済み
リダイレクトは、[migration-redirects.csv](migration-redirects.csv)でステージングされ、
各対応する移動が実際に発生するときの正規ファイル。

**確認済み（3件のエントリ、ステージング済み）:**&#x200B;既存のパターンが`b2b/`に再配置されました。 を参照
[migration-redirects.csv](migration-redirects.csv)。

**保留中 – ブループリントが&#x200B;*削除された場合に追加されました* （図に縮小された場合ではない）:**
パターン、分割、または重複行のブループリントが後で完全に削除された場合は、
正規パターン URLへのブループリント URL。 デフォルトの移行アプローチ（簡素化から図へ）
ブループリント URLは維持され、**はこれらのリダイレクトを**必要としません。 以下にリストされている
ブループリントが完全に廃止された場合の完全性：

```
# Pattern blueprints — if deleted, redirect to the new pattern URL
# (slugs are placeholders; finalize when each pattern is authored)
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/customer-activity → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/data-science → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/real-time-lookup → use-case-patterns/personalization-patterns/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-journeys-with-marketo → use-case-patterns/b2b-patterns/marketo-data-journeys
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/ajo-b2b-paid-media-controller → use-case-patterns/b2b-patterns/paid-media-orchestration
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/intake-and-create → use-case-patterns/b2b-patterns/campaign-intake-and-creation
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint → use-case-patterns/b2b-patterns/campaign-review-and-approval
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/campaign-v8/campaign-v8-overview → use-case-patterns/campaign-orchestration-patterns/<new-pattern-slug>

# Duplicate blueprints — if deleted, redirect to the existing pattern URL
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/advertising-activation → use-case-patterns/audience-building-activation/audience-activation-to-destinations
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/segment-match → use-case-patterns/audience-building-activation/audience-collaboration-segment-match
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2bactivation → use-case-patterns/b2b-patterns/account-audience-activation  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-buying-group-journeys → use-case-patterns/b2b-patterns/buying-group-marketing  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/b2b-cja → use-case-patterns/b2b-patterns/account-analytics  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-journeys → use-case-patterns/campaign-orchestration-patterns/event-triggered-messaging
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-campaigns → use-case-patterns/campaign-orchestration-patterns/batch-outbound-message-activation
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-edge → use-case-patterns/personalization-patterns/offer-decisioning
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-hub → use-case-patterns/personalization-patterns/offer-decisioning

# Optional one-off — if customer-journey-analytics/analysis.md is relocated to experience-platform/
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/analysis → architecture-diagrams/architecture-overview/analysis
```

上記のいずれかをアクティブなリダイレクト行に変換する場合は、コンマ区切りとしてフォーマットします `source,dest`
完全な`/en/docs/...` パス （サフィックス `.html`なし）を使用し、内の既存のパターンと一致します
[`redirects.csv`](../redirects.csv).

### リダイレクト作成ポリシー（耐久性のあるルール）

移行の手順ごとに、次のルールに従います。

1. **ファイルが移動または名前が変更されました** →、古いURLから新しいURLにリダイレクトを追加します。
2. **削除されたファイル** （ブループリントが置き換えられました。図は保持されていません）→削除されたURLから次のURLにリダイレクトを追加
正規の置換URL。
3. **ファイルが配置で簡略化されました** （URLは変更されていません）。リダイレクト→ありません。
4. **目次アンカーの名前が変更されました** （例：セクション見出しの変更）→の下の各ページのリダイレクトを追加
URLが変更されるので、このアンカーが表示されます。

### ライターに関するオープンな質問

1. **意思決定管理エッジとハブ** – 両方とも同じ既存のエッジにマップされます `offer-decisioning.md`
パターン： デプロイメントのバリエーションを含む単一の図に統合するか、別の図として扱います
両方が同じパターンにリンクするダイアグラム
2. **Journey Optimizer ジャーニーとイベントトリガーメッセージ** – 担当者がこの重複をフラグしました
不確実な分類。 ブループリントを削減する前に、スコープの整合性を確認します。
3. **`customer-journey-analytics/analysis.md`** — コンテンツは実際にはExperience Platformに関するものです
CJAではなくクエリサービスです。 `experience-platform/` フォルダーへの再配置を検討してください。 （1 リダイレクト
その場合は追加されます。[migration-redirects.csv](migration-redirects.csv)を参照してください。）
4. **Campaign v7 （非推奨）** – 非推奨の3つのv7 ファイルが図として分類されました/
ナビゲーション： 移行するか、そのまま残すか、目次から完全に削除するかを確認します。
5. **`customer-success-stories.md`** — リンクのみの参照ページ （`overview.md`ではありません）。
ナビゲーションとして分類されます。 確認または再分類。
6. **B2B セクション目次アンカー** — `{#b2b-patterns}`を提案しました。 その他のパターン サブセクションでは
   `-patterns`接尾辞（`{#personalization-patterns}`, `{#analysis-patterns}`,
   `{#campaign-orchestration-patterns}`). リダイレクトをオーサリングする前に、別のアンカーを確認するか、選択します。
7. **B2B セクションの配置（目次**） — `+ Use Case Patterns{#use-case-patterns}`に基づいて提案されました。
兄弟の順序（オーディエンスの構築とアクティベーション、Personalization、Campaign Management）
&amp; Orchestration, Analysis, B2B Activation &amp; Marketing, Conversational Experience）は
作家の呼び出し。
8. **オーナーライター調整** – 各ブループリントの変換と既存のパターンの再配置
コンテンツが移動する前に、ライターの承認が必要です。 監査テーブルはターゲットステートであり、
順序付け計画：順序付けは、調整の後に続く移行計画で行われます。

## 監査テーブル

| パス | title | 概要 | dominant_type | 推奨事項 | proposed_pattern_category | proposed_pattern_title | proposed_diagram_title | duplicate_of | pattern_score | diagram_score | メモ |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| help/blueprints/experience-platform/experience-cloud.md | Adobe Experience Cloud アーキテクチャ図 | Experience Cloudのアプリケーションとサービスが、AEPの基盤でどのように連携するかを示す、大規模なアーキテクチャ。 | ダイアグラム | ダイアグラム |  |  | Experience Cloud アーキテクチャの概要 |  | 0 | 3 | オーバーライド 3 （ビジネス目標なし）。 3つの補完的な図（マーケティングテクチャ、統合、企業状況）。 コントロール母集団：予想通り。 |
| help/blueprints/experience-platform/platform-applications.md | Adobe Experience Platformのアーキテクチャ図 | Experience Platformと他のExperience Cloudアプリケーションの関係を示すアーキテクチャ図。 | ダイアグラム | ダイアグラム |  |  | AEPとアプリケーションアーキテクチャ |  | 0 | 3 | 上書き3. 2つの概要/詳細図、実装ガイダンスなし。 統合へのクロスリンク – 学習ドキュメント。 コントロール母集団：予想通り。 |
| help/blueprints/experience-platform/platform-data-flow.md | Adobe Experience Platform データフローアーキテクチャ図 | Experience Platformとの間の取り込みパスと出力パスを示すデータフローアーキテクチャ図。 | ダイアグラム | ダイアグラム |  |  | AEPのデータフローアーキテクチャ |  | 0 | 3 | 上書き3. データ収集ドキュメントを参照した、単一のデータフロー図。 純粋なアーキテクチャ成果物： コントロール母集団：予想通り。 |
| help/blueprints/experience-platform/guardrails.md | Experience Platform およびアプリケーションガードレール | AEPおよびアプリケーションのシステムの制約、パフォーマンスへの期待、遅延に関するガードレール。 | ダイアグラム | ダイアグラム |  |  | AEPとアプリケーションのガードレールと遅延 |  | 0 | 3 | 上書き3. レイテンシ図と参照テーブル： アーキテクト指向（エッジ対ハブ）: ハウツーではなくドキュメントに関する制約を追加。 コントロール母集団：予想通り。 |
| help/blueprints/experience-platform/deployment/websdk.md | Experience Platform Web SDKとEdge Networkのアーキテクチャ図 | データ収集フローを示すweb SDKとEdge Networkのデプロイメントアーキテクチャ。 | ダイアグラム | ダイアグラム |  |  | Web SDKとEdge Networkのデプロイメント |  | 0 | 3 | 上書き3. 2つの図（フローとシーケンス）。 参照チュートリアルですが、ドキュメント内のハウツーはありません。 建築に焦点を当てる。 コントロール母集団：予想通り。 |
| help/blueprints/experience-platform/deployment/appsdk.md | アプリケーション固有の SDK デプロイメントアーキテクチャ図 | アプリケーション固有のSDK統合パスとデータ収集アーキテクチャ図。 | ダイアグラム | ダイアグラム |  |  | アプリケーションに特化したSDKの導入 |  | 0 | 3 | 上書き3. ストーリーを最小限に抑えた単一の配信図。 純粋なアーキテクチャ成果物： コントロール母集団：予想通り。 |
| help/blueprints/audience-activation/advertising-activation.md | Audience ActivationからソーシャルおよびAdvertisingの宛先 | ID設定と配信先の設定をおこない、RTCDPを介してFacebookとGoogleの広告ネットワークにオーディエンスをアクティベートできます。 | パターン | 複製 |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md | 4 | 1 | この範囲には既存のパターンが適用されます。 重複した上書き。 アクション：純粋な図とクロスリンクに簡素化します。 |
| help/blueprints/audience-activation/audience-manager.md | デバイスベース - Audience Managerによる匿名オーディエンスターゲティング | Audience ManagerまたはRTCDPを使用した、チャネルをまたいだデバイスベースのターゲティングによる匿名オーディエンスのアクティベーション。 | ダイアグラム | ダイアグラム |  |  | 匿名デバイスベースのオーディエンスターゲティング |  | 1 | 2 | 最小限のストーリー。 アーキテクチャ図が表示され、システム・トポロジが示されています。 ビジネス目標のフレーミングはありません。デプロイメント SDKとハブ/エッジの概念です。 |
| help/blueprints/audience-activation/customer-activity.md | サポートとセールスのシナリオのためのリアルタイムのプロファイルアクセス | プロファイル検索APIを使用して、サポート担当者や営業担当者がリアルタイムで顧客の状況を把握できます。 | パターン | パターン | audience-building-activation | サポートとセールスのためのリアルタイムのプロファイル検索 |  |  | 3 | 1 | ビジネス成果（エージェントコンテキスト）をフレーム化します。 前提条件チェックリストがあり、実装ステップが30行を超えています。 固有のユースケース：ハブプロファイルアクセス（エッジパーソナライゼーションではない）。 既存のパーソナライゼーションパターンとの違い： |
| help/blueprints/audience-activation/data-science.md | プロファイルエンリッチメントのためのカスタムデータサイエンスブループリント | マシンラーニングモデルのスコアをRTCDPに取り込み、パーソナライゼーションとセグメンテーションのためのプロファイルを強化。 | パターン | パターン | audience-building-activation | プロファイル強化のためのデータサイエンスモデル取得 |  |  | 3 | 1 | ビジネス成果をフレーム化（パーソナライゼーションのための強化）。 ユースケースと考慮事項があり、実装に関する考慮事項は30行を超えています。 メッセージやアクティベーションではなく、データサイエンスワークフローに集中する： |
| help/blueprints/audience-activation/enterprise-destinations.md | エンタープライズ宛先へのオーディエンスとプロファイルのアクティベーション | プロファイルやオーディエンスの変更を、クラウドストレージやエンタープライズアプリケーションにストリーミング配信し、セールス、サポート、分析に活用できます。 | ダイアグラム | ダイアグラム |  |  | オーディエンスとプロファイルのアクティベーション |  | 1 | 2 | ビジネス目標のフレーミングはない。 スパース実装ガイダンス： クラウドストレージ/エンタープライズアプリケーション向けのアーキテクチャダイアグラム + システムトポロジ。 視覚的に優勢： |
| help/blueprints/audience-activation/real-time-lookup.md | webおよびモバイルPersonalizationのリアルタイムEdgeプロファイルアクセス | エッジの統合プロファイルにミリ秒単位でアクセスし、リアルタイムのwebおよびモバイルのパーソナライゼーションを実現します。 | パターン | パターン | personalization | Web/Mobile PersonalizationのEdge プロファイルへのアクセス |  |  | 5 | 2 | 強力なビジネスフレーミング（低遅延パーソナライゼーション）: 2つの実装パターン（Web SDKとEdge API）。 広範な前提条件と手順（>30行）。 暗黙的なKPI （待ち時間、スループット）: |
| help/blueprints/audience-activation/rtcdp-target.md | Adobe Targetを使用した既知のCustomer Personalization | RTCDPでAdobe Targetのオーディエンスとプロファイルを共有し、既知の訪問者に対してwebとモバイルのパーソナライズを実現します。 | 混在 | Split | personalization | Adobe Targetによるリアルタイムのオーディエンス共有 | Target統合アーキテクチャ | help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md | 3 | 2 | 既存の既知の訪問者パターンと重複していますが、範囲が狭い（ターゲットのみ）。 3つの統合パターン。 アーキテクチャ図+ エッジの導入を考慮。 パターンコンテンツ+ダイアグラムは実質的な→分岐の両方です。 |
| help/blueprints/audience-activation/segment-match.md | Segment Match を使用した Audience Collaboration | プライバシー制御とのセグメントマッチにより、安全なパートナーオーディエンスのコラボレーションを実現。 | パターン | 複製 |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md | 4 | 1 | 既存のパターンがまさにそれをカバーしています。 重複した上書き。 図に保存する固有コンテンツ：詳細なRBAC/同意/ガバナンス設定とプログラマティック広告ワークフロー。 |
| help/blueprints/b2b/overview.md | B2B分析、アクティベーション、マーケティングのブループリント | B2B分析、オーディエンスのアクティベーション、購買グループ、Marketo、Workfrontのブループリントを示すナビゲーションページ。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | オーバーライド 1:overview.mdという名前のファイル。 移行から除外されました。 |
| help/blueprints/b2b/b2bactivation.md | B2B オーディエンスおよびプロファイルのアクティベーションブループリント | アカウントとプロファイルデータを使用して、web、電子メール、広告のチャネルをまたいでアカウントベースのB2B オーディエンスを活用できます。 | パターン | 複製 |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md | 3 | 1 | オーバーライド 2：同等のパターンが存在します。 ブループリントは、アーキテクチャに焦点を当てたサブセットです。 |
| help/blueprints/b2b/b2b-account-activation.md | Advertisingの宛先とファイルの宛先に対するB2B アカウントのアクティベーション | アカウントのオーディエンスの作成とアクティベーションを利用して、LinkedInやクラウドストレージの宛先を介してB2B アカウントをターゲティングできます。 | ダイアグラム | ダイアグラム |  |  | B2B Account Audience Activation |  | 1 | 2 | 最小限のビジネスフレームワーク、KPIなし、最小限のストーリー性。 アーキテクチャ図が存在します。LinkedIn/クラウドストレージのトポロジについて説明しました。 図として保存。 |
| help/blueprints/b2b/b2b-buying-group-journeys.md | 購買グループベースのマーケティングとジャーニー管理のブループリント | 定義された役割とソリューションへの関心を持つ購買グループにリードを絞り込むアカウントジャーニーを設計できます。 | パターン | 複製 |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md | 5 | 2 | オーバーライド 2：同等のパターンが存在します。 ブループリントには豊富なパターンコンテンツが含まれていますが、既存のパターンはより包括的です。 |
| help/blueprints/b2b/b2b-journeys-with-marketo.md | Adobe Marketo Data Blueprintを活用したB2Bジャーニー | MarketoデータをJourney Optimizer B2B editionにデプロイすることで、購買グループのジャーニーとアカウントエンゲージメントを調整できます。 | パターン | パターン | b2b | Marketo Data IntegrationによるB2B アカウントジャーニー |  |  | 4 | 1 | 強力なビジネスフレームワーク： リストされているKPI、複数の実装オプション、広範な考慮事項（>30行）。 Marketo データ統合の深さ（XDM設定、ID ステッチ、フィールドブロッキング）により、既存のパターンと差別化されています。 新しいb2b/カテゴリへのルート。 |
| help/blueprints/b2b/ajo-b2b-paid-media-controller.md | AJO B2B - Account Journey Orchestration - Paid Media Controller | ウォーターフォールロジックを使用してB2B有料メディアキャンペーンを調整し、アカウントをキャンペーンに割り当て、配信先にアクティベートします。 | パターン | パターン | b2b | ウォーターフォールのスプリットパスロジックによるB2B有料メディアオーケストレーション |  |  | 4 | 2 | 強力なビジネスフレームワーク： 明示的なKPI、複数の実装オプション、前提条件、30行を超えるストーリー。 既存の購買グループのパターンとは異なる（ナーチャリングではなく、有料メディアの優先順位付けに焦点を当てる）。 新しいb2b/カテゴリへのルート。 |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md | Marketo Engage と Workfront 統合ブループリントの概要 | Marketo EngageおよびWorkfront with Fusionを使用したキャンペーン計画から実行オートメーションの概要。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | オーバーライド 1:overview.mdという名前のファイル。 移行から除外されました。 |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md | 取り込みと作成のブループリント | WorkfrontフォームとMarketo Engageのプログラムテンプレートにより、B2B マーケティングキャンペーンのリクエスト受付から制作までを自動化できます。 | パターン | パターン | b2b | キャンペーンリクエスト受注と自動プログラム作成 |  |  | 4 | 1 | キャンペーンベロシティに即した強力なビジネスフレームワーク。 暗黙的なKPI （エラー/手戻り作業の削減）、ワークフローのステップが30行を超える、準備状況チェックリスト。 新しいb2b/カテゴリーへのルート（Marketo+Workfrontの運用は主にB2B）。 |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md | レビューと承認のブループリント | Fusionの自動化機能を使用して、Workfrontの校正ワークフローと承認ワークフローをMarketo Engageのメールアセットと統合できます。 | パターン | パターン | b2b | キャンペーンアセットのレビューと承認のワークフロー |  |  | 3 | 2 | コンプライアンスと正確性に基づく強力なビジネスフレーミング、暗黙的なKPI （承認ベロシティ）、30行を超えるストーリー、ワークフロー計画セクション。 新しいb2b/カテゴリへのルート。 |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md | 顧客の成功事例 | MarketoとWorkfrontの統合結果を紹介するユーザー事例やウェビナーへのリンクです。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | 最小限のコンテンツ（6つのハイパーリンク）。 ビジネスの枠組み、KPI、アーキテクチャ、ストーリーなど必要ありません。 ナビゲーションとして扱われます。 筆者は確認する必要があります。 |
| help/blueprints/customer-journey-analytics/overview.md | Customer Journey Analyticsの設計図 | さまざまなチャネルからの顧客データと行動を統合、分析し、ジャーニーベースのビューを作成できます。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | オーバーライド 1: overview.md. 目次スタイルのランディングページ： 移行から除外されました。 |
| help/blueprints/customer-journey-analytics/b2b-cja.md | B2B Customer Journey Analyticsの設計図 | アカウントを主要なデータモデルとして使用している、B2B企業向けのアカウントベースのCJAレポートおよび分析。 | パターン | 複製 |  |  |  | help/blueprints/use-case-patterns/analysis/b2b-analytics.md | 4 | 2 | 上書き2：同等のパターンは、CJA B2B editionを使用したB2B アカウントレベルの分析をカバーしています。 アクション：図、クロスリンクに簡素化します。 |
| help/blueprints/customer-journey-analytics/cja-rtcdp.md | Adobe Customer Journey AnalyticsとAdobe Real-Time CDPの連携 | ターゲティングとパーソナライゼーションのために、CJAからRTCDPにオーディエンスを作成して公開します。 | ダイアグラム | ダイアグラム |  |  | CJAとRTCDPのオーディエンス公開の統合 |  | 1 | 3 | 強力なアーキテクチャ重視（システム間の統合、導入の形態）: 最小限のストーリー。 一意のコンテンツ：CJA オーディエンスの公開待ち時間のガードレール。 |
| help/blueprints/customer-journey-analytics/cja-ajo.md | Customer Journey AnalyticsとJourney Optimizer blueprint | Adobe CJAでAJOの配信データとインタラクションデータを分析し、CJAオーディエンスをAJOに公開します。 | ダイアグラム | ダイアグラム |  |  | CJAとAJOの連携と分析 |  | 1 | 3 | 強力なアーキテクチャ重視： 最小限のストーリー。 一意のコンテンツ：双方向のCJAとAJOのデータ共有パターン |
| help/blueprints/customer-journey-analytics/analysis.md | データ分析とインテリジェンスブループリント | Experience Platform Query Serviceを使用して、データレイクデータを分析。 | ダイアグラム | ダイアグラム |  |  | Experience Platform Query ServiceとBI ツールの統合 |  | 1 | 3 | CJA固有ではなく、クエリサービスを対象としています。 CJA フォルダーに配置が間違っている可能性があります。experience-platform/への再配置を検討してください。 強力なアーキテクトオーディエンス（PostgreSQL、BI ツール）: |
| help/blueprints/customer-journeys/overview.md | 顧客ジャーニーのブループリント | イベント主導のジャーニーと、チャネルをまたいでブランド主導のキャンペーンをサポートする最新のマーケティングプラットフォーム。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | オーバーライド 1: overview.md. ジャーニーのサブカテゴリの目次。Journey OptimizerとCampaignの配置について説明します。 |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md | Journey Optimizer Blueprints | イベント主導の1:1 プロファイルオーケストレーションと、チャネルをまたいだオーディエンスベースのブランドコミュニケーション。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | オーバーライド 1: overview.md. ユースケースのタブと統合パターンを備えたランディングページ。 |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md | Journey Optimizer - トリガーメッセージとAdobe Experience Platformのブループリント | 顧客の行動にもとづいてパーソナライズされたマルチステップのエクスペリエンスを提供する、リアルタイムのイベント駆動型ワークフロー。 | パターン | 複製 |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md | 4 | 2 | 2を警告で上書き：エージェントが重複している可能性が高いが不確かであるとフラグ付けされます。 削減する前にスコープの調整を検証する： アーキテクチャに関する考慮事項は、プロファイルの鮮度、セグメントの選定タイミングなど、独自のものであり、図に保存する価値があります。 |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md | Journey Optimizer - キャンペーンオーケストレーション | 電子メール、SMS、プッシュ通知、ダイレクトメールなど、アウトバウンドチャネルをまたいでスケジュールされたオーディエンスベースのマルチステップコミュニケーション。 | パターン | 複製 |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md | 3 | 2 | オーバーライド 2：同等のパターン 複数のアーキテクチャ図。図として保持します。 一意のコンテンツ：リレーショナルデータベース/オーディエンスポータル/スキニープロファイルアーキテクチャの詳細。 |
| help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md | Journey Optimizer - サードパーティメッセージングのブループリント | Journey Optimizerとサードパーティのメッセージングシステムの連携を示し、コミュニケーションのオーケストレーションを実現します。 | 混在 | Split | campaign-management-orchestration | Journey Optimizerと3rd パーティのメッセージ統合 | 3rd パーティのメッセージングアーキテクチャ |  | 2 | 2 | Tied scores → Split. ダイアグラム（システム間トポロジ）とパターンコンテンツ（実装ステップ、統合制約：ベアラー認証、静的IPなし、レート制限）。 両方を保存する価値があります。 |
| help/blueprints/customer-journeys/decision-management/decision-management-overview.md | 意思決定管理のブループリント | 一元化されたオファーライブラリと意思決定エンジンを利用して、カスタマージャーニー全体でパーソナライズされたオファーを提供できます。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | オーバーライド 1: overview.md. 意思決定管理のコンポーネントとエッジとハブのデプロイメントのアプローチについて説明します。 |
| help/blueprints/customer-journeys/decision-management/decision-management-edge.md | エッジでの意思決定管理のブループリント | エッジネットワークで秒単位の遅延を発生させ、リアルタイムでweb エクスペリエンスとモバイルエクスペリエンスにパーソナライズされたオファーを提供します。 | 混在 | 複製 |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | 上書き2：オファー決定支援へのマップ。 Edgeのデプロイメントのバリエーション – ハブの設計図を単一のデプロイメントオプション図に統合することを検討する。 |
| help/blueprints/customer-journeys/decision-management/decision-management-hub.md | ハブでの意思決定管理のブループリント | キオスク、エージェント支援エクスペリエンス、アウトバウンド配信など、チャネル全体でパーソナライズされたオファーを提供します。 | 混在 | 複製 |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | 上書き2：オファー決定支援へのマップ。 ハブのデプロイメントのバリエーション - Edge Blueprintを単一のデプロイメントオプション図に統合することを検討する。 |
| help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md | Campaign v8 Blueprint, Campaign &amp; Platform | ETL、セグメンテーション、トランザクションメッセージなどの機能を備えた、次世代のバッチキャンペーン管理プラットフォーム。 | パターン | パターン | campaign-management-orchestration | Campaign v8 バッチオーケストレーションとトランザクションメッセージ | Campaign v8 アーキテクチャのデプロイメントモデル |  | 4 | 3 | 個別の技術的アプローチ（AJOではなく、Campaign v8 ネイティブ）。 複数のアーキテクチャ図、ビジネスフレーミング、ガードレールに含まれるKPI （20M msg/hr バッチ、1M/hr リアルタイム）。 既存のパターンカタログに同等のものはありません。 メモ：スコアも分割として認定されます – パターンを提案しますが、ライターは図を保持したくなるかもしれません。 |
| help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md | Real-Time CDP と Adobe Campaign v8 の統合パターン | パーソナライズされた会話のために、RTCDPオーディエンスとCampaign v8とのプロファイル統合を紹介します。 | ダイアグラム | ダイアグラム |  |  | RTCDP - Campaign v8 オーディエンスとプロファイル交換 |  | 1 | 2 | スタンドアロンのユースケースではなく、統合コネクタの設計図。 図+簡単な前提条件/ガードレール。 アーキテクト指向： |
| help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md | Journey Optimizer と Adobe Campaign v8 ブループリント | 1:1 エクスペリエンスのCampaign v8 トランザクションメッセージを使用したAJO オーケストレーションを示します。 | ダイアグラム | ダイアグラム |  |  | Journey Optimizer - Campaign v8 トランザクションメッセージングの統合 |  | 1 | 2 | 統合コネクタ： 図+実装ステップ+技術的な制約（4,000 msg/5min スロットル、イベント開始のみ）。 AJOおよびCampaign v8 パターンへのクロスリンク。 |
| help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md | Campaign v7 ブループリント | 非推奨：バッチベースのメッセージ、オンボーディング、リマーケティング、ダイレクトメール、シンプルなトランザクションメッセージ。 | ナビゲーション | ナビゲーション |  |  |  |  |  |  | 非推奨の製品（v8へのfrontmatter リンク）。 最小限のコンテンツ（アーキテクチャ図のみ）: 移行しないでください。 |
| help/blueprints/customer-journeys/campaign-v7/rtcdp-and-campaign-v7.md | Real-Time CDPとCampaign v7およびCampaign Standardの統合パターン | Adobe RTCDPとAdobe Real-Time CDPの連携をCampaign v7/Standardで紹介し、パーソナライズされた会話を実現。 | ダイアグラム | ダイアグラム |  |  | RTCDP - Campaign v7/Standard オーディエンスおよびプロファイル交換 |  | 1 | 2 | 非推奨（廃止予定）: 統合コネクタ： 図+包括的な実装ステップ。 新しいパターンには移行しないでください。そのまま残します。 |
| help/blueprints/customer-journeys/campaign-v7/ajo-and-campaign-v7.md | Journey Optimizer と Adobe Campaign v7 ブループリント | 1:1 エクスペリエンスのCampaign v7 トランザクションメッセージを使用したAJO オーケストレーションを示します。 | ダイアグラム | ダイアグラム |  |  | Journey Optimizer - Campaign v7 トランザクションメッセージングの統合 |  | 1 | 2 | 非推奨（廃止予定）: 統合コネクタ： 図+実装ステップ+制約。 移行しないでください。そのまま残します。 |
