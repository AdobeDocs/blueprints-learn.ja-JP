---
title: Customer Analytics & Insightの生成
description: 行動分析とパフォーマンス分析のためのクロスチャネル分析ワークスペース、計算指標、ダッシュボードの構築方法について説明します。
solution: Customer Journey Analytics, Experience Platform
exl-id: 235a4eb0-91ae-4030-b90e-7eda08c67ae1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 3%

---

# 顧客分析とinsightの生成

このガイドでは、顧客分析とinsight生成のユースケース パターンについて説明します。このパターンでは、[!DNL Adobe Experience Platform]個のデータセットを[!DNL Customer Journey Analytics]に接続して、データビュー、フリーフォーム分析ワークスペース、計算指標、ダッシュボード、モバイルスコアカードを構築し、オプションでCJA定義オーディエンスを[!DNL Adobe Experience Platform]に公開してアクティベーションします。

このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

アクティベーションとエンゲージメント（メッセージの送信、コンテンツのパーソナライズ、オーディエンスのアクティベーション）に重点を置く他のパターンとは異なり、このパターンは、顧客行動の分析、キャンペーンのパフォーマンスの測定、トレンドの特定、戦略と最適化の意思決定に役立つインサイトの生成などの理解に重点を置いています。

## ユースケースパターン

**顧客分析とinsightの生成**

クロスチャネルの分析ワークスペース、計算指標、ダッシュボードを構築して、顧客行動とキャンペーンのパフォーマンスを把握できます。

**実行プラン：** Data Connection > Data View Configuration > Workspace Analysis > Dashboard Publishing

## ユースケースの概要

企業は、チャネルをまたいだ顧客の行動、キャンペーンのパフォーマンス、カスタマージャーニーにおける顧客の脱落、共感を呼ぶコンテンツ、時間の経過とともに様々なセグメントがどのように維持されるのかを把握する必要があります。 Customer Analyticsとinsight generationは、このニーズに対応します。アナリストは[!DNL Adobe Experience Platform]の豊富なクロスチャネルデータを[!DNL Customer Journey Analytics]に接続し、フリーフォームワークスペースの構築、カスタム指標の作成、アトリビューションモデルの設定、関係者が利用するためのダッシュボードの公開を行うことができます。

このパターンは、複数のオーディエンスにサービスを提供します。例えば、詳細な探索分析を必要とするマーケティングアナリスト、パフォーマンスダッシュボードを必要とするキャンペーンマネージャー、エンゲージメントと顧客維持率のインサイトを必要とするプロダクトマネージャー、一目でKPI スコアカードを必要とする経営陣などです。 導入のアプローチは、主要な分析焦点であるキャンペーンパフォーマンスの測定、クロスチャネルジャーニー分析、分析主導のオーディエンスのアクティベーション、ガイド付きの製品インサイトなどによって異なります。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

**分析とレポートの改善**

統合ダッシュボードとセルフサービスツールを通じてレポート機能を強化し、より迅速で実用的なマーケティングインサイトを獲得できます。

- **KPI:**&#x200B;効率、生産性

このビジネス目標について詳しくは、[分析とレポートの改善](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)を参照してください。

**データ主導の意思決定を可能にする**

セルフサービス型の分析、リアルタイムの顧客インサイト、AIを活用した予測により、戦略を策定できます。

- **KPI:**&#x200B;効率、生産性

このビジネス目標について詳しくは、[&#x200B; データ主導の意思決定を有効にする](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)を参照してください。

**マーケティングアトリビューションの改善**

マーケティングの顧客接点、チャネル、キャンペーンがコンバージョンと収益に与える影響を正確に測定。

- **KPI:**&#x200B;効率、増分収益

このビジネス目標について詳しくは、[&#x200B; マーケティングアトリビューションの改善](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)を参照してください。

**マーケティング費用とROIの最適化**

最も高いリターンを生み出すチャネルと施策を把握し、マーケティング予算の配分を最適化できます。

- **KPI:**&#x200B;効率、増分収益

このビジネス目標について詳しくは、[&#x200B; マーケティング費用とROIの最適化](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)を参照してください。

## 戦術的なユースケース

次に、このパターンで実装できる戦術的なユースケースの例を示します。

- キャンペーンパフォーマンスダッシュボード – メール、SMS、プッシュ通知、有料メディアキャンペーンをまたいだ配信指標、エンゲージメント率、コンバージョン、収益アトリビューション
- カスタマージャーニーのフォールアウト分析 – 購入、登録、オンボーディングファネルにおいて、顧客がどこで離脱しているのかを特定します
- コホート維持分析：数週間、数カ月、数四半期にわたって、さまざまな獲得コホートがどの程度維持しているのかを測定できます
- チャネルアトリビューションモデル：ファーストタッチ、ラストタッチ、線形、時間減衰のアトリビューションを比較し、コンバージョンを促進するチャネルを把握できます
- コンテンツパフォーマンス分析：セグメント、チャネル、ライフサイクルのステージごとに、最も共感を呼ぶコンテンツを特定できます
- 製品の利用状況と導入分析：機能の導入状況、エンゲージメント頻度、ユーザーの増加傾向を追跡できます
- 顧客のライフサイクルのステージ分析：ライフサイクルのステージ（新、アクティブ、リスクあり、休眠）ごとに顧客をセグメンテーションおよび分析できます
- マーケティングミックス最適化ダッシュボード – チャネルへの投資と売上への貢献度を比較
- クロスチャネルのエンゲージメントスコアリングとレポート - web、アプリ、電子メール、キャンペーンのインタラクションから複合エンゲージメントスコアを構築できます

## 主要業績評価指標

次のKPIは、このユースケースパターンの成功を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| 効率性 | Insight作成までの時間と手作業によるレポート作成の時間を短縮 | CJAの導入前後でレポートを作成したアナリストの時間を追跡したい |
| 生産性 | ビジネスユーザーが作成したセルフサービス分析の数 | Workspaceプロジェクトの作成とダッシュボードの使用状況のモニタリング |
| 売上増加 | インサイトにもとづく最適化の意思決定による売上 | CJAの分析にもとづいて最適化されたキャンペーンの売上向上を測定 |
| コンバージョン率 | 主要なカスタマージャーニーにおけるFunnelの完了率 | CJAのフォールアウトビジュアライゼーションを使用して、各ジャーニーステップでのフォールアウト率を追跡します |
| エンゲージメント | チャネルをまたいだ顧客インタラクションの深さと頻度 | CJAを使用して、エンゲージメントスコアリングの計算指標を構築 |
| 定着 | 定義された期間の顧客返品率 | CJAコホート分析を使用して顧客維持率を測定する |

## アプリケーション

このユースケースパターンでは、次のアプリケーションを使用します。

- **[!DNL Customer Journey Analytics]（CJA）** – 接続、データビュー、ワークスペース分析、ガイド付き分析、計算指標、ダッシュボード、オーディエンス公開、Content Analytics
- **[!DNL Adobe Experience Platform]（AEP）** — CJA接続をフィードするデータレイク、データセット、XDM スキーマ、プロファイルおよびイベントデータ

## 関連ドキュメント

次のリソースでは、このユースケースパターンに関する追加情報を提供しています。

### [!DNL Customer Journey Analytics] – はじめに

- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJAのガードレール](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

### 接続

- [接続の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [接続の作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [接続の管理](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)

### データビュー

- [データビューの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [データビューの作成または編集](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [コンポーネント設定の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [永続性の設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [アトリビューション設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [書式設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [指標の重複排除](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [値を含める/除外](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [セッション設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)
- [派生フィールド](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Workspaceと分析

- [Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [プロジェクトの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [フリーフォームテーブル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [フローの可視化](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [フォールアウトの可視化](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [コホートテーブル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [アトリビューションパネル](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [ディメンションの分類](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [プロジェクトの共有](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [プロジェクトのスケジュール](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [書き出しの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/export/export-cloud)

### ガイド付き分析

- [ガイド付き分析の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [トレンド表示](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [エンゲージメントの頻度ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [顧客維持ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [アクティブな成長ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [リリースの影響ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/release)
- [初回使用の影響ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/impact/first-use)
- [タイムラインビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/streams/timeline)

### コンポーネント

- [フィルターの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [フィルターの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [計算指標の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [計算指標の作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [計算指標関数](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [注釈の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [日付範囲](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)
- [指標コンポーネント](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/apply-create-metrics)

### オーディエンスの公開

- [オーディエンスの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [オーディエンスの作成と公開](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [オーディエンスの管理](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)

### コンテンツ分析

- [Content Analytics](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/content-analytics/content-analytics)
- [Content Analytics設定](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/config/configuration)

### ダッシュボードとスコアカード

- [モバイルスコアカードの作成](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [スコアカードの設定とキュレート](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analyticsダッシュボード：エグゼクティブガイド](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [概要数値のビジュアライゼーション](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)

### AEP財団

- [データセットの概要](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/overview)
- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [オーディエンスポータルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-portal)

### AJOレポートの統合

- [AJO + CJA統合ガイド](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [キャンペーンメールレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/campaign-global-report-cja-email)
- [ジャーニーメールレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/journey-global-report-cja-email)

### チュートリアルとガイド

- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
