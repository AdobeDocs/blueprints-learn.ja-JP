---
title: Decisioning を使用したクロスチャネルジャーニー
description: リアルタイムの意思決定を組み込んだマルチステップのジャーニーを編成して、最適なチャネル、コンテンツ、オファーを選択する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: eabdd91f-bb7d-4de3-adb5-5940d3ca4a78
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 5%

---

# 意思決定機能を利用したクロスチャネルジャーニー

このガイドでは、[!DNL Adobe Journey Optimizer]と[!DNL Adobe Real-Time Customer Data Platform]を使用して、1つ以上のジャーニーノードでリアルタイム決定を組み込むマルチステップのマルチチャネルジャーニーを編成する、決定ユースケースパターンを使用したクロスチャネルジャーニーについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

決定付きクロスチャネルジャーニーは、[!DNL Adobe Experience Platform] エコシステムの中で最も洗練されたキャンペーンオーケストレーションパターンです。 マルチステップのオーケストレーションされたジャーニーを拡張し、リアルタイムの意思決定を組み込みます。[!DNL AJO] Decisioningを使用して、プロファイルの現在のコンテキストを評価し、ジャーニーキャンバス内の1つ以上の意思決定ポイントで最適なチャネル、コンテンツ、オファーを動的に選択します。

## ユースケースパターン

**決定を伴うクロスチャネルジャーニー**

1つ以上のノードでリアルタイムの意思決定を組み込んだ、マルチステップのマルチチャネルジャーニーを編成して、最適なチャネル、コンテンツ、オファーを選択します。

**実行プラン：** オーディエンスの評価/ジャーニーの実行/決定ノード/チャネルの選択/メッセージ配信/レポート

## ユースケースの概要

企業は、あらかじめ決められた決められた順序に従うのではなく、各個人のリアルタイムのコンテキストに動的に対応する、適応的でパーソナライズされたカスタマージャーニーを提供する必要があります。 顧客の好むチャネル、エンゲージメント履歴、ロイヤルティ層、予測される生涯価値、現在の製品への関心などは、あらゆる顧客接点における次善のアクションを明らかにするのに役立ちます。

決定機能を備えたクロスチャネルジャーニーでは、このニーズに対応します。ジャーニーオーケストレーション（マルチステップフロー、タイミング、条件、チャネル配信を管理）と決定（適格性ルールの評価、ランキング戦略の適用、各決定ポイントでの最適なオファーまたはコンテンツのバリエーションの選択）の2つの強力な[!DNL AJO]機能を組み合わせます。

このパターンは、次のような場合に適しています。

- ジャーニーは、固定されたチャネルやコンテンツの順序に従うのではなく、各プロファイルのリアルタイムの状態に動的に適応する必要があります
- 複数のオファー、コンテンツバリエーション、チャネルは、1つ以上のジャーニーノードの候補であり、プロファイルコンテキストに基づいて最適なオプションを選択する必要があります
- ジャーニー全体でオファーの選択を最適化するには、AIを活用したランキングまたはフォーミュラベースのランキングが必要です
- 複雑な分岐ロジックを維持するのではなく、チャネル選択ロジックとオファー管理を一元化された意思決定フレームワークに統合したいと考えています

ターゲットオーディエンスには、ライフサイクルプログラム、ロイヤルティジャーニー、ウィンバック（顧客の取り戻し）シーケンス、オンボーディングフローなどを管理するマーケターが含まれます。これらのフローでは、大規模なパーソナライゼーションを実現するには、各顧客接点での意思決定の自動化が必要になります。

>[!NOTE]
>ジャーニーで個々のノードでの動的な意思決定（固定系列のナーチャリングやオンボーディングプログラムなど）が必要ない場合は、[&#x200B; マルチステップのオーケストレーションされたジャーニー](multi-step-orchestrated-journey.md)を参照してください。 このパターンは設定が簡単で、AJO Decisioningは必要ありません。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

**[パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
個人の好み、行動、ライフサイクルのステージに合わせて、コンテンツ、オファー、メッセージを調整。
**KPI:**&#x200B;のエンゲージメント、コンバージョン率、顧客満足度（CSAT）

**[顧客ロイヤルティと生涯価値の向上](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
ロイヤルティプログラム、特典、パーソナライズされたエンゲージメントを通じて、顧客関係を深化し、長期的な価値を最大化します。
**KPI:**&#x200B;顧客のライフタイムバリュー、リテンション、アップセル/クロスセル %

**[顧客維持率の向上](../../business-objectives/customer-experience/improve-customer-retention.md)**
価値主導の体験と継続的な関係育成を通じて、既存顧客との関係を維持し、更新する。
**KPI:** リテンション、顧客生涯価値、エンゲージメント

**[クロスセルとアップセルの収益を促進](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
行動や購入履歴にもとづいて、既存顧客に補完的な商品やサービスを宣伝します。
**KPI:** アップセル/クロスセル %、増分収益、顧客生涯価値

## 戦術的なユースケース

次のシナリオは、意思決定を伴うクロスチャネルジャーニーを実際にどのように適用できるかを示しています。

- **適応型ウィンバックジャーニー** – 意思決定では、各プロファイルのエンゲージメント履歴に基づいてチャネル（電子メール、プッシュ通知、SMS）を選択し、予測される生涯価値に基づいて最適なインセンティブオファーを動的に選択するマルチステップジャーニー
- **次善のアクションライフサイクルジャーニー** — オンボーディングコンテンツ、クロスセルオファー、ロイヤルティ特典、リテンションインセンティブから選択して、顧客ライフサイクルの各段階で何を伝えるべきかを決定します
- **動的なコンテンツ選択によるパーソナライズされたオンボーディング** – 各顧客接点で意思決定を行い、最も関連性の高い製品エデュケーションコンテンツ、ヒント、アクティベーションオファーを選択する、新規顧客オンボーディングジャーニー
- **パーソナライズされた特典を利用したクロスチャネルロイヤルティプログラムのジャーニー** — ロイヤルティメンバーは、決定者が、階層、購入履歴、カテゴリーの親和性にもとづいて、パーソナライズされた特典オファーを選択するジャーニーを進みます
- **チャネルとインセンティブの最適化による動的リエンゲージメント** — アウトリーチチャネルとインセンティブの両方を動的に選択し、応答可能性を最大化する休眠顧客リエンゲージメント
- **AIによるコンテンツレコメンデーションを利用した顧客ライフサイクルナーチャリング** — AIによる意思決定により、各顧客接点で最も関連性の高いコンテンツまたは製品レコメンデーションを選択する、継続的なナーチャリングジャーニー

## 主要業績評価指標

このユースケースパターンの有効性を測定するには、次のKPIを使用します。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| ジャーニー完了率 | ジャーニー全体を完了したプロファイルの割合 | ジャーニーレポート：完了/入力済 |
| オファーの承認率 | エンゲージメントした（クリック済み、利用済み）決定済みオファーの割合 | 意思決定レポート：オファークリック数/オファーインプレッション数 |
| チャネルエンゲージメント率 | ジャーニーで使用された各チャネルの開封率とクリック率 | ジャーニーレポートのチャネルごとの配信指標 |
| コンバージョン率 | ターゲット コンバージョンアクションを完了したジャーニー参加者の割合 | ジャーニーの離脱イベントトラッキングまたはCJA funnel analysis |
| フォールバックオファー率 | パーソナライズされたオファーではなく、フォールバックオファーを返す決定要求の割合 | 決定レポート：フォールバック選択/総選択 |
| 顧客生涯価値の影響 | ジャーニー参加者とコントロールグループのCLVの変化 | CJAコホート分析とホールドアウト比較 |
| クロスセル/アップセルの売上 | 意思決定で選択したオファーに起因する売上の増加 | オファー主導のコンバージョンに関するCJAのアトリビューション分析 |
| ランク付けの有効性 | AIによるランク付けオファーとランダム/優先ベースの選択のパフォーマンスの違い | ランキング戦略のA/B実験 |

## アプリケーション

このユースケースパターンを実装するには、次のアプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（[!DNL AJO]）** — ジャーニーオーケストレーション （マルチステップ キャンバス設計、入力条件、待機、条件、終了条件）、チャネル間でのメッセージ オーサリング、チャネル サーフェス設定、競合および優先度管理
- **[!DNL Adobe Journey Optimizer]決定** — オファーとコンテンツ項目の管理、適格性ルール、ランキング戦略（優先度、式、AI）、決定ポリシー、プレースメント、フォールバックオファー
- **[!DNL Adobe Real-Time Customer Data Platform]（[!DNL RT-CDP]）** — ジャーニー入力とオファーの適格性セグメントに対するオーディエンス評価、計算属性と傾向スコアを使用したプロファイルエンリッチメント、同意とガバナンスの適用
- **[!DNL Adobe Experience Platform]（[!DNL AEP]）** — クロスチャネル解決、データモデリング、取り込みインフラストラクチャ用のリアルタイム顧客プロファイルストア、ID サービス

## 関連ドキュメント

次のリソースでは、このユースケースパターンで使用される機能に関する追加の詳細を示します。

### ジャーニー連携

- [ジャーニーの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [ジャーニーの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [ジャーニーのプロパティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [オーディエンスアクティビティの読み取り](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [一般イベント](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [オーディエンスの選定イベント](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [条件アクティビティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [「待機」アクティビティ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [ジャーニーへのメッセージの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [終了条件](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [ジャーニー入力管理](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [ジャーニーをテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [ジャーニーを公開](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

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

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP プールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP ウォームアッププラン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [メールサーフェス設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### メッセージのオーサリングとパーソナライゼーション

- [メールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツフラグメントの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 競合、優先度、頻度の管理

- [競合と優先度管理の概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [優先スコア](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [潜在的な競合の特定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [ジャーニーの上限と調停](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [頻度ルール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [オーディエンス構成](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language リファレンス](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### レポートと分析

- [ジャーニーライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA統合ガイド](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### プロファイルとID

- [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Customer AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### データガバナンスと同意

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Journey Optimizerでの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [抑制リストの管理](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ID サービスのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
