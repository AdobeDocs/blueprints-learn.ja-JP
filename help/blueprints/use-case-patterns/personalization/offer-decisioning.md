---
title: Offer Decisioning
description: 一元化された意思決定ロジックを使用して、チャネルをまたいでプロファイルに最適なオファーやコンテンツを選択する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 5%

---

# オファー決定支援

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO） Decisioningと[!DNL Adobe Real-Time Customer Data Platform] （RT-CDP）を使用して、チャネルをまたいで各顧客プロファイルに対する次善のオファーを決定する一元化されたオファー選択ロジックを実装する、オファー決定のユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

このパターンは、「何を示すべきか」という決定を「どこで示すべきか」というチャネルロジックから切り離し、メール、web、モバイルアプリなどの顧客接点をまたいで、一貫性のある最適化されたオファー選択を可能にします。 AJO Decisioningは、オファーの作成とカタログ管理、適格性ルール（各オファーを表示できる担当者）、ランキング戦略（適格なオファーの選択方法）、プレースメント（オファーが表示される場所）、意思決定ポリシー（すべてをまとめる）など、オファーのライフサイクル全体を管理します。

## ユースケースパターン

この節では、オファー決定の実行計画とパターン定義について説明します。

**オファー決定**

一元化された意思決定ロジックを使用して、チャネルをまたいでプロファイルに最適なオファーやコンテンツを選択します。

**実行プラン：** オーディエンス評価> オファーの適格性> ランキング戦略>決定実行>配信> レポート

## ユースケースの概要

企業は、多くの場合、顧客とのやり取りにおいて、各顧客に対して最も関連性の高いオファー、プロモーション、インセンティブを提供する必要があります。 電子メールキャンペーン、web サイトのホームページ、モバイルアプリ、マルチステップのジャーニーの意思決定段階など、顧客が誰で、何に適格か、望ましい成果を上げる可能性が最も高いオファーにもとづいて、利用可能なオプションカタログから最適なオファーを選択するという課題は同じです。

Offer Decisioningは、すべてのオファー選択ロジックをAJOの意思決定管理エンジンに一元化することで、この問題に対処します。 決定エンジンは、オファーの割り当てを個々のキャンペーンやチャネルにハードコーディングするのではなく、各プロファイルの属性、オーディエンスメンバーシップ、文脈的シグナルを評価し、最適なオファーをリアルタイムで決定します。 この一元管理により、顧客がどのチャネルを通じてエンゲージしても、同じ顧客が一貫性のある最適化されたオファーを受け取ることができます。

このパターンは、スコープにおける既知の訪問者のweb/アプリのパーソナライゼーションとは異なります。オファーの決定は、チャネルに依存せず一元化されていますが、既知の訪問者のパーソナライゼーションは、デジタルサーフェスのパーソナライゼーションに重点を置いています。 カタログモデルにおける行動レコメンデーションとは異なります。対象となる商品セットが、ビジネスルール、適格性の制約、規制要件（プロモーション、金融商品、インセンティブ）などによって管理される場合に、オファー決定機能を使用します。 アイテムセットが大規模で継続的に変化し、行動の類似性や親和性のシグナル（製品カタログ、コンテンツライブラリ）によって選択が決定される場合は、行動レコメンデーションを使用します。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

**[パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
個人の好み、行動、ライフサイクルのステージに合わせて、コンテンツ、オファー、メッセージを調整。
**KPI:**&#x200B;のエンゲージメント、コンバージョン率、顧客満足度（CSAT）

**[クロスセルとアップセルの収益を促進](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
行動や購入履歴にもとづいて、既存顧客に補完的な商品やサービスを宣伝します。
**KPI:** アップセル/クロスセル %、増分収益、顧客生涯価値

**[顧客ロイヤルティと生涯価値の向上](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
ロイヤルティプログラム、特典、パーソナライズされたエンゲージメントを通じて、顧客関係を深化し、長期的な価値を最大化します。
**KPI:**&#x200B;顧客のライフタイムバリュー、リテンション、アップセル/クロスセル %

## 戦術的なユースケース

次のシナリオは、オファー決定を実際にどのように適用できるかを示しています。

- メール施策で「次善のオファー」を活用：送信時に、受信者ごとに最も関連性の高いプロモーションを選択します
- web サイト上のリアルタイムのプロモーションバナー：意思決定機能では、訪問者のプロファイルにもとづいて、ページ読み込み時にオファーを選択します
- ユーザーのライフサイクル段階に最適なインセンティブを提供する、パーソナライズされたアプリ内カード
- クロスチャネルのオファーの一貫性 – 同じ意思決定ロジックで電子メール、web、プッシュ通知を提供し、顧客が統一されたオファー体験を目にできるようにします
- 顧客価値の階層にもとづく動的なクーポンまたは割引の選択（価値の高い顧客にプレミアムオファーを提供するなど）
- 現在のサブスクリプションレベルに基づいて、製品のアップグレードまたはアップセルオファーを選択
- ロイヤルティ報酬：層とアクティビティ履歴にもとづいてパーソナライズされたオファー

## 主要業績評価指標

次のKPIは、オファー決定実装の有効性を測定するのに役立ちます。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| オファーの承認率 | クリック、引き換え、コンバージョンにつながる配信されたオファーの割合 | オファークリック数/引き換え数/配信されたオファー数 |
| オファーの選択の配布 | あらゆる意思決定で選択された各オファーの割合 | オファーあたりのカウント / レンダリングされた決定合計 |
| フォールバック率 | パーソナライズされたオファーが選定されず、フォールバックが提供された意思決定の割合 | フォールバックインプレッション数/総意思決定数 |
| コンバージョン率 | 目的のアクション（購入、サインアップ、引き換え）を完了したオファー受信者の割合 | コンバージョン/オファーインプレッション |
| 売上増加 | 選択したオファーとコントロールグループまたはフォールバックの決定に起因する売上 | パーソナライズされたオファーからの収益 – フォールバック/コントロールからの収益 |
| クロスチャネルの一貫性スコア | 定義されたウィンドウ内で複数のチャネルにわたって同じオファーを受け取るプロファイルの割合 | 一貫性のあるオファー/マルチチャネルのインプレッション数 |
| オファークリックスルー率 | クリックにつながるオファーインプレッションの割合 | オファークリック数/オファーインプレッション数 |

## アプリケーション

このユースケースパターンでは、次のAdobe アプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO）** — オファー作成、適格性ルール、ランキング戦略、プレースメント、および決定ポリシー用の意思決定管理エンジン、オファー配信のチャネル設定およびメッセージのオーサリング、キャンペーンおよびジャーニーの実行
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** — オファーの適格性セグメントに対するオーディエンス評価。適格性とランキングで使用されるプロファイルデータと計算属性
- **[!DNL Adobe Experience Platform]（AEP）** — AJOとRT-CDPの両方をサポートする統合プロファイルストア、ID解決、データ基盤

## 関連ドキュメント

次のリソースでは、このユースケースパターンで使用されるコンポーネントに関する追加の詳細を示します。

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

### オファーの配信

- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Decisioning APIを使用したオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### チャネル設定

- [メール設定の基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [メールサーフェス設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [サブドメインをデリゲート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [プッシュ通知チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [SMS チャネルの設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### メッセージのオーサリングとパーソナライゼーション

- [メールコンテンツのデザイン](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツのプレビューとテスト](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### キャンペーンとジャーニー

- [キャンペーンの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [ジャーニーの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### コンテンツの検証

- [コンテンツ実験を始める](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [コンテンツ実験を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### プロファイルとID

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Customer AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### データモデリングと収集

- [XDM システムの概要](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

### レポートと分析

- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [ジャーニーグローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### データガバナンスとライフサイクル

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [データ使用状況ラベルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/labels/overview)
- [高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Journey Optimizerでの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### チュートリアル

- [意思決定管理APIの概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
