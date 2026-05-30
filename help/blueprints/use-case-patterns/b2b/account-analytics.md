---
title: B2B 分析
description: クロスチャネルのカスタマージャーニー分析にB2B アカウントレベルの情報を含める方法について説明します。
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 2%

---

# B2B分析

このガイドでは、[!DNL Customer Journey Analytics] （[!DNL CJA]）B2B editionと[!DNL Real-Time Customer Data Platform] （[!DNL RT-CDP]）B2B editionを使用して、B2B アカウントレベルの情報をクロスチャネルのカスタマージャーニー分析に組み込むB2B分析のユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

B2B Analyticsは、アカウントベースの接続、B2B固有のコンテナ （アカウント、グローバルアカウント、商談、購買グループ）、アカウントレベルのレポートにより、標準の[!DNL CJA]機能を拡張します。 この機能により、アカウントレベルでのマーケティングとセールスのエンゲージメントを分析し、機会の進捗状況を追跡して、購買グループの完全性を測定し、拡張されたB2B セールスサイクル全体のマーケティング接点に売上を関連付けることができます。

## ユースケースパターン

**B2B分析**

クロスチャネルのカスタマージャーニー分析に、B2Bのアカウントレベルの情報を含めましょう。

**実行計画：** B2B Data Connection > Account Data View Configuration > Workspace Analysis > Dashboard Publishing

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

## アプリケーション

このユースケースパターンを実装するには、次のアプリケーションを使用します。

- **[!DNL Customer Journey Analytics]B2B edition** — アカウントベースの接続、B2B固有のデータビューコンテナ、アカウントレベルのワークスペース分析、購買グループ分析、商談分析、B2B セグメンテーション、およびB2B アトリビューションを、拡張されたルックバックウィンドウで提供します
- **[!DNL Real-Time CDP]B2B edition** — アカウントプロファイルの統合、B2B ID解決、B2B スキーマクラス （アカウント、商談、購買グループ）、B2B エンゲージメントデータの取り込み用の[!DNL Marketo Engage]統合など、B2B データ基盤を提供します

## 関連ドキュメント

次のリソースでは、このユースケースパターンを実装するための追加情報を提供します。

**[!DNL CJA]B2B edition**

- [CJA B2B editionの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [CJAの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJAのガードレール](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-admin/guardrails)

**接続**

- [接続の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/overview)
- [接続の作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/create-connection)
- [接続の管理](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-connections/manage-connections)

**データビュー**

- [データビューの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/data-views)
- [データビューの作成または編集](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [コンポーネント設定の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [永続性の設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [アトリビューション設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [書式設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [派生フィールド](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [セッション設定](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspaceと分析**

- [Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)
- [プロジェクトの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [フリーフォームテーブル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [フローの可視化](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [フォールアウトの可視化](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [コホートテーブル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [アトリビューションパネル](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [プロジェクトの共有](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [プロジェクトのスケジュール](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [ディメンションの分類](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**コンポーネント**

- [フィルターの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [フィルターの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [計算指標の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [計算指標の作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [注釈の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/annotations/overview)
- [日付範囲](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**オーディエンス**

- [オーディエンスの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [オーディエンスの作成と公開](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/publish)
- [オーディエンスの管理](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-components/audiences/manage)

**ダッシュボードとスコアカード**

- [モバイルスコアカードの作成](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [スコアカードの設定とキュレート](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analyticsダッシュボード：エグゼクティブガイド](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**ガイド付き分析**

- [ガイド付き分析の概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel ビュー](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [トレンド表示](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/guided-analysis/trends/usage)
- [顧客維持ビュー](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [RT-CDP B2B editionの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [B2B edition スキーマ](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/schemas/b2b)
- [B2B ソースの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/sources/b2b)

**AEP data foundation**

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [ソースの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/home)
- [Marketo Engage コネクタ](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [サンドボックスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/sandbox/home)

**データガバナンスとライフサイクル**

- [データガバナンスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)
- [高度なデータライフサイクル管理](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home)

**チュートリアルとガイド**

- [スキーマ構成の基本](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition)
- [計算属性の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/computed-attributes/overview)
- [Observability Insightsの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/observability/home)
