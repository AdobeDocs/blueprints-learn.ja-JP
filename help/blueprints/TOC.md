---
user-guide-title: Customer Experience Orchestration ブループリント
breadcrumb-title: 設計図
user-guide-description: ブループリントは、既存のビジネス上の問題に対処するための反復可能な実装で、アーキテクチャ図、技術上の考慮事項および関連ドキュメントリンクが含まれます。
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: ffef3a39ae84b85167a3b8b8a3622c76fb6cb251
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 25%

---


# Customer Experience Orchestration ブループリント {#architecture}

+ [カスタマーエクスペリエンスオーケストレーションのブループリント](/help/blueprints/overview.md)
+ アーキテクチャの概要{#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platformとアプリケーション](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platformのデータフロー](/help/blueprints/experience-platform/platform-data-flow.md)
   + [Experience Platform ガードレール](/help/blueprints/experience-platform/guardrails.md)
   + デプロイメント{#deployment}
      + [Experience Platform Web SDK（&amp; [!DNL Edge Network]）](/help/blueprints/experience-platform/deployment/websdk.md)
      + [アプリケーション SDK](/help/blueprints/experience-platform/deployment/appsdk.md)
+ オーディエンスとプロファイルのアクティベーション{#audience-activation}
   + [デバイスベース - Audience Managerを使用した匿名のオーディエンスターゲティング](/help/blueprints/audience-activation/audience-manager.md)
   + Real-Time Customer Data Platform（RTCDP） {#known-customer-audience-activation}
      + [ソーシャル宛先と広告宛先への Audience Activation](/help/blueprints/audience-activation/advertising-activation.md)
      + [エンタープライズ宛先のブループリントに対するオーディエンスとプロファイルのアクティベーション](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [サポートおよびセールスシナリオに対するリアルタイムのプロファイルアクセス](/help/blueprints/audience-activation/customer-activity.md)
      + [Web およびモバイルパーソナライゼーションのためのリアルタイムエッジプロファイルアクセス](/help/blueprints/audience-activation/real-time-lookup.md)
      + [Segment Match によるオーディエンスの共同作業](/help/blueprints/audience-activation/segment-match.md)
      + [Target を使用した既知の顧客パーソナライゼーション](/help/blueprints/audience-activation/rtcdp-target.md)
+ B2B アクティベーションおよびマーケティング{#b2b-activation}
   + [概要](/help/blueprints/b2b/overview.md)
   + [B2B 活性化](/help/blueprints/b2b/b2bactivation.md)
   + [B2B アカウントの有効化](/help/blueprints/b2b/b2b-account-activation.md)
   + [購入グループベースのマーケティングとジャーニー管理](/help/blueprints/b2b/b2b-buying-group-journeys.md)
   + [Marketo データを使用した B2B ジャーニー](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
   + [B2B Customer Journey Analytics](/help/blueprints/customer-journey-analytics/b2b-cja.md)
   + [B2B ペイド メディア コントローラー](/help/blueprints/b2b/ajo-b2b-paid-media-controller.md)
   + Marketo EngageとWorkfrontの統合ブループリント{#marketo-engage-and-workfront-integration-blueprint}
      + [概要](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [取り込みと作成](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [レビューして承認](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [顧客の成功事例](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
+ Content &amp; commerce{#content-commerce}
   + [Adobe CommerceとReal-Time CDP](/help/blueprints/content-commerce/commerce/commerce-rtcdp.md)
+ Customer Journey Analytics{#customer-journey-analytics}
   + [概要](/help/blueprints/customer-journey-analytics/overview.md)
   + [B2B Customer Journey Analytics](/help/blueprints/customer-journey-analytics/b2b-cja.md)
   + [RTCDPへのCJA オーディエンスの共有](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA と Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ カスタマージャーニー{#customer-journeys}
   + [概要](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer{#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
      + [AJO ジャーニー](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md)
      + [AJO キャンペーン](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md)
      + [サードパーティメッセージ](/help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md)
   + 意思決定管理{#decision-management}
      + [概要](/help/blueprints/customer-journeys/decision-management/decision-management-overview.md)
      + [Edgeの意思決定管理](/help/blueprints/customer-journeys/decision-management/decision-management-edge.md)
      + [ハブでの意思決定管理](/help/blueprints/customer-journeys/decision-management/decision-management-hub.md)
   + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md)
      + [Real-Time CDPとAdobe [!DNL Campaign] v8](/help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer と Adobe Campaign v8](/help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md)
   + 非推奨のブループリント{#deprecated-blueprints}
      + Campaign Standard{#campaign-standard}
         + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/en/docs/campaign-standard){target="_blank"}
         + [AdobeのReal-Time CDP [!DNL Campaign Standard]](https://experienceleague.adobe.com/en/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
      + Campaign v7{#campaign-v7}
         + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)
+ データ分析、インテリジェンス、AI／ML{#data-exploration}
   + [データ分析とインテリジェンス](/help/blueprints/data-insights/analysis.md)
   + [プロファイルエンリッチメントのためのカスタムデータサイエンス](/help/blueprints/data-insights/data-science.md)
