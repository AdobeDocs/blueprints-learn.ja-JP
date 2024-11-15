---
user-guide-title: デジタルエクスペリエンスのブループリント
breadcrumb-title: ブループリント
user-guide-description: ブループリントは、既存のビジネス上の問題に対処するための反復可能な実装で、アーキテクチャ図、技術上の考慮事項および関連ドキュメントリンクが含まれます。
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: 6a13de73d7f61295092faccfc21172f5e188331d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 54%

---


# デジタルエクスペリエンスのブループリント {#architecture}

+ [デジタルエクスペリエンスブループリント](/help/blueprints/overview.md)
+ 業界の垂直的なブループリント {#vertical-blueprints}
   + [概要](/help/blueprints/vertical-blueprints/overview.md)
   + [アパレル](/help/blueprints/vertical-blueprints/apparel.md)
   + [小売](/help/blueprints/vertical-blueprints/retail.md)
   + [通信業](/help/blueprints/vertical-blueprints/telecommunications.md)
   + [旅行およびホスピタリティ](/help/blueprints/vertical-blueprints/travel-hospitality.md)
+ アーキテクチャの概要 {#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platformとアプリケーション](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platformデータフロー](/help/blueprints/experience-platform/platform-data-flow.md)
   + デプロイメント {#deployment}
      + [Experience PlatformWeb SDK （&amp; [!DNL Edge Network]）](/help/blueprints/experience-platform/deployment/websdk.md)
      + [アプリケーション SDK](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [ガードレール](/help/blueprints/experience-platform/deployment/guardrails.md)
+ オーディエンスとプロファイルのアクティベーション {#audience-activation}
   + [概要](/help/blueprints/audience-activation/overview.md)
   + [匿名オーディエンスアクティベーション](/help/blueprints/audience-activation/anonymous.md)
   + 既知の顧客のアクティベーション（RTCDP） {#known-customer-audience-activation}
      + [概要](/help/blueprints/audience-activation/known.md)
      + [ソーシャルおよび広告チャネルに対するアクティベーション](/help/blueprints/audience-activation/advertising-activation.md)
      + [ファイルおよびエンタープライズストリーミング宛先に対するアクティベーション](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [顧客アクティビティハブ](/help/blueprints/audience-activation/customer-activity.md)
      + [セグメントの一致](/help/blueprints/audience-activation/segment-match.md)
   + [Experience Cloudアプリケーションを使用したアクティベーション](/help/blueprints/audience-activation/platform-and-applications.md)
   + Web およびモバイルのパーソナライゼーション{#web-personalization}
      + [概要](/help/blueprints/audience-activation/web-personalization/overview.md)
      + [行動パーソナライゼーション - Target](/help/blueprints//audience-activation/web-personalization/behavioral.md)
      + [既知の顧客パーソナライゼーション - Target と RTCDP](/help/blueprints/audience-activation/web-personalization/known-personalization.md)
      + [意思決定管理](/help/blueprints/audience-activation/web-personalization/decision-management-edge.md)
+ B2B アクティベーションとマーケティング{#b2b-activation}
   + [概要](/help/blueprints/b2b/overview.md)
   + [B2B 活性化](/help/blueprints/b2b/b2bactivation.md)
   + [B2B アカウントの有効化](/help/blueprints/b2b/b2b-account-activation.md)
   + [購入グループベースのマーケティングとジャーニー管理](/help/blueprints/b2b/b2b-buying-group-journeys.md)
   + Marketo Engage と Workfront 統合ブループリント{#marketo-engage-and-workfront-integration-blueprint}
      + [概要](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [取り込みと作成](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [レビューして承認](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [顧客の成功事例](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
+ コンテンツとCommerce{#content-commerce}
   + [Adobe Commerceと RTCDP](/help/blueprints/content-commerce/commerce/commerce-rtcdp.md)
+ Customer Journey Analytics {#customer-journey-analytics}
   + [概要](/help/blueprints/customer-journey-analytics/overview.md)
   + [CJA オーディエンスと RTCDP の共有](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA と Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ カスタマージャーニー{#customer-journeys}
   + [概要](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer{#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer.md)
      + 意思決定管理{#decision-management}
         + [概要](/help/blueprints/customer-journeys/decision_management/decision-management-overview.md)
         + [エッジでの意思決定管理](/help/blueprints/customer-journeys/decision_management/decision-management-edge.md)
         + [ハブでの意思決定管理](/help/blueprints/customer-journeys/decision_management/decision-management-hub.md)
      + [Journey Optimizer と Adobe Campaign](/help/blueprints/customer-journeys/ajo-and-campaign.md)
      + [サードパーティメッセージ](/help/blueprints/customer-journeys/3rd-party-messaging.md)
   + Campaign Standard{#campaign-standard}
      + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja){target="_blank"}
      + [AdobeのReal-Time CDP [!DNL Campaign Standard]](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ja){target="_blank"}
   + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Real-Time CDPとAdobe [!DNL Campaign] v8](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer と Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7{#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDPとAdobe [!DNL Campaign] v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Journey OptimizerとAdobe [!DNL Campaign] v7](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ データ収集、アクセスおよび書き出し {#data-ingestion}
   + [概要](/help/blueprints/data-ingestion/overview.md)
   + [複数サンドボックスイベント転送のデータ収集](/help/blueprints/data-ingestion/multi-sandbox-event-forwarding.md)
   + [データの準備と取り込み](/help/blueprints/data-ingestion/ingestion.md)
   + [データアクセスと書き出し](/help/blueprints/data-ingestion/egress.md)
   + [イベント転送](/help/blueprints/data-ingestion/server-side-collection.md)
+ データ分析、インテリジェンス、AI／ML {#data-exploration}
   + [概要](/help/blueprints/data-insights/overview.md)
   + [データ分析とインテリジェンス](/help/blueprints/data-insights/analysis.md)
   + [プロファイルエンリッチメントのためのカスタムデータサイエンス](/help/blueprints/data-insights/data-science.md)
