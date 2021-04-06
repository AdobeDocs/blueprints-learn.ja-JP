---
title: オンライン/オフラインのウェブパーソナライゼーションシナリオ
description: Webパーソナライゼーションを電子メールや、既知の匿名チャネルパーソナライゼーションと同期します。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
translation-type: tm+mt
source-git-commit: 2daba1965d6dce011bcce924f8e7471d7dfd42fb
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# オンライン/オフラインのウェブパーソナライゼーションシナリオ

Webパーソナライゼーションを電子メールや、既知の匿名チャネルパーソナライゼーションと同期します。

## 使用例

* ランディングページ最適化
* 行動分析およびオフラインプロファイルのターゲティング
* トランザクション、忠誠度、CRMデータ、モデル化されたインサイトなどのオフラインのインサイトに加え、旧製品/コンテンツ表示、製品/コンテンツアフィニティ、環境属性、サードパーティオーディエンスデータ、人口統計に基づくパーソナライズ

## アプリ

* リアルタイム顧客データプラットフォーム
* Adobe Target
* Adobe Audience Manager（オプション）:サードパーティのオーディエンスデータ、Co-opベースのデバイスグラフ、Adobe Analyticsでのプラットフォームセグメントの表示機能、プラットフォームでのAdobe Analyticsセグメントの表示機能を追加
* Adobe Analytics（オプション）:過去の行動データに基づくセグメントの作成機能と、Adobe Analyticsのデータに基づく細かい分類機能が追加されました。

## 建築

<img src="assets/onoff.svg" alt="オンライン/オフラインのウェブパーソナライゼーションシナリオのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* Experience Platform間で共有されるセグメントは、セグメントの実現から数分以内に共有されます。セグメントの実現は、ストリーミングまたはバッチの評価の方法を使用して行われます。 Experience PlatformとAudience Managerの間で、Experience PlatformセグメントのメンバーシップがAudience Managerプロファイルで実現され始めるまでに、約4時間の初期セグメント設定の同期が行われます。 Audience Managerプロファイルに入ると、Experience PlatformセグメントのメンバーシップをAdobe Target経由で同じページパーソナライゼーションで使用できます。
* Experience PlatformとAudience Managerの間の4時間のセグメント構成同期内に発生するセグメント実現に関しては、これらのセグメント実現は、後続のバッチセグメントジョブで「既存の」セグメントとしてAudience Managerされます。
* Experience Platformからのバッチセグメント共有 — 1日に1回、またはAPIを使用して手動で開始。 これらのセグメントのメンバーシップが認識されると、数分以内にAudience Managerに共有され、ターゲット内の同じ/次のページのパーソナライゼーションに使用できます。
* ストリーミングセグメントは約5分以内に実現されます。 これらのセグメントの再分割が行われると、数分以内にAudience Managerに共有され、ターゲット内の同じ/次のページのパーソナライゼーションに使用できます。
* デフォルトでは、セグメント共有サービスでは、各Adobe Analyticsレポートスイートで最大75オーディエンスを共有できます。 お客様がAudience Managerライセンスを持っている場合、Adobe AnalyticsとAdobe Target、Audience ManagerとAdobe Targetの間で共有できるオーディエンスの数に制限はありません。

## 導入の前提条件

| 申し込み/サービス | 必要なライブラリ | メモ |
|---|---|---|
| Adobe Target | プラットフォームWeb SDK*、at.js 0.9.1以降、またはmbox.js 61+ | at.jsは、mbox.jsが開発されなくなったので、推奨されます。 |
| Adobe Audience Manager（オプション） | プラットフォームWeb SDK*またはdil.js 5.0+ |  |
| Adobe Analytics（オプション） | プラットフォームWeb SDK*またはAppMeasurement.js 1.6.4以降 | Adobe Analyticsの追跡では、地域データ収集(RDC)を使用する必要があります。 |
| Experience CloudIDサービス | プラットフォームWeb SDK*またはVisitorAPI.js 2.0以降 | （推奨）Experience Platform Launchを使用してIDサービスをデプロイし、アプリケーションが呼び出される前にIDが確実に設定されるようにします |
| Experience PlatformモバイルSDK（オプション） | iOSおよびAndroid™の場合は4.11以降 |  |
| Experience PlatformWeb SDK | 1.0、現在のExperience PlatformSDKバージョンでは、[様々な使用例がExperience Cloudアプリケーションでまだサポートされていません](https://github.com/adobe/alloy/projects/5) |  |


## 導入手順

1. [Webアプリケーションまたはモバイルアプリケ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) ーション用のAdobeターゲットの実装
1. [Adobe Audience Managerの実装](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html) （オプション）
1. [Adobe Analyticsの実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)  （オプション）
1. [Experience Platformとリアルタイムの顧客プロファイルの実装](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)
1. [Experience CloudIDサービス](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html)または[Experience PlatformWeb SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)を実装します
   >[!NOTE]
   >
   >各アプリケーションでExperience CloudIDを使用し、同じExperience Cloud組織に属している必要があります。これにより、複数のアプリケーション間でオーディエンスを共有できます。
1. [Experience PlatformとAdobe Targetの間でのオーディエンス共有のプロビジョニングの要求(共有オーディエンス)](https://www.adobe.com/go/audiences)

## 導入データフロー図

Web/モバイルパーソナライゼーションのブループリントは、従来のアプリケーション固有のSDK（AppMeasurement.jsなど）を使用するか、プラットフォームのWeb SDK/モバイルSDKとEdge Networkを使用して実装できます。

### プラットフォームWeb/モバイルSDKとエッジアプローチ

<img src="assets/websdkflow.svg" alt="プラットフォームWeb SDK/モバイルSDKおよびエッジネットワークアプローチのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

### アプリケーション固有のSDKアプローチ

<img src="assets/appsdkflow.png" alt="アプリケーション固有のSDKアプローチのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## 関連ドキュメント

* [Audience Managerや他のExperience CloudソリューションとのExperience Platformセグメントの共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)
* [Experience Platformセグメントの概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [ストリーミングセグメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Experience Platformセグメントビルダーの概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html)
* [Audience Managerソースコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html)
* [AAMを介したAdobe Analyticsセグメントの共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)
* [Experience PlatformWeb SDKドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience CloudIDサービスドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html)
* [Experience Platform Launchドキュメント](https://experienceleague.adobe.com/docs/launch/using/home.html)

## 関連するブログ投稿

* [Adobe Experience Platformリアルタイム顧客プロファイルを使用したウェブパーソナライゼーションのBlueprint](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [最適なオンラインエクスペリエンスの構築：クエリサービスを備えたエンリッチ統合プロファイル](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [Adobe Experience Platform判定エンジンとAEM Webサイトの統合](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [Adobe Experience Platformのアイデンティティ・サービス — お客様のアイデンティティ問題の解決方法](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [Adobe Experience Platformの予測オーディエンスがパーソナライズされたエクスペリエンスをどのように改善するか](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [オーディエンス管理用Adobe Experience PlatformWeb SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [「Customer Zero」プログラムを使用したAdobe Experience Platformリアルタイム顧客プロファイルの導入](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [Journey Orchestrationサービスとモバイルメッセージングベンダーを使用して、顧客がモバイルメッセージをリアルタイムでパーソナライズできるAdobe Experience Platform](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [秒単位のセグメント：Adobe Experience Platformがリアルタイムの顧客プロファイルを実現した経緯](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [最適なオンラインエクスペリエンスの構築：クエリサービスを備えたエンリッチ統合プロファイル](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
