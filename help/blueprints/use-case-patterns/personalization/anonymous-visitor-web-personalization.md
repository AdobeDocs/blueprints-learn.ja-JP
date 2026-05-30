---
title: 匿名訪問者の Web Personalization
description: セッション中の行動シグナルにもとづいて、未特定の訪問者にパーソナライズされたweb コンテンツを配信する方法を説明します。
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: e2446801-ffce-40e6-bfe9-abec623c9201
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 4%

---

# 匿名訪問者のweb パーソナライゼーション

このガイドでは、[!DNL Adobe Journey Optimizer] （AJO）、[!DNL Adobe Real-Time Customer Data Platform] （RT-CDP）、[!DNL Adobe Experience Platform] （AEP）を使用して、セッション中の行動シグナルに基づいて匿名（未識別）訪問者にパーソナライズされたweb コンテンツを配信する、匿名の訪問者web パーソナライゼーションのユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

このパターンは、限られたデータで動作します。現在のセッションで観察できるものと、同じデバイスまたはCookieを使用して以前の訪問から蓄積された匿名のエッジプロファイルだけです。 これにより、訪問者がアカウントを持っていない、または認証されていないfunnel上部のパーソナライゼーションに適しています。

## ユースケースパターン

次に、このユースケースのコアパターンと実行計画について説明します。

**匿名訪問者の Web Personalization**

AJOのweb チャネルを通じて、セッション中の行動シグナルにもとづいて、未特定の訪問者にパーソナライズされたコンテンツを提供します。

**実行計画：** Web サーフェス設定>動作ルール評価> コンテンツ配信> インプレッションの追跡> レポート

## ユースケースの概要

匿名訪問者のWeb Personalizationは、ログインしておらず、IDが不明で、統合された顧客プロファイルに解決できない、未特定のweb サイト訪問者に、関連性の高いパーソナライズされたコンテンツを配信する必要があります。 この制約にもかかわらず、閲覧ページ、サイト滞在時間、スクロールの深さ、紹介ソース、地理的な場所、デバイスタイプ、UTM キャンペーンパラメーターなどのセッション内の行動シグナルを活用することで、有意義なパーソナライゼーションを実現できます。

このパターンでは、AJOのweb チャネルサーフェスとコードベースのエクスペリエンスを使用して、ページコンテンツをリアルタイムで変更します。 Edgeによるセグメンテーションは、顧客がサイトを移動するたびに、それ以上の遅延で意思決定をおこなう必要があるため、主要な評価手法となります。 [!DNL Web SDK]は行動シグナルを収集して[!DNL AEP Edge Network]に送信し、エッジ評価されたオーディエンスルールによって、配信するコンテンツバリエーションが決定されます。

統合プロファイルとセグメントメンバーシップ全体を活用する既知の訪問者web/アプリのパーソナライゼーションとは異なり、このパターンは、現在のセッションで観察可能なデータと、訪問者のECID （[!DNL Experience Cloud ID]）に関連付けられた匿名のエッジプロファイルに制限されます。 この区別は、実装の計画に非常に重要です。パーソナライゼーションに使用できる行動シグナルは、[!DNL Web SDK]がキャプチャしたものと、cookie ベースのECIDを介したセッション間でエッジプロファイルストアに保持されるものに限定されます。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

**[web サイトのエンゲージメントの向上](../../business-objectives/acquisition-growth/increase-website-engagement.md)**

匿名の訪問者のシグナルに合わせてカスタマイズされた関連性の高いエクスペリエンスを通じて、サイトでの滞在時間、セッションごとのページ、web コンテンツとのインタラクションを改善します。

| KPI |
| --- |
| Web ページでの時間 |
| エンゲージメント |
| コンバージョン率 |

**[パーソナライズされた顧客体験の提供](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

個人の好み、行動、ライフサイクルの段階に合わせて、コンテンツ、オファー、メッセージを調整できます。自分の役割を特定できていない訪問者も含まれます。

| KPI |
| --- |
| エンゲージメント |
| コンバージョン率 |
| 顧客満足度（CSAT） |

**[コンバージョン率を向上](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

行動のコンテキストにもとづいて、最も関連性の高いコンテンツを表示することで、購入、サインアップ、フォーム送信などの望ましいアクションを実行した訪問者と見込み顧客の割合を向上させます。

| KPI |
| --- |
| コンバージョン率 |
| リードコンバージョン |
| Cpl （リード単価） |

## 戦術的なユースケース

次の例は、このパターンを適用できる特定のシナリオを示しています。

- **紹介ソースにもとづくランディングページの見出しのA/B テスト** — Google、ソーシャルメディア、またはダイレクトトラフィックから到着する訪問者に対して、異なる見出しをテストし、獲得チャネルによるエンゲージメントを最適化します
- **閲覧行動に基づくカテゴリー親和性レコメンデーション** – 現在のセッションで表示されたページに基づいて製品またはコンテンツのレコメンデーションを表示し、発見とコンバージョンを向上させます
- **離脱の意思を示すオファー** – 訪問者がサイトを離脱しようとしていることを示す行動シグナルが表示された場合、プロモーションオファーまたはリードキャプチャフォームを提示します
- **位置情報をターゲットにしたプロモーション バナー** – 訪問者の地理的な場所に基づいて、地域固有のプロモーション、店舗検索コンテンツ、地域オファーを表示します
- **デバイス別コンテンツレイアウト最適化** – 訪問者がデスクトップ、タブレット、モバイルのいずれを使用しているかに応じて、コンテンツレイアウト、画像サイズ、CTAの配置を調整します
- **新規訪問者と再訪問者のウェルカムメッセージ** – 初回訪問者のエクスペリエンスと、セッション全体でECID永続性を使用する再訪問者のエクスペリエンスを区別します
- **現在のセッションで閲覧したページに基づくコンテンツのレコメンデーション** – 訪問者が既に閲覧したページに基づいて、関連する記事、製品、リソースを動的に表示します
- **UTM キャンペーンパラメーターに基づく動的ヒーローバナー** – 参照元キャンペーンのメッセージまたはクリエイティブに合わせてヒーローバナーをパーソナライズします

## 主要業績評価指標

このユースケースパターンの有効性を測定するには、次のKPIを使用します。

| KPI | 説明 | 測定アプローチ |
| --- | --- | --- |
| Personalizationインプレッション率 | パーソナライズされたコンテンツが配信された、適格なページビューの割合 | AJOキャンペーンレポート：インプレッション数/ページビュー数 |
| CTR （クリックスルー率） | パーソナライズされたコンテンツインプレッションのうち、クリックに至った割合 | AJO キャンペーンレポート：クリック数/インプレッション数 |
| エンゲージメント向上 | パーソナライズされたコンテンツとデフォルトのコンテンツの比較による、ページ滞在時間の増加、セッションあたりのページ数、スクロール数の増加 | CJA workspaceとの比較：パーソナライズされたコホートと制御の違い |
| コンバージョン率 | パーソナライズされたコンテンツにアクセスし、望ましいアクションを完了した訪問者の割合 | CJA funnel analysis：インプレッション/インタラクション/コンバージョン |
| バウンス率の減少 | パーソナライズされたコンテンツを受け取る訪問者の、単一ページセッションの減少 | CJA session analysis：パーソナライズされた差分の直帰率とデフォルトの直帰率 |
| 実験の成功率 | 統計的に有意な勝者が得られたA/B テストの割合 | AJO実験レポート：信頼性のしきい値に達した実験 |

## アプリケーション

このユースケースパターンでは、次のアプリケーションを使用します。

- **[!DNL Adobe Journey Optimizer]（AJO）** — web チャネルサーフェスの設定、コンテンツオーサリング（webおよびコードベースのエクスペリエンス）、キャンペーンの実行、コンテンツ実験（A/B テスト）、意思決定（動的コンテンツ選択）、レポート
- **[!DNL Adobe Real-Time Customer Data Platform]（RT-CDP）** — セッション内の行動シグナルに基づくリアルタイムのオーディエンス評価のためのEdge セグメンテーション、匿名エッジプロファイル管理
- **[!DNL Adobe Experience Platform]（AEP）** — ビヘイビアーシグナル収集の[!DNL Web SDK]、リアルタイムデータルーティングおよびパーソナライゼーション配信の[!DNL Edge Network]、データストリーム設定

## アーキテクチャ

次のリファレンスアーキテクチャは、エッジで匿名の訪問者シグナルを収集し、オーディエンスルールと比較して評価し、パーソナライズされたコンテンツを配信するために使用する方法を示しています。

![匿名オーディエンスのアクティブ化とパーソナライゼーションのための参照アーキテクチャ &#x200B;](/help/blueprints/audience-activation/assets/anonymous_activation.png)

## 関連ドキュメント

次のExperience League リソースでは、このユースケースパターンで使用される機能に関する詳細を提供しています。

**Web チャネルとコードベースのエクスペリエンス**

- [web チャネルの基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/web/get-started-web)
- [web エクスペリエンスの構築](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/channels/web/create-web)
- [コードベースのエクスペリエンスチャネル](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [コードベースのエクスペリエンス設定](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

**オーディエンスとセグメント化**

- [セグメント サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/home)
- [セグメントビルダーUI ガイド](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder)
- [エッジセグメント化](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/edge-segmentation)
- [ストリーミングセグメンテーション](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language リファレンス](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/pql/overview)

**Personalizationとコンテンツ**

- [パーソナライゼーションの追加](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalizationの構文](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [動的コンテンツ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [コンテンツテンプレートの操作](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [コンテンツフラグメントの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

**コンテンツ実験**

- [コンテンツ実験を始める](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [コンテンツ実験を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [コンテンツ実験レポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [統計計算](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

**意思決定管理**

- [意思決定管理の概要](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [プレースメントの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [決定ルールの作成](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [パーソナライズされたオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [フォールバックオファーを作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [コレクションの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [決定を作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [ランキング戦略](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [メッセージでのオファーの配信](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

**キャンペーン**

- [キャンペーンの基本を学ぶ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [キャンペーンの作成](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

**[!DNL Web SDK]とデータ収集**

- [Web SDKの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/home)
- [Web SDKのインストール](https://experienceleague.adobe.com/ja/docs/experience-platform/web-sdk/install/overview)
- [データストリームの設定](https://experienceleague.adobe.com/ja/docs/experience-platform/datastreams/configure)
- [タグの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/tags/home)

**IDとプロファイル**

- [ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
- [ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)
- [結合ポリシーの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/merge-policies/overview)
- [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/home)

**データモデリング**

- [XDM システムの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/home)
- [スキーマ構成の基本](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/schema/composition)

**レポートと分析**

- [キャンペーンのライブレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [キャンペーングローバルレポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Customer Journey Analyticsの操作](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspaceの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-workspace/home)
- [CJAの概要](https://experienceleague.adobe.com/ja/docs/analytics-platform/using/cja-overview/cja-overview)

**データガバナンスとプライバシー**

- [データガバナンスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-governance/home)
- [高度なデータライフサイクル管理の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/data-lifecycle/home)
- [同意と環境設定のフィールドグループ](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/field-groups/profile/consents)

**ガードレール**

- [Journey Optimizerのガードレール](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)
- [リアルタイムの顧客プロファイルのガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/guardrails)
- [ID サービスのガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/guardrails)
