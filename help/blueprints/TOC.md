---
user-guide-title: 顧客体験オーケストレーション ビジネス目標、ユースケース、アーキテクチャ図、ブループリント
breadcrumb-title: ユースケースとブループリント
user-guide-description: Adobe Experience Platformとそのアプリケーションについて、主要なビジネス目標、ユースケースパターン、業界のユースケースを確認できます。 ビジュアルアーキテクチャ図とブループリントは、システム統合、データフロー、ソリューション設計のための技術参照情報を提供し、ビジネス価値と導入を結び付けます。
product: Adobe Experience Platform
mini-toc-levels: 3
role: Developer, User
nudge: orange
source-git-commit: 7f0b624616480cf563142c08eb0598d1dd55d551
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 15%
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
    + [サポートとセールスのためのリアルタイムのプロファイル検索](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md)
    + [プロファイル強化のためのカスタムデータサイエンス](/help/blueprints/use-case-patterns/audience-building-activation/data-science-profile-enrichment.md)
  + パーソナライズ機能{#personalization-patterns}
    + [匿名訪問者の Web Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
    + [既知の訪問者の Web/アプリPersonalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
    + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
    + [行動の推奨事項](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
    + [Web/Mobile PersonalizationのEdge プロファイルへのアクセス](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md)
    + [Adobe Targetによるオーディエンスの共有](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md)
  + キャンペーン管理とオーケストレーション{#campaign-orchestration-patterns}
    + [バッチ送信メッセージの有効化](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
    + [イベントトリガーメッセージ](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
    + [複数ステップの調整されたジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
    + [Decisioning を使用したクロスチャネルジャーニー](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
    + [Campaign v8 バッチオーケストレーションとトランザクションメッセージ](/help/blueprints/use-case-patterns/campaign-management-orchestration/campaign-v8-orchestration.md)
    + [Journey Optimizerとサードパーティメッセージの統合](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)
  + 分析{#analysis-patterns}
    + [Customer Analytics &amp; Insightの生成](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
  + B2B アクティベーションとマーケティング{#b2b-patterns}
    + [B2B Audience Activation](/help/blueprints/use-case-patterns/b2b/account-audience-activation.md)
    + [購買グループベースのマーケティングおよびジャーニー管理](/help/blueprints/use-case-patterns/b2b/buying-group-marketing.md)
    + [B2B 分析](/help/blueprints/use-case-patterns/b2b/account-analytics.md)
    + [Marketoデータを活用したB2Bジャーニー](/help/blueprints/use-case-patterns/b2b/marketo-data-journeys.md)
    + [AJO B2B Paid Media Controller](/help/blueprints/use-case-patterns/b2b/paid-media-orchestration.md)
    + [MarketoとWorkfrontの連携と作成](/help/blueprints/use-case-patterns/b2b/campaign-intake-and-creation.md)
    + [MarketoとWorkfrontのレビューと承認](/help/blueprints/use-case-patterns/b2b/campaign-review-and-approval.md)
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
    + [B2B オーディエンスとプロファイルのアクティベーション](/help/blueprints/b2b/b2b-audience-profile-activation.md)
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

+ ハンズオンラボ{#labs}
  + [ハンズオンラボの概要](/help/blueprints/labs/overview.md)
  + 実践的なワークショップ{#workshops}
    + AEP財団{#aep-foundations}
      + [概要](/help/blueprints/labs/aep-foundations/overview.md)
      + [セットアップ](/help/blueprints/labs/aep-foundations/setup.md)
      + サンドボックス設定{#aep-sandbox}
        + [Developer Console設定](/help/blueprints/labs/aep-foundations/sandbox-setup/developer-console-setup.md)
        + [デプロイメント手順](/help/blueprints/labs/aep-foundations/sandbox-setup/deployment-instructions.md)
      + Postman設定{#aep-postman}
        + [Postman インストール](/help/blueprints/labs/aep-foundations/postman-setup/postman-installation.md)
        + [環境ファイル](/help/blueprints/labs/aep-foundations/postman-setup/environment-file.md)
        + [API コレクション](/help/blueprints/labs/aep-foundations/postman-setup/api-collection.md)
        + [サンドボックスアクセス](/help/blueprints/labs/aep-foundations/postman-setup/sandbox-access.md)
        + [アクセストークン](/help/blueprints/labs/aep-foundations/postman-setup/access-token.md)
      + リアルタイムの顧客プロファイル{#aep-rtcp}
        + [講義](/help/blueprints/labs/aep-foundations/real-time-customer-profile/lectures.md)
        + プロファイルの検査{#aep-rtcp-inspect}
          + [概要](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/overview.md)
          + [プロファイルの基本](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-basics.md)
          + [結合ポリシー](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/merge-policies.md)
          + [プロファイルおよびID API](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-and-identity-apis.md)
      + LID手法{#aep-lid}
        + [前提条件](/help/blueprints/labs/aep-foundations/lid-methodology/prerequisites.md)
        + [ラベル](/help/blueprints/labs/aep-foundations/lid-methodology/label.md)
        + 特定{#aep-lid-identify}
          + [概要](/help/blueprints/labs/aep-foundations/lid-methodology/identify/overview.md)
          + [パート 1 – 残りのテーブルタイプ](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-1-remaining-table-types.md)
          + [パート 2 - キーフィールド](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-2-key-fields.md)
        + [非正規化](/help/blueprints/labs/aep-foundations/lid-methodology/denormalize.md)
      + XDM モデリング{#aep-xdm}
        + [講義](/help/blueprints/labs/aep-foundations/xdm-modeling/lectures.md)
        + UI モデリング{#aep-xdm-ui}
          + [概要](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/overview.md)
          + [ログインして参照](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/login-and-browse.md)
          + [モデル標準オブジェクト](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-standard-objects.md)
          + [カスタムオブジェクトのモデル化](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-custom-objects.md)
          + [プロファイル用に設定](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/configure-for-profile.md)
        + API モデリング{#aep-xdm-api}
          + [概要](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/overview.md)
          + スキーマの構築{#aep-xdm-api-build}
            + [概要](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/overview.md)
            + [標準フィールドグループを取得](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-standard-field-groups.md)
            + [カスタムフィールドグループの作成](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-custom-field-groups.md)
            + [プロファイルクラスを取得](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-profile-class.md)
            + [スキーマの作成](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-schema.md)
            + [スキーマの表示](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/view-schema.md)
            + [スキーマの変更 – JSON パッチ](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/modify-schema-json-patch.md)
          + Id フィールドをマーク{#aep-xdm-api-identity}
            + [概要](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/overview.md)
            + [プライマリ IDの作成](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-primary-identity.md)
            + [その他のIdの作成](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-other-identities.md)
            + [スキーマの表示](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/view-schema.md)
          + 関係の定義{#aep-xdm-api-relationships}
            + [概要](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/overview.md)
            + [プラン スキーマ IDを取得](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/get-plan-schema-id.md)
            + [スキーマ関係の作成](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-schema-relationship.md)
            + [プラン参照IDの作成](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-plan-reference-identity.md)
            + [スキーマの表示](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/view-schema.md)
          + [まとめ](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/recap.md)
        + Bonus Labs{#aep-xdm-bonus}
          + [APIによる自動化](/help/blueprints/labs/aep-foundations/xdm-modeling/bonus-labs/automate-with-apis.md)
      + データ取り込み{#aep-ingestion}
        + [講義](/help/blueprints/labs/aep-foundations/data-ingestion/lectures.md)
        + [ラボの概要](/help/blueprints/labs/aep-foundations/data-ingestion/lab-overview.md)
        + [サンプルファイル](/help/blueprints/labs/aep-foundations/data-ingestion/sample-files.md)
        + バッチ取り込み{#aep-ingestion-batch}
          + [概要](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/overview.md)
          + [データフローの作成](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-dataflow.md)
          + マッピングデータ{#aep-ingestion-batch-mapping}
            + [概要](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/overview.md)
            + [パススルーマッピングの修正](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/fix-passthrough-mappings.md)
            + [計算フィールド](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/calculated-fields.md)
            + [最終マッピングセットの確認](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/check-final-mapping-set.md)
          + [データフローの実行](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/run-dataflow.md)
          + [エラーのデバッグ](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/debugging-errors.md)
          + [新しいデータフローの作成](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-a-new-dataflow.md)
          + [エラーの修正](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/fixing-errors.md)
          + [検証と検証](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/verification-and-validation.md)
        + ストリーム取得{#aep-ingestion-stream}
          + [概要](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/overview.md)
          + [Sourceの設定](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/setup-source.md)
          + [マッピングの設定](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/configure-mapping.md)
          + [最終マッピングセットの確認](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/check-final-mapping-set.md)
          + [プロファイルのストリーム](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/stream-a-profile.md)
          + [取り込んだプロファイルを確認](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verify-ingested-profile.md)
          + [エラーの監視とデバッグ](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/monitoring-and-debugging-errors.md)
          + [検証と検証](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verification-and-validation.md)
        + Bonus Labs{#aep-ingestion-bonus}
          + [CreateDateのMAPPER エラーの修正](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/fix-mapper-errors-for-createdate.md)
          + [注文イベントのストリーム](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/stream-an-order-event.md)
          + データランディングゾーンの活用{#aep-ingestion-dlz}
            + [概要](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/overview.md)
            + [Sourceの設定](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/setup-source.md)
            + [マッピングの作成](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/create-mappings.md)
            + [データフローをスケジュール](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/schedule-dataflow.md)
            + [失敗したデータフローの再試行](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/retry-a-failed-dataflow.md)
            + 注文の読み込み{#aep-ingestion-dlz-orders}
              + [概要](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/overview.md)
              + [Sourceの設定](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/setup-source.md)
              + [初期マッピング](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/initial-mappings.md)
              + [オブジェクトコピーマッピング](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/object-copy-mappings.md)
              + [データフローの検証とスケジュール](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/verify-and-schedule-dataflow.md)
      + Segmentation and Activation{#aep-segmentation}
        + [講義](/help/blueprints/labs/aep-foundations/segmentation-and-activation/lecture.md)
        + Edgeのアクティベーション{#aep-segmentation-edge}
          + [概要](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/overview.md)
          + [Edge オーディエンスの作成](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/create-edge-audience.md)
          + [Edge イベントの送信](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/send-an-edge-event.md)
          + イベント転送の設定{#aep-segmentation-edge-ef}
            + [概要](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/overview.md)
            + [プロパティを作成](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-property.md)
            + [データストリームを作成](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-datastream.md)
      + オーディエンスの構築{#aep-audiences}
        + ユースケース 1 – 獲得{#aep-uc1}
          + [概要](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/overview.md)
          + 宛先の設定{#aep-uc1-destinations}
            + [Personalizationのカスタム配信先の設定](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-custom-personalization-destination.md)
            + [ストリーミング宛先の設定](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-streaming-destination.md)
          + [オーディエンスの構築1](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-1.md)
          + [オーディエンスの構築2](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-2.md)
          + [オーディエンスの構築3](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-3.md)
          + [Edge イベントの送信](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/send-an-edge-event.md)
          + [クリティカルシンキングのレビュー](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/critical-thinking-review.md)
        + ユースケース 2 - アップセル{#aep-uc2}
          + [概要](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/overview.md)
          + [事前作業](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/pre-work.md)
          + [オプション 1 - オーディエンスを使用した集計](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-1-using-audiences-to-aggregate.md)
          + [オプション 2 – 事前集計を使用する](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-2-use-pre-aggregates.md)
          + [クリティカルシンキングのレビュー](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/critical-thinking-review.md)
        + ユースケース 3 - アウトリーチ{#aep-uc3}
          + [概要](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/overview.md)
          + [ユースケースを構築3](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/build-use-case-3.md)
          + [クリティカルシンキングのレビュー](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/critical-thinking-review.md)
        + Bonus Labs{#aep-audiences-bonus}
          + [ハブへの注文イベントの送信](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-order-event-to-hub.md)
          + [Web イベントをハブに送信](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-web-event-to-hub.md)
          + [イベントの監視](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/monitor-your-event.md)
    + AJO財団{#ajo-foundations}
      + [概要](/help/blueprints/labs/ajo-foundations/overview.md)
      + [セットアップ](/help/blueprints/labs/ajo-foundations/setup.md)
      + サンドボックス設定{#ajo-sandbox}
        + [Developer Console設定](/help/blueprints/labs/ajo-foundations/sandbox-setup/developer-console-setup.md)
        + [デプロイメント手順](/help/blueprints/labs/ajo-foundations/sandbox-setup/deployment-instructions.md)
      + Postman設定{#ajo-postman}
        + [Postman インストール](/help/blueprints/labs/ajo-foundations/postman-setup/postman-installation.md)
        + [環境ファイルを読み込む](/help/blueprints/labs/ajo-foundations/postman-setup/import-environment-file.md)
        + [API コレクションのインポート](/help/blueprints/labs/ajo-foundations/postman-setup/import-api-collection.md)
      + 建築ビルディングブロック{#ajo-architecture}
        + [講義](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/lecture.md)
        + ユースケースのアーキテクチャへの割り当て{#ajo-architecture-mapping}
          + [概要](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/overview.md)
          + [Labの概要](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-introduction.md)
          + [ラボ演習](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-exercise.md)
          + [ラボレビュー](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-review.md)
      + データストア{#ajo-data-stores}
        + [リアルタイムの顧客プロファイルに関する講義](/help/blueprints/labs/ajo-foundations/data-stores/real-time-customer-profile-lecture.md)
        + Profile in Action{#ajo-profile}
          + [概要](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/overview.md)
          + [ログインして参照](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/login-and-browse.md)
          + [データストリームを作成](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/create-datastream.md)
          + [Edge Web イベントの送信](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/send-an-edge-web-event.md)
          + [ハブでプロファイルを検証](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-hub.md)
          + [Edgeでのプロファイルの検証](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-edge.md)
          + [データレイク上のイベントの検証](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-event-on-data-lake.md)
          + [プロファイルスナップショットの検証](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-snapshot.md)
          + [概要](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/summary.md)
        + [リレーショナルストア講義](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-lecture.md)
        + リレーショナルストアの実際{#ajo-relational}
          + [概要](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/overview.md)
          + [スキーマを参照](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/browse-schemas.md)
          + [Profile Target Dimension](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/profile-target-dimension.md)
          + [オーディエンスを読む](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/read-an-audience.md)
          + [概要](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/summary.md)
        + メールチャネルの設定{#ajo-email}
          + [概要](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/overview.md)
          + [プロファイル用に設定](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-profile.md)
          + [リレーショナル用に設定](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-relational.md)
          + [アクティブステータスの待機中](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/waiting-for-active-status.md)
      + 調整されたキャンペーン{#ajo-campaigns}
        + [メッセージ配信レクチャー](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-lecture.md)
        + メッセージ配信の実際{#ajo-campaigns-delivery}
          + [概要](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/overview.md)
          + [キャンペーンを作成](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/create-a-campaign.md)
          + [オーディエンスの構築](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/build-an-audience.md)
          + [フォークアクティビティを追加](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-fork-activity.md)
          + [メールアクティビティの追加](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-email-activities.md)
          + [キャンペーンのテスト](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/test-the-campaign.md)
          + [概要](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/summary.md)
        + [ワークフロービルディングブロックの講義](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/workflow-building-blocks-lecture.md)
        + 主力の電話機の起動{#ajo-campaigns-flagship}
          + [概要](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/overview.md)
          + [SMS チャネルの設定](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/configure-sms-channel.md)
          + [オーケストレーションされたキャンペーンの作成](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/create-an-orchestrated-campaign.md)
          + [オーディエンスの構築](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/build-an-audience.md)
          + [結果をフォーク](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/fork-the-result.md)
          + [オーディエンスを保存](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/save-the-audience.md)
          + [線をフィルタリング](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/filter-the-lines.md)
          + [SMSの作成](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/compose-the-sms.md)
          + [ワークフローの実行](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/run-the-workflow.md)
          + [概要](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/summary.md)
      + ジャーニー{#ajo-journeys}
        + [講義](/help/blueprints/labs/ajo-foundations/journeys/lecture.md)
        + 購入後の興奮{#ajo-journeys-post-purchase}
          + [概要](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/overview.md)
          + [イベントの設定](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-event.md)
          + [カスタムアクションの設定](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-custom-action.md)
          + [ビルドジャーニー](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/build-journey.md)
          + [テストジャーニー](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/test-journey.md)
          + [イベントの送信](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/send-an-event.md)
          + [取り込まれたイベントの検証](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-event-ingested.md)
          + [ジャーニーを検証](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-journey.md)
          + [概要](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/summary.md)
      + 決定{#ajo-decisioning}
        + [Experience Edge](/help/blueprints/labs/ajo-foundations/decisioning/experience-edge.md)
        + 決定事項の説明{#ajo-decisioning-explained}
          + [概要](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/overview.md)
          + [概要](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/introduction.md)
          + [決定項目XDM](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-xdm.md)
          + [決定項目作成](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-creation.md)
          + [コレクション](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/collections.md)
          + [ランキング式](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/ranking-formulas.md)
          + [選択戦略](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/selection-strategies.md)
          + [決定ポリシー](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-policies.md)
          + [ガードレール、AI モデルによる意思決定の未来](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/guardrails-ai-models-decisioning-future.md)
        + 放棄された参照{#ajo-decisioning-abandoned}
          + [概要](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/overview.md)
          + [決定ルールの作成](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-decision-rule.md)
          + [オファー属性の作成](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-attributes.md)
          + [オファーアイテムの作成](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-items.md)
          + [オファーコレクションを作成](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-collection.md)
          + [ランキング式の作成](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-ranking-formula.md)
          + [選択戦略の作成](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-selection-strategy.md)
          + [コードベースのエクスペリエンスチャネルの構築](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-code-based-experience-channel.md)
          + [ジャーニーの構築](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-the-journey.md)
          + [意思決定とCBEの実際](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/decisioning-and-cbes-in-action.md)
          + [概要](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/summary.md)
      + AIを活用したコンテンツ制作{#ajo-content-ai}
        + [講義](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/lecture.md)
        + [概要](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/overview.md)
        + [ブランド管理](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-management.md)
        + [コンテンツフラグメントの作成](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-fragments.md)
        + [コンテンツテンプレートの作成](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-template.md)
        + [電子メールの作成](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/creating-the-email.md)
        + [AI アシスタントとコンテンツPersonalization](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/ai-assistant-and-content-personalization.md)
        + [Personalizationとコンテンツのテスト](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/personalization-and-content-experimentation.md)
        + [コンテンツシミュレーション](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/content-simulation.md)
        + [ブランドの統一](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-alignment.md)
        + [電子メールのテスト](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/test-the-email.md)
        + [サマリ](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/summary.md)
