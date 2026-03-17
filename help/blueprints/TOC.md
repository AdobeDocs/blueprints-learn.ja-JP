---
user-guide-title: Customer Experience Orchestration のビジネス目標、ユースケース、アーキテクチャ図およびブループリント
breadcrumb-title: ユースケースとブループリント
user-guide-description: Adobe Experience Platformとアプリケーションの主なビジネス目標、ユースケースパターン、業界のユースケースについて説明します。 ビジュアルアーキテクチャの図とブループリントは、システム統合、データフロー、ソリューション設計のテクニカルリファレンスを提供し、ビジネス価値を実装に結び付けます。
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: 63154ca158b773287f0d1a7f88a81ac3181c43a0
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 12%

---


# Customer Experience Orchestration ブループリント {#architecture}

+ [Customer Experience Orchestration ブループリント](/help/blueprints/overview.md)
+ AEPとアプリの主なビジネス目標{#business-objectives}
   + [概要](/help/blueprints/business-objectives/overview.md)
   + 獲得と成長{#acquisition-growth}
      + [新規顧客の獲得](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)
      + [リードジェネレーションの向上](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)
      + [Web サイトエンゲージメントの向上](/help/blueprints/business-objectives/acquisition-growth/increase-website-engagement.md)
   + 収益と収益化{#revenue-monetization}
      + [コンバージョン率の向上](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)
      + [収益と売上の増加](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)
      + [クロスセルとアップセルの収益を促進](/help/blueprints/business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)
      + [顧客ロイヤルティと生涯価値の向上](/help/blueprints/business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)
   + コストと効率{#cost-efficiency}
      + [顧客獲得コストの削減](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)
      + [マーケティング費用と ROI の最適化](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)
      + [データ品質とガバナンスの向上](/help/blueprints/business-objectives/cost-efficiency/improve-data-quality-governance.md)
      + [マーケティングテクノロジーの統合と最新化](/help/blueprints/business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)
   + 顧客体験{#customer-experience-objectives}
      + [パーソナライズされた顧客体験の提供](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)
      + [顧客維持の向上](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)
      + [顧客のオンボーディングの改善](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)
      + [放棄された買い物かごとジャーニーの復元](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)
   + 分析とインサイト{#analytics-insights}
      + [分析とレポートの改善](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)
      + [データに基づく意思決定の有効化](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)
      + [マーケティングアトリビューションの改善](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)
   + 選定およびセールス（B2B）{#qualification-sales-b2b}
      + [リードの選定とコンバージョンの向上](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)
      + [顧客エンゲージメントの向上](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)
+ ユースケースパターン{#use-case-patterns}
   + [概要](/help/blueprints/use-case-patterns/overview.md)
   + オーディエンスの構築とアクティベーション{#audience-building-activation}
      + [Audience Activationから宛先へ](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)
      + [Segment Match を使用した Audience Collaboration](/help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md)
      + [イベント転送](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md)
      + [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md)
   + パーソナライズ機能{#personalization-patterns}
      + [匿名訪問者の Web Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
      + [既知の訪問者の Web/アプリPersonalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
      + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
      + [行動の推奨事項](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
   + キャンペーンの管理とオーケストレーション{#campaign-orchestration-patterns}
      + [バッチ送信メッセージの有効化](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
      + [イベントトリガーメッセージ](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
      + [複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
      + [Decisioning を使用したクロスチャネルジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
      + [購買グループベースのマーケティングおよびジャーニー管理](/help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md)
   + 分析{#analysis-patterns}
      + [Customer Analytics &amp; Insightの生成](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
      + [B2B 分析](/help/blueprints/use-case-patterns/analysis/b2b-analytics.md)
   + 会話経験{#conversational-experience-patterns}
      + [Brand Concierge会話体験](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md)
+ 業界の使用例{#industry-use-cases}
   + [ユースケースカタログ](/help/blueprints/industry-use-cases/use-case-catalog.md)
   + [自動車用](/help/blueprints/industry-use-cases/automotive/automotive-overview.md)
   + [B2B](/help/blueprints/industry-use-cases/b2b/b2b-overview.md)
   + [金融サービス](/help/blueprints/industry-use-cases/financial-services/financial-services-overview.md)
   + [ヘルスケア](/help/blueprints/industry-use-cases/healthcare/healthcare-overview.md)
   + [保険](/help/blueprints/industry-use-cases/insurance/insurance-overview.md)
   + [メディアとエンターテイメント](/help/blueprints/industry-use-cases/media-entertainment/media-entertainment-overview.md)
   + [小売](/help/blueprints/industry-use-cases/retail/retail-overview.md)
   + [通信](/help/blueprints/industry-use-cases/telecommunications/telecommunications-overview.md)
   + [旅行およびホスピタリティ](/help/blueprints/industry-use-cases/travel-hospitality/travel-hospitality-overview.md)
+ アーキテクチャ図とブループリント{#architecture-diagrams}
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
         + [プロファイルエンリッチメントのためのカスタムデータサイエンス](/help/blueprints/audience-activation/data-science.md)
   + B2B アクティベーションおよびマーケティング{#b2b-activation}
      + [概要](/help/blueprints/b2b/overview.md)
      + [B2B 活性化](/help/blueprints/b2b/b2bactivation.md)
      + [B2B アカウントの有効化](/help/blueprints/b2b/b2b-account-activation.md)
      + [購入グループベースのマーケティングとジャーニー管理](/help/blueprints/b2b/b2b-buying-group-journeys.md)
      + [Marketo データを使用した B2B ジャーニー](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
      + [B2B ペイド メディア コントローラー](/help/blueprints/b2b/ajo-b2b-paid-media-controller.md)
      + Marketo EngageとWorkfrontの統合ブループリント{#marketo-engage-and-workfront-integration-blueprint}
         + [概要](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
         + [取り込みと作成](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
         + [レビューして承認](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
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
            + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/ja/docs/campaign-standard){target="_blank"}
            + [AdobeのReal-Time CDP [!DNL Campaign Standard]](https://experienceleague.adobe.com/ja/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
         + Campaign v7{#campaign-v7}
            + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)
