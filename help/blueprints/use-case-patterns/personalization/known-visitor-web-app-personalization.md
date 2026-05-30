---
title: 既知の訪問者の Web/アプリPersonalization
description: リアルタイムのプロファイルとセグメントメンバーシップにもとづいて、特定された訪問者にパーソナライズされたコンテンツ、オファー、プロモーションを配信する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 585adc0e-f528-4a09-b931-ef6b45fa8ec8
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 4%

---

# 既知の訪問者のweb/アプリのパーソナライゼーション

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO）と[!DNL Adobe Real-Time Customer Data Platform] （RT-CDP）を使用して、デジタルサーフェス全体で特定された訪問者にパーソナライズされたコンテンツを配信する、既知の訪問者web/アプリのパーソナライゼーションのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

既知の訪問者のweb/アプリのパーソナライゼーションは、認証済みのデジタルエクスペリエンスの主要なパーソナライゼーションパターンです。 セッション内の行動シグナルのみに依存する匿名訪問者のパーソナライゼーションとは異なり、このパターンは、過去の行動データ、セグメントメンバーシップ、ロイヤルティ層、購入履歴、ライフサイクルステージ、計算属性、傾向スコアなどの、完全な統合プロファイルを活用します。 （AJO web チャネルを介した） web ページ、モバイルアプリ内メッセージ、コンテンツカードをまたいだパーソナライゼーションに対応しています。

## ユースケースパターン

ここでは、コアパターンとその実行計画について説明します。

**既知の訪問者のweb/アプリのパーソナライゼーション**

web、モバイル、アプリ、コンテンツカードサーフェスをまたいでリアルタイムのプロファイルとセグメントメンバーシップにもとづいて、パーソナライズされたコンテンツ、オファー、プロモーションを特定の訪問者に配信します。

**実行計画：** オーディエンス評価> Personalization Decisioning > サーフェス/チャネル設定> コンテンツ配信> インプレッションのトラッキング > レポート

## ユースケースの概要

認証されたデジタル資産を保有する企業（e コマースサイト、バンキングポータル、サブスクリプションサービス、ロイヤルティプログラム、モバイルアプリ）は、顧客一人ひとりのブランドとの関係を反映した、パーソナライズされた体験を提供する必要があります。 訪問者がログインするか、ID解決を通じて認識されると、プラットフォームは完全な統合プロファイルにアクセスし、特定の属性、行動、嗜好に合わせてコンテンツを配信できます。

このパターンは、特定された訪問者がweb プロパティにアクセスしたり、モバイルアプリを開いたりするシナリオに対応しており、システムはリアルタイムのプロファイルデータとオーディエンスメンバーシップにもとづいて、表示する最適なコンテンツ、オファー、プロモーションを決定する必要があります。 パーソナライゼーションの決定は、エッジでミリ秒単位で行われ、知覚できる遅延なしにサブ秒単位のコンテンツ配信が可能になります。

このパターンでは、決定論的パーソナライゼーション（特定のコンテンツを特定のオーディエンスセグメントにマッピングする場合）と動的な意思決定（AJO Decisioningが適格性ルールとランキング戦略を評価して、プロファイルごとに最適なコンテンツを選択する場合）の両方をサポートしています。 web ページ、モバイルのアプリ内メッセージ、コンテンツカードなど、複数のデジタルサーフェスにまたがり、顧客のデジタルジャーニー全体にわたって一貫性のあるパーソナライゼーションを可能にします。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### パーソナライズされた顧客体験の実現

個人の好み、行動、ライフサイクルのステージに合わせて、コンテンツ、オファー、メッセージを調整。 詳しくは、[ パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)を参照してください。

**KPI:**&#x200B;のエンゲージメント、コンバージョン率、顧客満足度（CSAT）

### web サイトのエンゲージメントの向上

適切なエクスペリエンスを通じて、サイトでの滞在時間、セッションごとのページ、web コンテンツとのインタラクションを改善できます。 詳しくは、[web サイトのエンゲージメントの向上](../../business-objectives/acquisition-growth/increase-website-engagement.md)を参照してください。

**KPI:**&#x200B;時間（web） ページ、エンゲージメント、コンバージョン率

### モバイルアプリのエンゲージメントの向上

パーソナライズされたアプリ内エクスペリエンスを通じて、日々のアクティブな利用状況、機能の導入、アプリ内コンバージョンを促進します。

**KPI:**&#x200B;のエンゲージメント、リテンション、コンバージョン率

## 戦術的なユースケース

このパターンの一般的な戦術的な実装は次のとおりです。

- ホームページ ヒーローパーソナライゼーション（ロイヤルティ層またはライフサイクルステージ別）：顧客が新規顧客、アクティブ顧客、リスクのある顧客、VIPの顧客のいずれであるかにもとづいて、異なるヒーローバナーを表示します
- 購入履歴にもとづく商品レコメンデーションカルーセル – 過去の購入データと商品の親和性スコアを使用して、関連性の高い商品を提案します
- 顧客セグメント別にパーソナライズされたプロモーションバナー – 価値の高い、リスクのある、新しい顧客セグメントに向けて、さまざまなプロモーションを表示します
- 機能の採用率にもとづくモバイルユーザー向けのアプリ内メッセージ – ユーザーの使用パターンにもとづいて、利用率の低い機能を誘導します
- アカウントダッシュボードでパーソナライズされたオファーを含むコンテンツカード – 顧客プロファイルに合わせてカスタマイズされた、永続的で却下できるオファー
- ロイヤルティプログラムのメンバーに、階層別の価格設定や特別割引を表示するなど、顧客層にもとづいてパーソナライズされた価格設定や割引表示を実現します
- オウンド製品にもとづくクロスセルのレコメンデーションウィジェット – 現在のポートフォリオにもとづいて補完的な製品またはサービスを提案します
- 興味にもとづいてパーソナライズされたナビゲーションやコンテンツの順序付け：示された好みにもとづいて、コンテンツモジュールやナビゲーション要素を並べ替える

## 主要業績評価指標

次のKPIは、このユースケースパターンの有効性を測定するのに役立ちます。

| KPI | 測定アプローチ | ベンチマークガイダンス |
| --- | --- | --- |
| Personalizationエンゲージメント率 | パーソナライズされたコンテンツ要素のクリック数とインタラクション数（インプレッション数で割る） | パーソナライズされたコンテンツは、デフォルトのコンテンツを20～50%上回る |
| コンバージョン率の向上 | パーソナライズされたエクスペリエンスのコンバージョン率と、制御/デフォルトのエクスペリエンスの比較 | パーソナライズされていない体験を10～30%向上 |
| CTR （クリックスルー率） | パーソナライズされたCTA、オファー、レコメンデーションのクリック数をインプレッション数で割った値 | サーフェスごと（web、アプリ内、コンテンツカード）およびセグメントごとに監視 |
| 1訪問あたりの売上高 | パーソナライズされたエクスペリエンスによるセッションによる売上 | パーソナライズされた訪問者とパーソナライズされていない訪問者のグループの比較 |
| コンテンツカードのインタラクション率 | コンテンツカードのクリック数と却下数（インプレッション数を基準） | カードの種類とオーディエンスセグメントごとに追跡 |
| アプリ内メッセージエンゲージメント | インプレッションに対するアプリ内メッセージのインタラクション（CTAのクリック、却下） | オーディエンスセグメントとメッセージタイプの比較 |
| ページ滞在時間 | パーソナライズされたコンテンツを提供したページに費やす平均時間とデフォルトのページ比較 | パーソナライズされたページで、滞在時間を増加できます |
| オファーの承認率 | コンバージョンイベントの結果として決定で選択されたオファーの割合 | オファー、プレースメント、ランキング戦略別に追跡 |

## アプリケーション

このユースケースパターンでは、次のアプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO）** — web チャネル設定、アプリ内チャネル設定、コンテンツカードチャネル設定、決定（オファーの選択とランキング）、メッセージ作成（パーソナライズされたコンテンツの作成）、キャンペーン実行、コンテンツ実験、レポート
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** — オーディエンスの評価（エッジ、ストリーミング、バッチ）、Edge Networkを介したリアルタイムのプロファイル検索、計算属性と傾向スコアによるプロファイルエンリッチメント
- **[!DNL Adobe Experience Platform]（AEP）** — プロファイルストア、ID サービス、Web SDK、モバイル SDK、データストリーム設定、エッジネットワーク配信

## 関連ドキュメント

次のリソースでは、このガイドで参照されているテクノロジーと設定に関する追加の詳細を提供します。

### web チャネルのパーソナライゼーション

- [web チャネルの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [web エクスペリエンスの構築](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [web チャネル設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### アプリ内とコンテンツカードのチャネル

- [アプリ内チャネルの概要](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [アプリ内チャネルの前提条件](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [アプリ内メッセージの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [コンテンツカードチャネル](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [コンテンツカード設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [コンテンツカードの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### 意思決定管理

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalizationとコンテンツ

- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [ヘルパー関数](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツフラグメントの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### オーディエンスとセグメンテーション

- [セグメント サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [エッジセグメント化](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language リファレンス](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### IDとプロファイル

- [ID サービスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [ID グラフのリンクルール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [結合ポリシーの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### データ収集とSDK

- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Web SDKのインストール](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [モバイル SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network Server APIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### キャンペーンと実験

- [キャンペーンの基本を学ぶ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [コンテンツ実験を始める](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [コンテンツ実験を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [コンテンツ実験レポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### 計算属性とエンリッチメント

- [計算属性の概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [計算属性UI ガイド](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Customer AIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### レポートと分析

- [キャンペーンのライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [AJO + CJA統合ガイド](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJAの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### ガバナンスとプライバシー

- [データガバナンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Journey Optimizerでの同意](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### ガードレール

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ID サービスのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
