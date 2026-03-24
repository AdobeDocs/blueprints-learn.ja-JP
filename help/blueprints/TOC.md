---
user-guide-title: 顧客体験オーケストレーション ビジネス目標、ユースケース、アーキテクチャ図、ブループリント
breadcrumb-title: ユースケースとブループリント
user-guide-description: Adobe Experience Platformとそのアプリケーションについて、主要なビジネス目標、ユースケースパターン、業界のユースケースを確認できます。 ビジュアルアーキテクチャ図とブループリントは、システム統合、データフロー、ソリューション設計のための技術参照情報を提供し、ビジネス価値と導入を結び付けます。
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: abed39b6b6f63f2eef6cb36b400319910f8cf472
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 25%

---


# 顧客体験オーケストレーションの設計図 {#architecture}

+ [顧客体験オーケストレーションの設計図](/help/blueprints/overview.md)
+ AEPとアプリの主なビジネス目標{#business-objectives}
   + [概要](/help/blueprints/business-objectives/overview.md)
   + 獲得と成長{#acquisition-growth}
      + [新規顧客の獲得](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)
      + [リードジェネレーションの増加](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)
      + [Web サイトのエンゲージメントの向上](/help/blueprints/business-objectives/acquisition-growth/increase-website-engagement.md)
   + 収益/収益化{#revenue-monetization}
      + [コンバージョン率の向上](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)
      + [売上と売上を増加](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)
      + [クロスセルとアップセルの売上向上](/help/blueprints/business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)
      + [顧客ロイヤルティと生涯価値の向上](/help/blueprints/business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)
   + コストと効率性{#cost-efficiency}
      + [顧客獲得コストの削減](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)
      + [マーケティングの支出とROIの最適化](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)
      + [データ品質とガバナンスを改善](/help/blueprints/business-objectives/cost-efficiency/improve-data-quality-governance.md)
      + [マーケティングテクノロジーの統合と近代化](/help/blueprints/business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)
   + 顧客体験{#customer-experience-objectives}
      + [パーソナライズされた顧客体験の実現](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)
      + [顧客維持率の向上](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)
      + [顧客オンボーディングの改善](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)
      + [放棄されたカートとジャーニーを復元する](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)
   + 分析/インサイト{#analytics-insights}
      + [分析とレポートの改善](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)
      + [データにもとづく意思決定](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)
      + [マーケティングアトリビューションの改善](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)
   + クオリフィケーションとセールス（B2B）{#qualification-sales-b2b}
      + [リードのクオリフィケーションとコンバージョンを向上](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)
      + [顧客エンゲージメントの向上](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)
+ ユースケースパターン{#use-case-patterns}
   + [概要](/help/blueprints/use-case-patterns/overview.md)
   + オーディエンスの構築と活用{#audience-building-activation}
      + [Audience Activationから宛先へ](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)
      + [Segment Match を使用した Audience Collaboration](/help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md)
      + [イベント転送](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md)
      + [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md)
   + パーソナライズ機能{#personalization-patterns}
      + [匿名訪問者の Web Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
      + [既知の訪問者の Web/アプリPersonalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
      + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
      + [行動の推奨事項](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
   + キャンペーン管理とオーケストレーション{#campaign-orchestration-patterns}
      + [バッチ送信メッセージの有効化](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
      + [イベントトリガーメッセージ](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
      + [複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
      + [Decisioning を使用したクロスチャネルジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
      + [購買グループベースのマーケティングおよびジャーニー管理](/help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md)
   + 分析{#analysis-patterns}
      + [Customer Analytics &amp; Insightの生成](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
      + [B2B 分析](/help/blueprints/use-case-patterns/analysis/b2b-analytics.md)
   + 会話体験{#conversational-experience-patterns}
      + [Brand Concierge会話体験](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md)
+ 業界のユースケース{#industry-use-cases}
   + [ユースケースカタログ](/help/blueprints/industry-use-cases/use-case-catalog.md)
   + [自動車用](/help/blueprints/industry-use-cases/automotive/automotive-overview.md)
   + [B2B](/help/blueprints/industry-use-cases/b2b/b2b-overview.md)
   + [金融サービス](/help/blueprints/industry-use-cases/financial-services/financial-services-overview.md)
   + [ヘルスケア](/help/blueprints/industry-use-cases/healthcare/healthcare-overview.md)
   + [保険](/help/blueprints/industry-use-cases/insurance/insurance-overview.md)
   + [メディアとエンターテイメント](/help/blueprints/industry-use-cases/media-entertainment/media-entertainment-overview.md)
   + [小売](/help/blueprints/industry-use-cases/retail/retail-overview.md)
   + [通信](/help/blueprints/industry-use-cases/telecommunications/telecommunications-overview.md)
   + [テクノロジー](/help/blueprints/industry-use-cases/technology/technology-overview.md)
   + [旅行およびホスピタリティ](/help/blueprints/industry-use-cases/travel-hospitality/travel-hospitality-overview.md)
+ アーキテクチャ図とブループリント{#architecture-diagrams}
   + アーキテクチャの概要{#architecture-overview}
      + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
      + [Experience Platformとアプリケーション](/help/blueprints/experience-platform/platform-applications.md)
      + [Experience Platform データフロー](/help/blueprints/experience-platform/platform-data-flow.md)
      + [Experience Platformのガードレール](/help/blueprints/experience-platform/guardrails.md)
      + デプロイメント{#deployment}
         + [Experience Platform Web SDK &amp; [!DNL Edge Network]](/help/blueprints/experience-platform/deployment/websdk.md)
         + [アプリケーション SDK](/help/blueprints/experience-platform/deployment/appsdk.md)
   + オーディエンスとプロファイルのアクティベーション{#audience-activation}
      + [デバイスベース - Audience Managerによる匿名オーディエンスターゲティング](/help/blueprints/audience-activation/audience-manager.md)
      + Real-Time Customer Data Platform（RTCDP） {#known-customer-audience-activation}
         + [ソーシャルおよび広告の宛先へのオーディエンスのアクティベーション](/help/blueprints/audience-activation/advertising-activation.md)
         + [オーディエンスとプロファイルのエンタープライズ配信先へのアクティベーションの設計図](/help/blueprints/audience-activation/enterprise-destinations.md)
         + [サポートとセールスのシナリオのためのリアルタイムのプロファイルアクセス](/help/blueprints/audience-activation/customer-activity.md)
         + [webとモバイルのパーソナライゼーションのためのリアルタイムのエッジプロファイルアクセス](/help/blueprints/audience-activation/real-time-lookup.md)
         + [Segment Matchによるオーディエンスの共同作業](/help/blueprints/audience-activation/segment-match.md)
         + [Adobe Targetによる既知の顧客パーソナライゼーション](/help/blueprints/audience-activation/rtcdp-target.md)
         + [プロファイルエンリッチメントのためのカスタムデータサイエンス](/help/blueprints/audience-activation/data-science.md)
   + B2B アクティベーション/マーケティング{#b2b-activation}
      + [概要](/help/blueprints/b2b/overview.md)
      + [B2B アクティベーション](/help/blueprints/b2b/b2bactivation.md)
      + [B2B アカウントのアクティベーション](/help/blueprints/b2b/b2b-account-activation.md)
      + [購買グループベースのマーケティングとジャーニー管理](/help/blueprints/b2b/b2b-buying-group-journeys.md)
      + [Marketoデータを活用したB2B ジャーニー](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
      + [B2B有料メディアコントローラー](/help/blueprints/b2b/ajo-b2b-paid-media-controller.md)
      + Marketo EngageとWorkfrontの連携の設計図{#marketo-engage-and-workfront-integration-blueprint}
         + [概要](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
         + [受注と作成](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
         + [レビューと承認](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
         + [顧客の成功事例](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
   + Customer Journey Analytics{#customer-journey-analytics}
      + [概要](/help/blueprints/customer-journey-analytics/overview.md)
      + [B2B Customer Journey Analytics](/help/blueprints/customer-journey-analytics/b2b-cja.md)
      + [RTCDPへのCJA オーディエンスの共有](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
      + [CJA と Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
      + [データ分析とインテリジェンス](/help/blueprints/customer-journey-analytics/analysis.md)
   + カスタマージャーニー{#customer-journeys}
      + [概要](/help/blueprints/customer-journeys/overview.md)
      + Journey Optimizer{#journey-optimizer}
         + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
         + [AJO ジャーニー](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md)
         + [AJO キャンペーン](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md)
         + [サードパーティーメッセージ](/help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md)
      + 意思決定管理{#decision-management}
         + [概要](/help/blueprints/customer-journeys/decision-management/decision-management-overview.md)
         + [Edgeの意思決定管理](/help/blueprints/customer-journeys/decision-management/decision-management-edge.md)
         + [Hub上の意思決定管理](/help/blueprints/customer-journeys/decision-management/decision-management-hub.md)
      + Campaign v8{#campaign-v8}
         + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md)
         + [Adobeを使用したReal-Time CDP [!DNL Campaign] v8](/help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md)
         + [Journey Optimizer と Adobe Campaign v8](/help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md)
      + 非推奨のブループリント{#deprecated-blueprints}
         + Campaign Standard{#campaign-standard}
            + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/ja/docs/campaign-standard){target="_blank"}
            + [Real-Time CDPとAdobe [!DNL Campaign Standard]](https://experienceleague.adobe.com/ja/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
         + Campaign v7{#campaign-v7}
            + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)
