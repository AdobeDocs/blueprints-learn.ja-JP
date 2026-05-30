---
title: 行動の推奨事項
description: 選択戦略とランキングモデルを使用して、アイテムとコンテンツのレコメンデーションを生成する方法について説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: db16e773-e0da-46c4-9fa5-d16f04feb46b
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 5%

---

# 行動レコメンデーション

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO） Decisioning、[!DNL Real-Time Customer Data Platform] （RT-CDP）、[!DNL Adobe Experience Platform] （AEP）を使用して、web、モバイルアプリ、メールチャネルをまたいでパーソナライズされたレコメンデーションエクスペリエンスを配信する、行動レコメンデーションのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

行動レコメンデーションは、商品の閲覧数、購入数、コンテンツのインタラクション、検索クエリなどの行動シグナルと、Adobe AJO Decisioningの選択戦略やランキングモデルを組み合わせることで、商品レベルまたはコンテンツレベルのレコメンデーションを生成します。 オファー決定支援では、適格性ルールとビジネス制約を使用して、オファー、プロモーション、インセンティブを決定します。一方、このパターンは、大規模で継続的に変化する項目カタログ（製品、記事、動画）に対して実行されます。このパターンでは、適格性を管理するのではなく、行動に即した親和性シグナルによって選択が促進されます。

## ユースケースパターン

**行動に関する推奨事項**

AJO Decisioningの選択戦略とランキングモデルを使用して、行動シグナルにもとづいて、コンテクストに即したコンテンツを提供するアイテムレベルまたはコンテンツレベルのレコメンデーションを生成します。

**実行計画：**&#x200B;行動シグナル取り込み>決定戦略評価> レコメンデーション配信> レポート

## ユースケースの概要

製品カタログ、コンテンツライブラリ、メディアライブラリを利用している企業は、行動履歴やセッション中のアクティビティにもとづいて、各訪問者に最も関連性の高い項目を表示する必要があります。 ホームページの「おすすめ」カルーセル、製品詳細ページのクロスセルウィジェット、メールキャンペーンに埋め込まれた製品レコメンデーションなど、訪問者の行動プロファイルをカタログの最も関連性の高い項目に一致させ、適切なチャネルでタイミングよく提供するという根本的な課題は同じです。

このパターンは、[!DNL Web SDK]または[!DNL Mobile SDK]を介してリアルタイムで行動シグナルを取り込み、商品属性と行動コンテキストを組み合わせたAJO Decisioningの選択戦略を通じて処理し、web、アプリ、またはメールチャネルを通じて推奨商品を配信することで、この課題に対処します。 ランキングモデルには、数式ベース（カテゴリーの親和性スコアによるソートなど）やAIを使用したランク（パーソナライズされたレコメンデーションモデルなど）を使用できます。 このパターンは、フォールバックレコメンデーションを設定することで、行動履歴のない新規訪問者に対するコールドスタートシナリオも処理します。

このパターンのターゲットオーディエンスには、実際のユーザー行動にもとづくパーソナライズされたレコメンデーションを通じて、エンゲージメント、コンバージョン、平均注文額を向上させたいと考えているコマースマーチャンダイジングチーム、コンテンツパーソナライゼーションチーム、デジタルエクスペリエンスチームが含まれます。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### [&#x200B; クロスセルとアップセルの収益を促進](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

行動や購入履歴にもとづいて、既存顧客に補完的な商品やサービスを宣伝します。

**KPI:** アップセル/クロスセル %、増分収益、顧客生涯価値

### [&#x200B; コンバージョン率を向上](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

購入、サインアップ、フォーム送信など、望ましいアクションを実行した訪問者と見込み顧客の割合を向上させます。

**KPI:** コンバージョン率、リードコンバージョン、リード単価

### [&#x200B; パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

個人の好み、行動、ライフサイクルのステージに合わせて、コンテンツ、オファー、メッセージを調整。

**KPI:**&#x200B;のエンゲージメント、コンバージョン率、顧客満足度（CSAT）

## 戦術的なユースケース

このパターンの一般的な戦術的な実装は次のとおりです。

- 製品詳細ページの製品クロスセルウィジェット（「顧客も購入しました」）
- 閲覧履歴に基づくホームページの「おすすめ」カルーセル
- 読み取り行動に基づくメディアサイトでのコンテンツのレコメンデーション
- 「最近閲覧した」と類似アイテムのウィジェットの組み合わせ
- 購入後の補完商品レコメンデーション
- 行動の親和性にもとづいて商品レコメンデーションを電子メールで送信
- セッション内の閲覧行動にもとづいて、カテゴリー固有のレコメンデーションを提供
- 行動シグナルにもとづく検索結果のランキング

## 主要業績評価指標

以下のKPIは、行動レコメンデーションの実装の効果を測定するのに役立ちます。

| KPI | 測定アプローチ |
| --- | --- |
| CTR （Recommendation Click-Through Rate） | 推奨項目のクリック数をレコメンデーションのインプレッションで割った値 |
| レコメンデーションコンバージョン率 | レコメンデーションクリックからの購入または望ましいアクションを、レコメンデーションクリックの合計で割った値 |
| レコメンデーションの影響を受ける売上 | 1つ以上のレコメンデーション主導型製品を含む注文の総収益 |
| 平均注文額（AOV）リフト | レコメンデーションを利用したセッションと利用しないセッションのAOVが増加 |
| 注文あたりのアイテム | レコメンデーションエンゲージメントセッションの注文あたりのアイテム数 |
| 推奨事項 | パーソナライズされた（フォールバック以外の）レコメンデーションを受け取った、適格なページビューまたはセッションの割合 |
| コールドスタートフォールバック率 | 行動履歴が不十分なため、フォールバックロジックによって提供されたレコメンデーションリクエストの割合 |

## アプリケーション

このユースケースパターンでは、次のアプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO） Decisioning** – 行動シグナルを評価し、各訪問者に最も関連性の高い項目を返す選択戦略、ランキングモデル、項目カタログ、および決定ポリシー
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** – 行動プロファイルデータの収集、レコメンデーションの範囲に対するオーディエンスの評価、行動の親和性スコアリングに対する計算属性
- **[!DNL Adobe Experience Platform]（AEP）** — [!DNL Web SDK]および[!DNL Mobile SDK]、[!DNL Edge Network]処理による行動イベントの取り込み、イベントデータおよびカタログデータのXDM スキーマ管理

## 関連ドキュメント

次のリソースでは、このパターンで使用されるテクノロジーと機能に関する追加の詳細を示します。

### 意思決定管理

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [コレクション修飾子の作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### データ収集とWeb/Mobile SDK

- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Web SDKのインストール](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [モバイル SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network Server APIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### XDMとデータモデリング

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [データセットの作成](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create)
- [2つのスキーマ間の関係の定義](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### IDとプロファイル

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### 計算属性とプロファイルエンリッチメント

- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [計算属性UI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Customer AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [チャネルサーフェスの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### メッセージのオーサリングとパーソナライゼーション

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### レポートと分析

- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [計算指標の概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### データガバナンスとライフサイクル

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [データセットの有効期限](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### 監視と監視

- [Observability Insightsの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [アラートの概要](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [取り込みのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [ID サービスのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)

### チュートリアルとガイド

- [ソースの概要](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [タグの概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [同意と環境設定のフィールドグループ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
