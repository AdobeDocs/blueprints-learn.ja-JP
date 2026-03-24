---
title: B2B 分析
description: クロスチャネルのカスタマージャーニー分析にB2B アカウントレベルの情報を含める方法について説明します。
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7528'
ht-degree: 1%

---

# B2B分析

このガイドでは、[!DNL Customer Journey Analytics] （[!DNL CJA]）B2B editionと[!DNL Real-Time Customer Data Platform] （[!DNL RT-CDP]）B2B editionを使用したB2B アカウントレベル分析の包括的な実装リファレンスを提供します。 Adobe Marketo Engageは、B2Bのアカウントレベルの情報をクロスチャネルのカスタマージャーニー分析に組み込む必要がある、ソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

フラットなアカウント構造から、複雑なグローバルなアカウント階層に至るまで、アカウント中心の分析に対する実行可能なすべてのアプローチをカバーし、各オプションを選択するタイミングに関するガイダンスを提供します。 このプランは、B2B データ接続、アカウントデータビューの設定、ワークスペース分析、ダッシュボード公開に対応しています。

B2B Analyticsは、アカウントベースの接続、B2B固有のコンテナ （アカウント、グローバルアカウント、商談、購買グループ）、アカウントレベルのレポートにより、標準の[!DNL CJA]機能を拡張します。 この機能により、アカウントレベルでのマーケティングとセールスのエンゲージメントを分析し、機会の進捗状況を追跡して、購買グループの完全性を測定し、拡張されたB2B セールスサイクル全体のマーケティング接点に売上を関連付けることができます。

## ユースケースの概要

B2B企業が直面する分析の課題は、顧客が個人ではなく、複数の関係者、購買グループ、機会で構成されるアカウントであるということです。 標準的な個人ベースの分析では、「最もエンゲージ率が高いアカウントは？」、「購買グループの完成度は？」、「商談の進行を促進するマーケティング接点はどれか？」といった質問に答えることはできません。

B2B Analyticsでは、[!DNL CJA] B2B editionを活用して、個人レベルの行動データと、アカウント、商談、購買グループのディメンションを組み合わせた、アカウント中心の分析ビューを作成することで、この問題に対処します。[!DNL RT-CDP] B2B editionは、分析レイヤーに情報を提供する、基盤となるアカウントプロファイルの統合とB2B ID解決を提供します。 これらのソリューションを組み合わせることで、企業はアカウントレベルでクロスチャネルジャーニー分析を構築し、マーケティングエンゲージメントとパイプラインの進行を関連付け、マーケティング部門と営業部門の両方に実用的なインサイトを提供することができます。

ターゲットオーディエンスには、B2B マーケティングオペレーションチーム、デマンドジェネレーションリーダー、レベニューオペレーションアナリスト、セールスリーダーが含まれ、アカウントレベルのエンゲージメントとパイプラインの健全性を可視化する必要があります。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### 分析とレポートの改善

統合ダッシュボードとセルフサービスツールを通じてレポート機能を強化し、より迅速で実用的なマーケティングインサイトを獲得できます。 B2B分析を活用すれば、複数のソースからのアカウントレベルのエンゲージメントデータを単一の分析環境に統合し、マーケティングプログラムがパイプラインと収益にどのような影響を与えるのかをクロスチャネルで把握できます。

**KPI:**&#x200B;効率、生産性

[分析とレポートの改善について詳しく見る](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### データにもとづく意思決定

セルフサービス型の分析、リアルタイムの顧客インサイト、AIを活用した予測により、戦略を策定できます。 アカウントレベルの分析により、マーケティング部門と営業部門は、アカウントの優先順位付け、エンゲージメント戦略の最適化、パイプラインの機会の調整に必要なデータを取得できます。

**KPI:**&#x200B;効率、生産性

[データにもとづく意思決定について詳しく見る](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### リードのクオリフィケーションとコンバージョンを向上

スコアリング、育成、パーソナライズされたフォローアップにより、リードの品質を向上させ、パイプラインの進行を加速させることができます。 CJA B2B editionには、B2Bのセールスサイクルに特化して設計された、13 ヶ月間のアカウントルックバックウィンドウが用意されています。これにより、カスタマージャーニー全体で正確なマルチタッチアトリビューションを実現します。

**KPI:**&#x200B;効率、増分収益

[リードのクオリフィケーションとコンバージョンの改善について詳しく見る](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## 戦術的なユースケース

次のシナリオは、このパターンを実際にどのように適用できるかを示しています。

- **アカウントエンゲージメントスコアリング分析** — web、電子メール、イベント、コンテンツのインタラクションをまたいだエンゲージメントを集計してアカウントを測定およびランク付けし、セールスのフォローアップのために購買意欲の高いアカウントを特定します
- **購買グループの完全性トラッキング** – アカウントをまたいで購買グループの構成を分析し、役割のカバーされていない部分を特定し、不完全な購買グループに対するリード獲得を優先します
- **商談パイプラインの相関関係** — マーケティングエンゲージメントデータを商談ステージの進行と相関させ、パイプラインの進行を促進するキャンペーンとタッチポイントを把握します
- **マルチタッチ B2B アトリビューション** — 13か月間のルックバックウィンドウを含むアトリビューションモデルを適用して、ファーストタッチから成約に至るまでのB2B購買ジャーニー全体のマーケティング顧客接点に貢献度を割り当てます
- **アカウントジャーニーマッピング** – 最初の認知から機会の創出、成約に至るまでのクロスチャネルのアカウントジャーニーを可視化し、共通のパスと摩擦ポイントを特定します
- **キャンペーンがパイプラインに与える影響** – 特定のキャンペーンがアカウントパイプラインの作成、機会の増加、収益の生成にどのように影響しているかを測定します
- **購買グループのエンゲージメントの進捗状況** – 購買グループのエンゲージメントスコアが時間の経過とともにどのように変化するかを追跡し、エンゲージメントのしきい値と商談の結果を関連付けます
- **アカウントベースのコンテンツパフォーマンス** – 特定のアカウントセグメント、業界、購買グループの役割に響くコンテンツアセットとトピックを分析します
- **営業部門とマーケティング部門の連携ダッシュボード** — マーケティング部門と営業部門の両方が、アカウントエンゲージメント、パイプラインの健全性、収益アトリビューションに関する統合的なビューを提供する共有ダッシュボードを構築します
- **アクティブ化のためのアカウントセグメンテーション** — アカウントレベルの分析に基づいてB2B セグメントを作成し（例えば、「オープンな機会のないエンゲージメントの高いアカウント」）、下流のアクティブ化のために公開します

## 主要業績評価指標

次のKPIは、このユースケースパターンの成功を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| アカウントエンゲージメントスコア | アカウント内のあらゆるコンタクトをまたいでエンゲージメント指標を集計 | アカウントレベルでのweb訪問、メールでのやり取り、イベントへの参加、コンテンツのダウンロードを組み合わせた計算指標 |
| 購買グループの完全性 | 購買グループ内で入力された必要な役割の割合 | 購入グループごとに必要な役割の合計数に対する、入力済みの役割の割合（時間の経過に伴い追跡） |
| マーケティングの影響を受けたパイプライン | マーケティング活動によって影響を受けたパイプラインの売上 | 関連するアカウントの連絡先がアトリビューションウィンドウ内にマーケティングのタッチポイントを持つ商談値 |
| アカウントから商談へのコンバージョン率 | 適格な機会を生み出すエンゲージメントアカウントの割合 | 定義された期間のエンゲージメント済みアカウントの合計で割った商談を持つアカウント |
| 平均取引サイクル長 | マーケティングへの最初の接触から成約までの時間 | 最初のタッチポイントが商談の成約に至るまでの平均期間 |
| マーケティングアトリビューション収益 | マーケティング接点による売上 | マーケティングタッチによる商談成立からの収益（アトリビューションモデル別） |
| アカウントへのリーチと浸透度 | ターゲットアカウントあたりの連絡先のエンゲージ数 | 既知のコンタクトの合計数に対し、アカウントあたりのマーケティングインタラクションを示す一意のコンタクト |
| 購買担当者別のコンテンツエンゲージメント | 購買グループの役割ごとにセグメント化されたエンゲージメント指標 | 購買グループ内のペルソナや役割ごとに分類された、ページビュー、ダウンロード、滞在時間 |

## ユースケースパターン

**B2B分析**

クロスチャネルのカスタマージャーニー分析に、B2Bのアカウントレベルの情報を含めましょう。

**関数チェーン：** B2B Data Connection > Account Data View Configuration > Workspace Analysis > Dashboard Publishing

## アプリケーション

このユースケースパターンを実装するには、次のアプリケーションを使用します。

- **[!DNL Customer Journey Analytics]B2B edition** — アカウントベースの接続、B2B固有のデータビューコンテナ、アカウントレベルのワークスペース分析、購買グループ分析、商談分析、B2B セグメンテーション、およびB2B アトリビューションを、拡張されたルックバックウィンドウで提供します
- **[!DNL Real-Time CDP]B2B edition** — アカウントプロファイルの統合、B2B ID解決、B2B スキーマクラス （アカウント、商談、購買グループ）、B2B エンゲージメントデータの取り込み用の[!DNL Marketo Engage]統合など、B2B データ基盤を提供します

## 基本関数

このユースケースパターンでは、次の基本機能を使用する必要があります。 各機能について、ステータスは、通常それが必要か、事前設定が想定されているか、適用できないかを示します。

| 基本関数 | ステータス | 整えておく必要があるもの | Experience League リファレンス |
| --- | --- | --- | --- |
| 管理とガバナンス | 必須 | [!DNL CJA] B2B editionと[!DNL RT-CDP] B2B editionの使用権限で設定されたサンドボックス。 [!DNL CJA]とB2B データモデルへのアクセス権を持つデータエンジニア、アナリスト、マーケティングオペレーションユーザー向けにプロビジョニングされた役割。 | [&#x200B; サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home) |
| データモデリングと準備 | 必須 | B2B クラスを使用して設定されたB2B XDM スキーマ：XDM ビジネスアカウント、XDM ビジネスオポチュニティ、XDM ビジネスアカウント人物との関係、XDM ビジネスオポチュニティ人物との関係、およびXDM ビジネスマーケティングリストメンバー。 アカウント属性、商談ステージ、購買グループの役割のフィールドグループを定義する必要があります。 プロファイル用に作成および有効化されたデータセット。 | [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)、[B2B edition スキーマ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| データソースと収集 | 必須 | B2B データソースは、通常、[!DNL Marketo Engage] ソースコネクタまたは[!DNL Salesforce] CRM ソースコネクタを介して接続されます。 アカウントレコード、オポチュニティレコード、個人とアカウントの関係、行動エンゲージメントイベントは、Adobe AEPのデータセットに取り込む必要があります。[!DNL Web SDK] または[!DNL Marketo]統合は、アカウントの関連付けを使用して行動イベントをキャプチャする必要があります。 | [&#x200B; ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)、[Marketo Engage コネクタ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| IDとプロファイル設定 | 必須 | 個人とアカウントの関係を解決するために設定された、B2B ID解決。 アカウント ID、人物ID （[!DNL Marketo] リード IDまたはCRM連絡先ID）、クロスデバイス ID （ECID、電子メール）をリンクする必要があります。 ID グラフは、B2B データモデルに固有の、多対多の人物とアカウントのマッピングをサポートする必要があります。 | [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)、[B2B ID解決](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| オーディエンスの定義とセグメント化 | 同じ位置に仮定 | B2B セグメントが[!DNL CJA]からAEPに公開され、アクティブ化される場合は、アカウントレベルのオーディエンス定義を使用できます。 分析のみのユースケースの場合、これは厳密な前提条件ではありませんが、セグメントベースの分析に推奨されます。 | [&#x200B; セグメント化サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## サポート機能

次の機能は、このユースケースパターンを強化しますが、コア実行には必要ありません。

| 補助機能 | ステータス | なぜそれが重要なのか | Experience League リファレンス |
| --- | --- | --- | --- |
| 計算属性/派生属性作成 | 推奨 | アカウントプロファイルの計算属性（エンゲージメントスコアの合計、最後のアクティビティからの日数、商談数など）は、アカウントレベルの分析に使用できる[!DNL CJA]の分析分析ディメンションを強化します。 | [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| データライフサイクル管理 | 推奨 | B2B データセット、特に[!DNL Marketo Engage]からの行動イベントデータは、急速に成長する可能性があります。 データセットの有効期限ポリシーは、ストレージの管理や、データ保持要件へのコンプライアンスの確保に役立ちます。 | [高度なデータライフサイクル管理](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| データ使用のラベル付けと適用 | 推奨 | B2B データには、多くの場合、機密性の高いビジネス情報（契約上の価値、競合他社のインテリジェンス）が含まれています。 データ使用ラベルとガバナンスポリシーにより、分析ワークフローやアクティベーションワークフローをまたいで、このデータを適切に使用できます。 | [&#x200B; データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| 監視と可観測性 | 推奨 | B2B ソースコネクタ （[!DNL Marketo]、[!DNL Salesforce]）では、取り込みの正常性を監視する必要があります。 [!DNL CJA]の接続の正常性の監視により、分析のデータの鮮度が確保されます。 取り込み失敗のアラートルールは、古いダッシュボードを防ぎます。 | [&#x200B; オブザーバビリティ インサイトの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| レポートと分析 | 含まれる | このパターンはそれ自体が分析パターンです。 この機能は、レポート機能と分析機能を提供するコア機能チェーンに組み込まれています。 | [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## アプリケーション関数

この計画では、アプリケーション機能カタログから次の機能を実行します。 関数は、番号付きのステップではなく実装フェーズにマッピングされます。

### [!DNL Customer Journey Analytics] B2B edition

| 関数 | 導入フェーズ | 説明 |
| --- | --- | --- |
| アカウントベースの接続 | フェーズ 1:B2B データ接続 | 組織レベルの分析のプライマリ IDとしてアカウントまたはグローバルアカウントを使用して接続を設定します |
| B2B データビューの設定 | フェーズ 2：アカウントデータビューの設定 | B2B固有のコンテナ（アカウント、グローバルアカウント、機会、購買グループ）を、標準の個人、セッション、イベントコンテナとともにデータビューを定義します |
| アカウントレベルのWorkspace分析 | フェーズ 3:Workspace Analysis | アカウントレベルのディメンション、指標、B2B コンテナを使用して、フリーフォームの分析を構築し、組織レベルのジャーニーインサイトを実現できます |
| 購買グループ分析 | フェーズ 3:Workspace Analysis | 購買グループの構成、エンゲージメント、購買決定プロセスの進行を分析できます |
| 機会の分析 | フェーズ 3:Workspace Analysis | Sales funnelのステージを通じた商談の進行を追跡し、マーケティングエンゲージメントデータと相関関係を持つ |
| B2B セグメンテーション | フェーズ 3:Workspace Analysis | B2B コンテナを使用してセグメントを作成し、アカウントレベルの分析をフィルタリング |
| B2B アトリビューション | フェーズ 3:Workspace Analysis | B2B セールスサイクル分析のために、13 ヶ月間のアカウントルックバックウィンドウを延長したアトリビューションモデルを適用する |
| 計算指標の作成 | フェーズ 3:Workspace Analysis | アカウントのエンゲージメント率、購買グループの完全性、パイプラインへの影響など、B2B KPIの計算指標を定義します |
| ダッシュボードとスコアカードの公開 | フェーズ 4：ダッシュボード公開 | マーケティングおよびセールス担当者向けの、ダッシュボードとモバイルスコアカードを作成して共有できます |
| オーディエンスの公開 | フェーズ 4：ダッシュボード公開 | [!DNL CJA]定義されたアカウントベースのオーディエンスをAEPに公開して、ダウンストリームでアクティベートする |

### [!DNL Customer Journey Analytics] – 標準関数

| 関数 | 導入フェーズ | 説明 |
| --- | --- | --- |
| データ接続 | フェーズ 1:B2B データ接続 | クロスチャネル分析のためにAEP B2B データセットを[!DNL CJA]接続にバインドする |
| データビュー設定 | フェーズ 2：アカウントデータビューの設定 | B2B データビュー内で標準的なディメンション、指標、アトリビューション、永続性の設定を行うことができます |
| Workspace Analysis | フェーズ 3:Workspace Analysis | テーブル、フォールアウト、フロー、コホート、アトリビューションの各ビジュアライゼーションを利用して、フリーフォーム分析を構築できます |
| ガイド付き分析 | フェーズ 3:Workspace Analysis | アカウントレベルでfunnel、トレンド、リテンションに関するガイド付きワークフローを活用 |

### [!DNL Real-Time CDP] B2B edition

| 関数 | 導入フェーズ | 説明 |
| --- | --- | --- |
| アカウントプロファイルの統合 | 前提条件（F2/F4） | 専用のXDM B2B スキーマクラスを使用して、クロスソースのB2B データを統合アカウントプロファイルに統合できます |
| B2B ID解決 | 前提条件（F4） | マルチレベルのアカウント階層と多対多のマッピングをサポートして、個人とアカウントの関係を解決します |
| [!DNL Marketo Engage]統合 | 前提条件（F3） | ネイティブのB2B ソースコネクタを使用して、[!DNL Marketo Engage]から行動エンゲージメントデータとアカウント/リードレコードを取り込みます |

## 前提条件

実装を開始する前に、次の項目を配置する必要があります。

- [ ] [!DNL CJA] B2B edition ライセンスがアクティブで、組織にプロビジョニングされています
- [ ] [!DNL RT-CDP] B2B edition ライセンスは、B2B スキーマとアカウントプロファイルが設定された状態でアクティブです
- [ ] B2B XDM スキーマが定義されています（アカウント、商談、アカウント人物の関係、商談人物の関係、マーケティングリストのメンバー）
- [ ] [!DNL Marketo Engage]および/またはCRM ソースコネクタが設定され、データをアクティブに取り込んでいます
- [ アカウントレベルの行動イベントデータ （web訪問、メールでのやり取り、フォーム送信）が、アカウントの関連付けを行ってAEPに流れ込んでいます]
- [ ]個の個人とアカウントの関係がID グラフで確立されます
- [ ]少なくとも30日間の過去B2B エンゲージメント データを有意義な分析に利用できます
- [ ]人の関係者が購買グループの役割の定義とソリューションの興味マッピングに同意しました
- [ ] [!DNL CJA] ユーザーアカウントは、B2B edition機能に適した製品プロファイルでプロビジョニングされます
- [ ]件のターゲット KPIとレポート要件が、マーケティング部門と営業部門のリーダーによって定義されました

## 実装オプション

次の節では、このユースケースパターンを実装するためのさまざまなアプローチについて説明します。

### オプション A：アカウント中心の分析

**アカウントのレンズを通じて、すべてのエンゲージメントとパイプラインのデータを分析する組織に最適：**&#x200B;組織。 このアプローチでは、アカウントコンテナを主要な分析単位として使用し、アカウントが購入ジャーニーをどのように進んでいるのかをトップダウンで把握できます。

**仕組み：**

アカウントをプライマリ IDとして使用して[!DNL CJA] B2B接続を設定します。 あらゆる行動イベント、機会、購買グループのデータを、アカウントレベルにロールアップできます。 データビューでは、アカウントを最上位のコンテナとして使用し、その中に人物、セッション、イベントがネストされています。 これにより、「価格ページにアクセスしたアカウント数と、30日以内に商談を創出したアカウント数」などの分析が可能になります。

アカウント中心の分析は、アカウントが購買単位であるB2B企業に最も自然なビューを提供します。 業界、企業規模、アカウント層、アカウントオーナーなどのディメンションを使用して、エンゲージメントパターンとパイプライン指標を分析できます。 アトリビューションは、長いB2B販売サイクルに対応する13 ヶ月のルックバックウィンドウを利用して、アカウントレベルで適用されます。

**重要な考慮事項：**

- ID グラフにクリーンなアカウントと個人のマッピングが必要
- すべての個人レベルのイベントは、アカウントに起因するものでなければなりません
- アカウントに関連付けられない匿名web トラフィックは、アカウントレベルの分析には表示されません

**利点：**

- 購買ジャーニー全体をリアルタイムで把握
- B2Bの売上がどのように発生するのかに一致する、アカウントベースのアトリビューションが可能です
- アカウント内のネストされたコンテナとして、購買グループと商談分析をサポート
- 分析とアカウントベースドマーケティング（ABM）戦略の連携

**制限：**

- 堅牢な個人とアカウントのID解決が必要
- 匿名または一致しないエンゲージメントデータは分析から除外されます
- 人を中心に据えた分析よりも複雑な設定が必要

**Experience League:**

- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [B2B edition スキーマ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)

### オプション B：グローバルなアカウント中心の分析

**親会社が複数の子会社アカウントを持つ複雑なアカウント階層を持つ大規模組織に最適：**。 このアプローチでは、グローバルアカウントをプライマリ識別子として使用し、すべての子アカウントアクティビティを親組織レベルにロールアップします。

**仕組み：**

アカウントではなくプライマリ IDとしてグローバルアカウントを使用する[!DNL CJA] B2B接続を設定します。 これにより、親組織の下にあるすべての子会社アカウントからエンゲージメントデータが集計されます。 例えば、「Acme Corp」が地域の子会社「Acme EMEA」および「Acme APAC」を持っている場合、グローバルアカウント接続は、3つのエンティティのすべてのエンゲージメントを単一の分析的ビューに統合します。

データビューには、トップレベルコンテナとしてグローバルアカウントが含まれ、ネストされたコンテナとしてアカウント、人物、セッション、イベントが含まれます。 これにより、同じワークスペースプロジェクト内のグローバルおよび子会社のアカウントレベルの両方で分析が可能になります。 アトリビューションのルックバックウィンドウは、グローバルアカウントレベルで適用され、企業階層全体のあらゆるタッチポイントをキャプチャします。

**重要な考慮事項：**

- B2B データモデルで定義された親子関係を持つアカウント階層データが必要です
- グローバルアカウント IDは、すべてのアカウントレコードで入力され、正確である必要があります
- 子アカウントは、親に正しくマッピングする必要があります

**利点：**

- 複雑なエンタープライズアカウント構造を一元的に可視化
- 単一のエンタープライズ顧客が複数のアカウントレコードを持つ場合に、断片化された分析を防止します
- 単一のグローバルアカウント内の地域子会社の比較が可能
- エンタープライズレベルのパイプラインと売上レポートをサポート

**制限：**

- 多くの企業では、正確なアカウント階層データが必要であり、その維持に苦慮しています
- グローバルレベルでのみ表示すると、子会社レベルのパターンが不明瞭になる可能性があります
- 階層関係を確立および維持するための追加のデータモデリング作業

**Experience League:**

- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### オプション C：ハイブリッド型の個人とアカウント分析

**個人ベースの分析からアカウントベースの分析に移行する組織、または個人レベルとアカウントレベルの両方のビューを必要とする組織に最適です。** このアプローチでは、同じ接続から、1つの人中心と1つのアカウント中心の2つのデータビューを作成します。

**仕組み：**

すべてのB2B データセット （イベント、アカウント、商談、購買グループ、個人とアカウントの関係）を含む単一の[!DNL CJA] B2B接続を設定します。 次に、2つのデータビューを作成します。1つはプライマリコンテナとしてPersonを使用し（標準[!DNL CJA]と同様）、もう1つはプライマリコンテナとしてAccountを使用します。 アナリストは、質問に応じてデータビューを切り替えることができます。

個人を中心としたデータビューは、従来の個人レベルのジャーニー分析（例：「商談になるリードのコンバージョンパスは何か？」）を提供し、アカウントを中心としたデータビューは、組織レベルの分析（例：「エンゲージメントからパイプラインへのコンバージョン率が最も高いアカウントはどれか？」）を提供します。 どちらのビューも同じ基礎データを使用するため、一貫性が確保されます。

**重要な考慮事項：**

- ディメンションと指標の設定が異なる可能性がある2つのデータビューが必要
- アナリストは、各ビューを使用するタイミングに関するトレーニングを必要としている
- 計算指標は、データビューごとに個別に作成する必要がある場合があります

**利点：**

- 個人レベルとアカウントレベルの両方で、データを柔軟に分析
- 個人レベルの分析に慣れたチームが容易に導入できる方法
- 個人レベルとアカウントレベルの指標の比較が可能
- リードベースとアカウントベースの両方のマーケティング戦略をサポート

**制限：**

- 維持と同期を維持するための2つのデータビュー
- アナリストがどのビューを使用すべきかについて混乱が生じる可能性がある
- 計算された指標とフィルターは、ビュー間での重複が必要な場合があります

**Experience League:**

- [データビューの作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [データビューの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

### オプションの比較

| 条件 | オプション A：アカウント中心 | オプション B：グローバルなアカウント中心 | オプション C：ハイブリッド人物+ アカウント |
| --- | --- | --- | --- |
| 主な用途 | フラットなアカウント構造を持つ標準的なB2B | 親子階層を持つ企業 | 移行中の組織またはデュアルニーズ |
| 複雑 | 中 | 高 | Medium – 高 |
| 必要データ構成 | アカウントと人物のマッピング | アカウント階層+ マッピング | アカウントと人物のマッピング |
| アトリビューション範囲 | アカウントレベル（13か月間のルックバック） | グローバルアカウントレベル（13か月間のルックバック） | 個人レベルとアカウントレベルの両方 |
| 匿名データ | アカウントビューから除外 | グローバル表示から除外 | 個人ビューに含まれる、アカウントビューから除外される |
| 要件定義 | [!DNL RT-CDP] B2B edition、[!DNL CJA] B2B edition | [!DNL RT-CDP] B2B edition、[!DNL CJA] B2B edition、階層データ | [!DNL RT-CDP] B2B edition、[!DNL CJA] B2B edition |
| メンテナンス作業 | 単一のデータ表示 | 単一のデータ表示 | ふたつのデータビュー |

### 適切なオプションの選択

- **組織がフラットなアカウント構造（親子階層なし）を持ち、ABM戦略が個々のアカウントレベルで機能し、アカウントレベルの分析への最もシンプルなパスが必要な場合は、オプション A**&#x200B;を選択します。
- **ターゲットアカウントが地域または部門の子会社アカウントを持つ大企業で、企業の親レベルでの統合レポートが必要な場合は、オプション B**&#x200B;を選択します。 このオプションを使用するには、高品質のアカウント階層データが必要です。
- **リード ベースからアカウント ベースのマーケティングに移行する場合、アナリストは個人レベルのfunnel分析とアカウント レベルのエンゲージメント分析の両方を必要とするか、B2BとB2Cの両方のビジネスラインを組み合わせて使用する必要があります。C** オプションを選択します。

## 実装フェーズ

推奨される実装シーケンスの概要を、次のフェーズで説明します。

### フェーズ 1:B2B データ接続

**アプリケーション関数：** [!DNL CJA] B2B: アカウントベースの接続、[!DNL CJA]: データ接続

AEP B2B データセットを[!DNL CJA]にバインドする[!DNL CJA]接続を設定して分析を行います。 この接続は、どのデータセットが[!DNL CJA]に流れ込むか、プライマリ識別子の種類（アカウントまたはグローバルアカウント）、履歴データとストリーミングデータがどのように取り込まれるかを定義します。 接続は、その後のすべての分析の基盤となります。

#### 決定：プライマリID タイプ

接続でアカウント IDまたはグローバルアカウント IDをプライマリ IDとして使用するかどうかを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| アカウント ID | フラットアカウント構造、親子階層なし | 容易な設定：各アカウントを個別に分析 最も一般的な選択肢は、SMBに焦点を当てたB2Bです。 |
| グローバルアカウント ID | 子会社階層を持つ企業アカウント | 階層データが必要です。親のすべての子会社を集計します。 企業向けABM プログラムに最適。 |

#### 決定：データセットの選択とタイプ指定

B2B データセットに含めるべき内容と、各データセットの型付け方法を決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| イベントデータセット（行動） | 常に含める | web インタラクション、メールイベント、フォーム送信、コンテンツのダウンロード。 タイムスタンプフィールドが必要です。 これらはエンゲージメントのシグナルです。 |
| アカウントレコードデータセット（プロファイル） | 常に含める | 業界、サイズ、階層、所有者などのアカウント属性。 アカウント分析のためのディメンションのコンテキストを提供します。 |
| 商談データセット （ルックアップ/プロファイル） | パイプライン分析用に含める | オポチュニティステージ、値、クローズ日。 パイプラインと収益アトリビューション分析に必要です。 |
| 購買グループデータセット（ルックアップ/プロファイル） | 購買グループの分析用に含める | 購買グループの役割、エンゲージメントスコア、完全性。 購買グループの構成分析に必要。 |
| 個人とアカウントの関係データセット （参照） | 常に含める | 人物をアカウントにマッピングします。 個人レベルのイベントをアカウントレベルの分析に関連付ける上で非常に重要です。 |
| キャンペーン/プログラムデータセット（ルックアップ） | アトリビューション用に含める | キャンペーンのメタデータ、プログラムの種類、チャネル。 キャンペーンの影響分析を有効にします。 |

#### 決定：バックフィル範囲

接続にインポートする履歴データの量を決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 既存のすべてのデータ | B2Bの販売サイクルは長く（6～18か月）、包括的な履歴が必要です | B2B向け製品。 大規模なデータセットのバックフィルには数日かかることもありますが、包括的なアトリビューションデータを提供します。 |
| カスタム日付範囲（過去2～3年） | データ品質は一定の範囲を超えて低下する | 完全性とデータ品質のバランス。 CRM データに過去の不整合がある場合に一般的です。 |
| バックフィルなし | テストまたは開発のみ | 新しいデータのみが流れ込みます。 実稼動B2B分析には適していません。 |

#### B2B データ接続の設定

**UI ナビゲーション：** [!DNL Customer Journey Analytics] >接続>新しい接続を作成

主要な設定の詳細：

- B2B データセットを含むAEP サンドボックスを選択します
- キャパシティプランニングの1日の平均イベント数の設定
- 各データセットを追加し、タイプ（イベント、ルックアップ、プロファイル）を指定します
- B2B接続にアカウント IDまたはグローバルアカウント IDを使用するように人物ID フィールドを設定します
- ほぼリアルタイムの更新を必要とするデータセットのストリーミングを可能にします
- 履歴バックフィルの「既存のすべてのデータのインポート」を有効にする

**オプションが異なる場所：**

**オプション A （アカウント中心）の場合：**
プライマリ IDをアカウント IDに設定します。 アカウントレコード、商談、購買グループ、人物/アカウントの関係データセットを追加できます。 クロスデータセット参加用のアカウント ID フィールドを使用して、個人レベルのイベントデータセットを設定します。

**オプション B （グローバル アカウント中心）の場合：**
プライマリ識別子をグローバルアカウント IDに設定します。 アカウント階層データにグローバルアカウント ID フィールドが含まれていることを確認します。 すべてのデータセットは、適切なロールアップのためにグローバルアカウント IDを含めるか、または結合できる必要があります。

**オプション C （ハイブリッド）の場合：**
あらゆるB2B データセットに単一の接続を構築できます。 アカウント IDをプライマリ IDとして使用します。 人物を中心としたビューは、同じ接続で別のデータビュー設定を使用してフェーズ 2で作成されます。

**Experience League ドキュメント：**

- [接続の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [接続の作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [接続の管理](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)
- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### フェーズ 2: アカウントデータビューの設定

**アプリケーション関数：** [!DNL CJA] B2B: B2B データビュー設定、[!DNL CJA]: データビュー設定

接続データを分析でどのように表示するかを定義するデータビューを設定します。 B2B分析の場合、これには、B2B固有のコンテナ（アカウント、商談、購買グループ）の設定、B2B スキーマフィールドのディメンションおよび指標へのマッピング、B2Bに適したルックバックウィンドウを使用したアトリビューションモデルの設定、B2B ビジネスロジックの派生フィールドの作成が含まれます。

#### 決定：コンテナ設定

どのB2B コンテナを有効にし、どのように名前を付けるかを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| アカウント +人物+ セッション + イベント | 購買グループや商談分析を使用しない標準的なB2B | 最もシンプルなB2B コンテナ階層： アカウントは最上位のコンテナです。 |
| アカウント +商談+人物+ セッション + イベント | パイプラインと収益の分析が必要 | 商談をコンテナレベルとして追加し、商談スコープの分析を可能にします。 |
| アカウント+購買グループ+商談+人物+セッション+イベント | 購買グループの構成を含む完全なB2B分析 | 最も包括的なものです。 B2B データモデルのあらゆるレベルでの分析が可能です。 |
| グローバルアカウント + アカウント +人物+ セッション + イベント | グローバルアカウント階層分析 | アカウントの上の最上位のコンテナとしてグローバル アカウントを追加します。 |

#### 決定：B2B指標のアトリビューションモデル

コンバージョン指標のデフォルトにするアトリビューションモデルを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| リニアアトリビューション（13か月間のルックバック） | B2B ジャーニーのあらゆる顧客接点に平等に貢献度を割り当てる | マーケティング活動の全体像を把握するのに最適です。 B2B マーケティングの出発点。 |
| U字型アトリビューション（13 ヶ月間のルックバック） | ファーストタッチとラストタッチを重視 | リード創出と商談コンバージョンの瞬間をハイライト表示。 需要創出分析の一般的な手法。 |
| 時間減衰（13か月間のルックバック） | より多くの貢献度を割り当てるべき最近の顧客接点 | エンゲージメントの最新性が、営業部門の準備状況に関する重要なシグナルである場合に最適です。 |
| ラストタッチ | コンバージョン前の最終接点をシンプルにレポート | 早い段階のマーケティングは理解しやすいが、過小評価されている。 クイック運用レポートにのみ使用します。 |

#### 決定：B2Bのセッション定義

B2B エンゲージメントのセッションを定義する方法を決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 30分タイムアウト（デフォルト） | 標準のweb分析セッション動作 | web エンゲージメント分析のための標準。 長いコンテンツ消費セッションをフラグメント化する可能性があります。 |
| 拡張タイムアウト（60 ～ 120分） | B2B利用者は、より長いリサーチセッションに参加する | 一般的に、B2B バイヤーは、技術的なコンテンツ、価格設定、ドキュメントのレビューに多くの時間を費やしています。 |
| イベントベースの新しいセッション | 特定のイベントは、常に新しいセッションを開始する必要があります | キャンペーンのクリックスルーやデモリクエストを常に新しい分析セッションで開始する必要がある場合に使用します。 |

#### アカウントデータビューの設定

**UI ナビゲーション：** [!DNL Customer Journey Analytics] > データビュー/新しいデータビューの作成

主要な設定の詳細：

- フェーズ 1で作成された接続を選択
- 組織に適したタイムゾーンとカレンダータイプを設定します
- コンテナの名前をB2B関連の用語（アカウント/エンゲージメント/タッチポイントなど）に変更します。
- B2B スキーマフィールドをディメンションにマッピングする：アカウント名、アカウント ID、業界、企業規模、アカウント層、アカウント所有者、商談ステージ、商談値、購買グループの役割、ソリューションへの関心
- エンゲージメント指標のマッピング：イベント（オカレンス）、人物、セッション、ページビュー、フォーム送信、メール開封、メールクリック
- 主要ディメンションの永続性を設定します（例えば、アカウント業界はアカウントレベルで保持されます）
- コンバージョン指標のデフォルトとして、13か月のルックバックを使用してアトリビューションを線形に設定します
- マーケティングチャネルの分類、エンゲージメントスコアリング層、商談ステージのグループ化のための派生フィールドを作成します

**オプションが異なる場所：**

**オプション A （アカウント中心）の場合：**
アカウントを最上位コンテナとして使用して、単一のデータビューを設定します。 パイプラインと購買グループの分析が必要な場合は、商談と購買グループのコンテナを含めます。

**オプション B （グローバル アカウント中心）の場合：**
トップレベルコンテナとしてグローバルアカウントを設定します。 アカウントをサブコンテナとして含めて、グローバル分析と子会社分析の両方を有効にします。

**オプション C （ハイブリッド）の場合：**
同じ接続から2つのデータビューを作成します。 データビュー1は、プライマリコンテナとして人物を使用します（標準[!DNL CJA]動作）。 データビュー2では、B2B コンテナを含むプライマリコンテナとしてアカウントを使用します。 該当する場合は、両方のビューに同じ指標をマッピングします。

**Experience League ドキュメント：**

- [データビューの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [データビューの作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [コンポーネント設定の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [永続性の設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [アトリビューション設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [派生フィールド](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [セッション設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

### フェーズ 3:Workspace分析

**アプリケーション関数：** [!DNL CJA] B2B: アカウントレベルのWorkspace Analysis、購買グループ Analysis、商談分析、B2B セグメンテーション、B2B アトリビューション、[!DNL CJA]: Workspace Analysis、計算指標の作成、ガイド付き分析

KPIで定義された分析的インサイトを提供するワークスペースプロジェクトを構築します。 この段階では、B2B ディメンションと指標を含むフリーフォームテーブルの作成、B2BKPIの計算指標の作成、B2Bに特化したビジュアライゼーション（アカウントレベルのフロー、商談funnel、購買グループのエンゲージメント）の設定、B2B コンテナを使用したフィルター/セグメントの作成、B2B アトリビューションモデルの適用が含まれます。

#### 決定：分析ワークスペース構造

ワークスペースプロジェクトの整理方法を決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| 複数のパネルを持つ単一の包括的なプロジェクト | 小規模なチームでは、あらゆる関係者が同じレポートを閲覧 | 保守が容易： パネルを使用して、トピック（エンゲージメント、パイプライン、アトリビューション）を分類します。 1 プロジェクトにつき最大40枚のパネル。 |
| オーディエンス別の複数の焦点を絞ったプロジェクト | 関係者によって、必要なビューは異なります | マーケティング部門はエンゲージメントとアトリビューションを把握。 セールスがパイプラインやアカウントの健全性を取得。 オペレーションはデータ品質を確保し、 より多くのメンテナンスを、よりターゲットを絞って。 |
| ガイド付き分析機能によるテンプレートベースのプロジェクト | 専門家でないユーザー向けのセルフサービス分析 | Funnelとトレンドビューにガイド付き分析を使用すると。 反復可能な分析用にテンプレートとして保存。 幅広い導入に最適。 |

#### 決定：B2B計算指標

B2BのKPIに必要な計算指標を決定する。

| 指標 | 数式 | 作成するタイミング |
| --- | --- | --- |
| アカウントエンゲージメント率 | （アカウントイベントの合計数/アカウントの合計数） | Always — コア B2B指標 |
| 購買グループの完全性% | （入力済みの役割/必要な役割） * 100 | 購買グループ分析がスコープ内の場合 |
| アカウントから商談へのコンバージョン率 | 機会/エンゲージメントアカウントを持つアカウント | パイプライン分析が必要な場合 |
| パイプラインの影響% | 影響を受けたパイプラインの値/パイプラインの合計値 | マーケティングアトリビューションが必要な場合 |
| コンタクトあたりの平均エンゲージメント | イベント/アカウントごとのユニーク人物 | アカウント浸透分析が必要な場合 |
| 役割別のコンテンツエンゲージメント | 購買グループの役割でフィルタリングされたイベント | B2B向けコンテンツ最適化 |

#### 決定：B2B フィルター/セグメントスコープ

どのコンテナレベルのフィルターを作成するかを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| アカウントレベルのフィルター | 条件に一致するアカウント（例：エンタープライズアカウント、特定の業界）を対象とした分析 | 対象アカウントのすべてのイベントが含まれます。 B2Bでは一般的です。 |
| オポチュニティレベルのフィルター | 特定の機会タイプまたはステージを対象とした分析 | 選定の機会に関連するすべてのイベントが含まれます。 |
| 購買グループレベルのフィルター | 購買グループの特定の状態を対象とした分析 | 適格な購買グループの人々からのイベントが含まれます。 |
| 個人レベルのフィルター | 条件に一致する個人（特定の役割、役職など）を対象とした分析 | 標準フィルター動作： B2Bの文脈における個々のエンゲージメントを分析する場合に使用します。 |

#### ワークスペース分析の構築

**UI ナビゲーション：** [!DNL Customer Journey Analytics] / Workspace / プロジェクト / プロジェクトを作成

主要な設定の詳細：

- フェーズ 2で作成されたB2B データビューを選択します
- アカウントレベルのディメンション（アカウント名、業界、階層）をエンゲージメント指標ごとに分割して、フリーフォームテーブルを構築します
- 商談funnelのビジュアライゼーションで、ステージ間の商談の進行状況を示します
- 役割ごとの役割の入力率とエンゲージメントを示す購買グループ構成テーブルを作成します
- 13か月間のルックバックによるアトリビューションモデル（線形、U字型、時間減衰）を比較するB2B アトリビューションパネルを設定します
- 購買ジャーニーの一般的なパスを示すアカウントフローのビジュアライゼーションを作成
- アカウントのリテンションとリエンゲージメントを長期的に分析するコホートテーブルを構築します
- B2B フィルターを適用して、アカウント層、業界、エンゲージメントレベルごとに分析をセグメント化します
- 重要なイベント（キャンペーンのリリース、製品リリース、価格変更）の注釈を作成します

**Experience League ドキュメント：**

- [Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [プロジェクトの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [フリーフォームテーブル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [アトリビューションパネル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [フローの可視化](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [フォールアウトの可視化](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [コホートテーブル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [フィルターの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [計算指標の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [計算指標の作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [注釈の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [ガイド付き分析の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [ディメンションの分類](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

### フェーズ 4：ダッシュボードの公開

**アプリケーション関数：** [!DNL CJA]: ダッシュボードとスコアカード公開、[!DNL CJA]: オーディエンス公開

共有可能なダッシュボードとモバイルスコアカードを作成して、B2B分析のインサイトを関係者に提供できます。 このフェーズでは、[!DNL CJA]定義されたB2B オーディエンスをAEPに公開して、B2B オーディエンスのアクティベーションなどの下流のユースケースでアクティベートすることも対象としています。

#### 決定：ダッシュボードの配信方法

B2B分析のインサイトをステークホルダーに提供する方法を決定する。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| Workspace プロジェクト（デスクトップ） | インタラクティブな調査を必要とするアナリストやマーケティングオペレーション | フルインタラクティブ、ドリルダウン、フィルター切り替え。 [!DNL CJA] アクセスが必要です。 |
| モバイルスコアカード | 経営陣とセールスリーダーの連携 | 傾向線を使用した概要数値。 [!DNL Adobe Analytics] ダッシュボードアプリからアクセスできます。 限定的なインタラクション： |
| スケジュールされたPDF/CSV書き出し | [!DNL CJA]人のアクセス権を持たない関係者で、定期的な更新が必要 | スケジュールに従った自動配信： インタラクティブなし。 週/月ごとの経営陣の概要に最適です。 |
| 上記のすべて | 多様な関係者ニーズを有する大規模な組織 | リーチの拡大： メンテナンス作業の増加： 成熟したB2B分析プログラム向け。 |

#### 決定：[!DNL CJA]からのオーディエンスの公開

B2B セグメントをAEPに公開してアクティベーションするかどうかを決定します。

| オプション | 選択するタイミング | 検討事項 |
| --- | --- | --- |
| アカウントベースのオーディエンスを公開 | 分析インサイトを活用して、ターゲティングと抑制を強化しましょう | [!DNL RT-CDP]を介して[!DNL CJA]定義のセグメント（例：「オープンな機会のない高度にエンゲージされたアカウント」）のアクティブ化を有効にします。 更新頻度：4時間～毎週 |
| 公開しない | 分析はレポート用であり、アクティベーション用ではありません | 容易な設定： アクティベーションは[!DNL RT-CDP]で個別に処理されました。 |

#### ダッシュボードとオーディエンスの公開

**UI ナビゲーション：** [!DNL Customer Journey Analytics] > プロジェクト / 共有（Workspace用）、プロジェクト / 作成/ モバイルスコアカード（スコアカード用）、コンポーネント / オーディエンス / 公開（オーディエンス公開用）

主要な設定の詳細：

- 主要なB2B KPI （エンゲージメントアカウントの合計、パイプラインの価値、購買グループの完全性）の概要番号を含むエグゼクティブダッシュボードを構築します
- トレンド指標の比較期間（月単位、四半期単位）を設定します
- アカウントエンゲージメント、パイプラインの健全性、アトリビューション指標のタイルを使用して、モバイルスコアカードを作成します
- 上級管理職が地域、業界、アカウント階層ごとにビューを切り替えるためのフィルターを追加する
- 週次エグゼクティブレポート用にスケジュールされたプロジェクト配信を設定する
- オーディエンスの公開の場合：B2B フィルターを選択し、ID名前空間（アカウント ID）を設定し、更新頻度を設定します

**Experience League ドキュメント：**

- [モバイルスコアカードの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [プロジェクトの共有](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [プロジェクトのスケジュール](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [スコアカードの設定とキュレート](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analyticsダッシュボード：エグゼクティブガイド](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [オーディエンスの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [オーディエンスの作成と公開](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)

## 実装に関する考慮事項

以下のセクションでは、実装中に留意すべきガードレール、一般的な落とし穴、ベストプラクティス、トレードオフの決定について説明します。

### ガードレールと制限

- [!DNL CJA]接続には、1つのAEP サンドボックスのデータセットのみを含めることができます – [CJA ガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)
- データビューごとに最大5,000のディメンションと5,000の指標
- データビューごとに最大100個の派生フィールド
- B2B アトリビューションは、アカウントレベルの分析において、最大13か月のルックバックウィンドウをサポートします
- すべてのサンドボックスで[!DNL CJA]のお客様ごとに最大75個の公開オーディエンス
- オーディエンスの公開の最小更新頻度は4時間ごとです
- AEPから[!DNL CJA]へのストリーミングの遅延は、通常90分未満です
- フリーフォームテーブルは、最大10個のディメンション分類に対応しています
- モバイルスコアカードは、スコアカードごとに最大16個のタイルをサポートします
- Workspace プロジェクトでは、1つのプロジェクトにつき最大40 パネルをサポートします
- 大規模なB2B データセット（数十億件のレコード）のバックフィルは、完了に数日かかる場合があります

### よくある落とし穴

- **不完全な個人とアカウントのマッピング：**&#x200B;個人レベルのイベントがアカウントに関連付けられない場合、個人レベルの分析には表示されません。 すべてのイベントデータセットに、直接または個人とアカウントの関係のルックアップデータセットを通じて、アカウント IDに結合できるフィールドが含まれていることを確認します。 分析を構築する前に、アカウントの関連付けが欠落しているイベントの割合を監査します。
- **データセットのタイプ指定が正しくありません：** B2B参照データセット（商談、購買グループ、個人とアカウントの関係）は、[!DNL CJA]接続で参照またはプロファイルタイプとして正しく指定されている必要があります。 ルックアップデータセットをイベントデータセットとして入力すると、[!DNL CJA]が各レコードをタイムスタンプ付きイベントとして扱おうとするため、誤った結果が生成されます。
- B2B:**に対して** アトリビューションウィンドウが短すぎます。デフォルトの30日間のアトリビューションウィンドウを使用すると、通常6～18か月に及ぶB2B ジャーニーの初期段階のタッチポイントを見逃すことになります。 B2B アトリビューション指標の13か月間のルックバックウィンドウを常に設定します。
- **アカウントレベルの指標と個人レベルの指標を誤って混在させる：** アカウントレベルの分析で「人物」をカウントすると、誤解を招く可能性があります。 計算された指標が適切なコンテナレベルで定義されていることを確認します。 「アカウントエンゲージメント率」では、アカウントレベルのイベントを人ではなくアカウントで割る必要があります。
- **古い購買グループデータ：**&#x200B;購買グループの構成と役割の割り当ては、時間の経過とともに変化します。 購買グループのデータセットが定期的に更新されない場合、完全性の指標は不正確になります。 ソースシステム（[!DNL Marketo Engage]または[!DNL AJO] B2B edition）が購買グループデータをアクティブに同期していることを確認します。
- **単一のワークスペース プロジェクトの過負荷：** B2B分析は、エンゲージメント、パイプライン、アトリビューション、購買グループにまたがっています。 ひとつのプロジェクトにすべてを集約しようとすると、読み込みが遅くなり、操作が混乱します。 複数の焦点を絞ったプロジェクトや、明確にラベル付けされたパネルを使用することも可能です。

### ベストプラクティス

- 後でオプション B （グローバルアカウント）を使用する予定がある場合でも、オプション A （アカウント中心）から開始します。 アカウント中心の分析が容易になり、階層が複雑になる前にデータモデルを検証できます。
- アカウントの関連付け、孤立したアカウント数、購買グループの完全性指標を使用してイベントの割合を追跡する、専用の「B2B データ品質」ワークスペースプロジェクトを作成します。 データの問題を早期に発見するために、今週実施してください。
- 派生フィールドを使用して、アカウントレベルのイベント数にもとづいて、エンゲージメントのスコアリング層（高/Medium/低）を構築します。 これにより、分析が簡素化され、技術的な知識を持たない関係者でもダッシュボードをより実用的なものにできます。
- B2B アトリビューションを設定する際は、ベースラインとして線形アトリビューションを開始し、U字型モデルと時間減衰モデルを比較します。 モデル間の違いにより、マーケティングミックスが認知度に向けられているのか、コンバージョンに向けられているのかが明らかになります。
- 経営陣にとって最も重要なKPIをカバーするタイルが8つまでである、「B2B エグゼクティブサマリー」モバイルスコアカードを公開します。 集中力を維持する：「現状はどうなっているか」という質問に対して、経営陣が回答する必要があります 「なぜ？」ではなく
- 主要なイベント（製品の発売、主要なキャンペーンの開始、価格設定の変更、セールスプロセスの変更）に注釈を付けて、データトレンドのコンテキストを提供します。 B2B データでは、多くの場合、イベントのコンテキストなしに説明できない急増や急減が発生します。
- [!DNL CJA]からB2B オーディエンスを公開する場合は、標準のアクティベーションセグメントに毎日の更新を使用し、時間制限のあるセグメントに対してのみ4時間の更新を使用します。 頻繁な更新は、処理リソースを消費します。

### トレードオフの決定

>[!NOTE]
>以下のトレードオフの決定は、組織の固有の要件と制約に基づいて評価する必要があります。

**データの完全性と分析精度の比較**

アカウント分析にすべての個人レベルのイベントを含めると（アカウントとの関連付けが脆弱なイベントも含めて）、データの完全性は向上しますが、アカウントマッピングが信頼性に欠ける場合、分析精度が低下する可能性があります。

- **すべてのイベントのメリットを含む：**&#x200B;包括的なエンゲージメント測定、アカウントエンゲージメントスコアの向上、より幅広い可視性
- **一致しないイベントの優先を除外：**&#x200B;正確なアカウントレベルの指標、信頼できるアトリビューション、信頼性の高いパイプライン相関関係
- **推奨事項：**&#x200B;一致しないイベントをアカウントレベルの分析から除外しますが、全体像を把握するために、個別の個人レベルのデータビュー（オプション C）にそれらを含めます。 並行して進めるワークストリームとして、アカウントとの関連データの品質を向上することを優先する。

**B2B アトリビューション ルックバック ウィンドウの長さ**

ルックバックウィンドウが長い（13か月）場合、より多くの顧客接点を把握できますが、現在の購買決定とは関連性のないマーケティング活動が含まれる場合があります。

- **より長いルックバック（13か月）のメリット：** B2B ジャーニー全体を把握し、認知段階のアクティビティをクレジットし、長いセールスサイクルに対応する
- **ルックバック期間が短い（6か月）方が好ましい：**&#x200B;最近のエンゲージメントに焦点を当て、古い顧客接点からのノイズを減らし、現在の購買意欲をより反映する
- **推奨事項：**&#x200B;長いセールスサイクル（12か月以上）を持つエンタープライズアカウントには、13か月間のルックバックを使用します。 サイクルが短い中規模のアカウントには、6 ヶ月間のルックバックを使用します。 比較する各ウィンドウに対して、別々の計算指標を作成します。

**単一の包括的なデータビューと複数の焦点を絞ったデータビュー**

B2Bのあらゆるコンテナとディメンションを含む単一のデータビューは、維持が容易ですが、アナリストにとっては複雑な作業に時間がかかる可能性があります。 複数のデータビュー（エンゲージメント、パイプライン、アトリビューション）は使いやすいが、維持は困難です。

- **単一ビューの利点：**&#x200B;単一プロジェクト内での一貫性、メンテナンスの簡素化、ドメイン間の分析
- **複数のビューのメリット：** アナリスト向けのシンプルさ、読み込み時間の短縮、ユースケースごとにカスタマイズされたコンポーネントリスト
- **推奨事項：**&#x200B;最初に、単一の包括的なデータビューを作成します。 アナリストが適切なディメンションと指標を見つけるのが困難であると報告した場合は、複数のビューに分割する前に、同じビュー内にキュレーションされたコンポーネントグループを作成します。 ワークスペーステンプレートを使用して、アナリストを適切なコンポーネントに誘導します。

## 関連ドキュメント

次のリソースでは、このユースケースパターンを実装するための追加情報を提供します。

**[!DNL CJA]B2B edition**

- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJAのガードレール](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

**接続**

- [接続の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [接続の作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [接続の管理](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)

**データビュー**

- [データビューの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [データビューの作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [コンポーネント設定の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [永続性の設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [アトリビューション設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [書式設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [派生フィールド](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [セッション設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspaceと分析**

- [Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [プロジェクトの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [フリーフォームテーブル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [フローの可視化](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [フォールアウトの可視化](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [コホートテーブル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [アトリビューションパネル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [プロジェクトの共有](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [プロジェクトのスケジュール](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [ディメンションの分類](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**コンポーネント**

- [フィルターの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [フィルターの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [計算指標の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [計算指標の作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [注釈の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [日付範囲](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**オーディエンス**

- [オーディエンスの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [オーディエンスの作成と公開](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [オーディエンスの管理](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)

**ダッシュボードとスコアカード**

- [モバイルスコアカードの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [スコアカードの設定とキュレート](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analyticsダッシュボード：エグゼクティブガイド](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**ガイド付き分析**

- [ガイド付き分析の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [トレンド表示](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [顧客維持ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [RT-CDP B2B editionの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [B2B edition スキーマ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [B2B ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/sources/b2b)

**AEP data foundation**

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Marketo Engage コネクタ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)

**データガバナンスとライフサイクル**

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [高度なデータライフサイクル管理](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

**チュートリアルとガイド**

- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Observability Insightsの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
