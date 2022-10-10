---
user-guide-title: デジタルエクスペリエンスブループリント
breadcrumb-title: ブループリント
user-guide-description: ブループリントは、既存のビジネス上の問題に対処するための反復可能な実装で、アーキテクチャ図、技術上の考慮事項および関連ドキュメントリンクが含まれます。
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: 6901596cbb661ffa8cf57c6ae958db1978bf1520
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 80%

---


# デジタルエクスペリエンスブループリント {#architecture}

+ [概要](/help/blueprints/overview.md)
+ 業界の垂直ブループリント{#vertical-blueprints}
   + [概要](/help/blueprints/vertical-blueprints/overview.md)
   + [アパレル](/help/blueprints/vertical-blueprints/apparel.md)
   + [小売](/help/blueprints/vertical-blueprints/retail.md)
   + [通信業](/help/blueprints/vertical-blueprints/telecommunications.md)
   + [観光および接客業](/help/blueprints/vertical-blueprints/travel-hospitality.md)
+ アーキテクチャの概要 {#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform およびアプリケーション](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platform データフロー](/help/blueprints/experience-platform/platform-data-flow.md)
   + デプロイメントパターン{#deployment}
      + [Experience Platform Web SDK および Edge ネットワーク](/help/blueprints/data-ingestion/websdk.md)
      + [アプリケーション SDK](/help/blueprints/data-ingestion/appsdk.md)
+ オーディエンスとプロファイルのアクティベーション {#audience-activation}
   + [概要](/help/blueprints/audience-activation/overview.md)
   + [匿名オーディエンスアクティベーション(AAM)](/help/blueprints/audience-activation/anonymous.md)
   + 既知の顧客のアクティベーション（RTCDP）{#known-customer-audience-activation}
      + [概要](/help/blueprints/audience-activation/known.md)
      + ソーシャルおよび広告チャネルに対するアクティベーション {#audience-activation}
         + [Facebook Custom Audiences へのアクティベーション](/help/blueprints/audience-activation/destinations/facebook.md)
         + [Google Customer Match へのアクティベーション](/help/blueprints/audience-activation/destinations/gcm.md)
      + [ファイルとエンタープライズストリーミング宛先に対するアクティベーション](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [顧客アクティビティハブ](/help/blueprints/audience-activation/customer-activity.md)
      + [セグメントの一致](/help/blueprints/audience-activation/segment-match.md)
   + [Experience Cloud アプリケーションを使用したアクティベーション](/help/blueprints/audience-activation/platform-and-applications.md)
+ B2B アクティベーションとマーケティング {#b2b-activation}
   + [概要](/help/blueprints/b2b/overview.md)
   + [B2B アクティベーション](/help/blueprints/b2b/b2bactivation.md)
+ Customer Journey Analytics {#customer-journey-analytics}
   + [概要](/help/blueprints/customer-journey-analytics/overview.md)
   + [CJA オーディエンスを RTCDP に共有する](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA と Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ カスタマージャーニー {#customer-journeys}
   + [概要](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer {#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer.md)
      + 意思決定管理 {#decision-management}
         + [概要](/help/blueprints/customer-journeys/decision_management/decision-management-overview.md)
         + [エッジでの意思決定管理](/help/blueprints/customer-journeys/decision_management/decision-management-edge.md)
         + [ハブでの意思決定管理](/help/blueprints/customer-journeys/decision_management/decision-management-hub.md)
      + [Journey Optimizer と Adobe Campaign](/help/blueprints/customer-journeys/ajo-and-campaign.md)
      + [サードパーティのメッセージング](/help/blueprints/customer-journeys/3rd-party-messaging.md)
   + Campaign Standard{#campaign-standard}
      + [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html)
      + [Real-Time CDPとAdobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html)
   + Campaign v8 {#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Adobe Campaign v8 とのReal-Time CDP](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Adobe Campaign v8 とのJourney Optimizer](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7 {#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP と Adobe Campaign v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Adobe Campaign v7 とのJourney Optimizer](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ データの取り込みとデータの書き出し{#data-ingestion}
   + [概要](/help/blueprints/data-ingestion/overview.md)
   + [データの準備と取り込み](/help/blueprints/data-ingestion/ingestion.md)
   + [イベント転送](/help/blueprints/data-ingestion/server-side-collection.md)
   + [マルチサンドボックスデータ収集](/help/blueprints/data-ingestion/multi-sandbox-data-collection.md)
+ データ分析、インテリジェンス、AI／ML {#data-exploration}
   + [概要](/help/blueprints/data-insights/overview.md)
   + [データ分析とインテリジェンス](/help/blueprints/data-insights/analysis.md)
   + [プロファイルエンリッチメントのためのカスタムデータサイエンス](/help/blueprints/data-insights/data-science.md)
+ Web およびモバイルパーソナライズ機能 {#web-personalization}
   + [概要](/help/blueprints/web-personalization/overview.md)
   + [行動によるパーソナライズ機能- Target](/help/blueprints/web-personalization/behavioral.md)
   + [既知の顧客のパーソナライズ機能 — Target と RTCDP](/help/blueprints/web-personalization/known-personalization.md)
   + [意思決定管理](/help/blueprints/web-personalization/decision-management-edge.md)