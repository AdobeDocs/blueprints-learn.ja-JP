---
title: オンライン/オフラインWebパーソナライゼーションのブループリント
description: web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
translation-type: tm+mt
source-git-commit: 9a52c5f9513e39b31956aaa0f30cad1426b63a95
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 48%

---

# オンライン/オフラインWeb/モバイルパーソナライゼーションのBlueprint

web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。

## ユースケース

* ランディングページの最適化
* 行動およびオフラインプロファイルターゲット設定
* オフラインインサイト（トランザクション、ロイヤリティおよび CRM データなど）およびモデル化されたインサイトに加えて、以前の製品／コンテンツ表示、製品／コンテンツの親和性、環境属性、サードパーティオーディエンスデータおよび人口統計に基づいたパーソナライズ機能

## アプリケーション

* [!UICONTROL リアルタイム顧客データプラットフォーム]
* Adobe Target
* Adobe Audience Manager（オプション）：サードパーティオーディエンスデータ、Co-op ベースのデバイスグラフ、Adobe Analytics で Platform セグメントを表示する機能および Platform で Adobe Analytics セグメントを表示する機能を追加
* Adobe Analytics（オプション）：Adobe Analytics データからの履歴行動データおよび詳細なセグメント化に基づいてセグメントを作成する機能を追加

## 構造

<img src="assets/onoff.svg" alt="オンライン/オフラインWebパーソナライゼーションのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

### セグメントの評価とアクティベーションのためのガードレール

| セグメントタイプ | 頻度 | スループット | 待ち時間（セグメント評価） | 待ち時間(セグメントアクティベーション) |
|---|---|---|---|---|
| エッジセグメント | エッジセグメントは現在ベータ版であり、有効なリアルタイムセグメントをExperience Platformエッジネットワークで評価し、Adobe TargetとAdobeJourney Optimizerを介した同じページ判定をリアルタイムで行うことができます。 |  | ～100 ms | Adobe Targetでのパーソナライゼーション、エッジプロファイルでのプロファイル検索、cookieベースの宛先を介したアクティベーションに対して、すぐに使用できます。 |
| ストリーミングセグメント化 | 新しいストリーミングイベントまたは記録がリアルタイム顧客プロファイルに取り込まれるたびに、そのセグメント定義が有効なストリーミングセグメントとなります。 <br>ストリーミングセグメントの条件に関するガイダンスについては、 [セグメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja) 化に関するドキュメントを参照してください。 | 1秒あたり最大1500イベント | ～ p95 &lt;5分 | これらのセグメントの実現が行われると、数分以内にAudience Managerとオーディエンス共有サービスに共有され、Adobe Targetの同じ/次のページのパーソナライゼーションに利用できます。 |
| 増分セグメント化 | 前回の増分またはバッチセグメントの評価後にリアルタイム顧客プロファイルに取り込まれた新しいデータに対して、1時間に1回。 |  |  | これらのセグメントのメンバーシップが認識されると、数分以内にAudience Managerとオーディエンス共有サービスに共有され、Adobe Targetの同じ/次のページのパーソナライゼーションに利用できます。 |
| バッチセグメント | 事前に定義されたシステムセットスケジュールに基づいて、またはAPIを介して手動で開始する1日に1回。 |  | ジョブあたり約1時間(最大10 TBのプロファイルストアサイズ)。10 TB ～ 100 TBのプロファイルストアサイズでは、ジョブあたり2時間。 バッチセグメントジョブのパフォーマンスは、プロファイル数、プロファイルのサイズ、評価対象のセグメント数に依存します。 | これらのセグメントのメンバーシップが認識されると、数分以内にAudience Managerとオーディエンス共有サービスに共有され、Adobe Targetの同じ/次のページのパーソナライゼーションに利用できます。 |

### アプリケーション間のオーディエンス共有のガードレール


| オーディエンス共有統合パターン | 詳細 | 頻度 | スループット | 待ち時間（セグメント評価） | 待ち時間(セグメントアクティベーション) |
|---|---|---|---|---|---|
| リアルタイム顧客データプラットフォームからAudience Manager |  | セグメントタイプによって異なります。上のセグメント化ガードレールの表を参照してください。 | セグメントタイプによって異なります。上のセグメント化ガードレールの表を参照してください。 | セグメントタイプによって異なります。上のセグメント化ガードレールの表を参照してください。 | セグメント評価が完了してから数分以内に<br>リアルタイムの顧客データプラットフォームとAudience Managerの初期オーディエンス設定の同期には、約4時間かかります。<br>4時間の間に実現したオーディエンスのメンバーシップは、その後のバッチセグメントジョブに関するAudience Managerに対して、「既存の」オーディエンスのメンバーシップとして書き込まれます。 |
| Adobe AnalyticsからAudience Managerへ | 各Adobe Analyticsレポートスイートで共有できるオーディエンスは、デフォルトで最大75個です。 Audience Managerライセンスを使用する場合、Adobe AnalyticsとAdobe Target、Adobe Audience Manager、Adobe Target間で共有できるオーディエンスの数に制限はありません。 |  |  |  |  |
| Adobe Analyticsからリアルタイム顧客データプラットフォーム | 現在はご利用いただけません。 |  |  |  |  |

## 実装パターン

Web/モバイルパーソナライゼーションのBlueprintは、以下に説明する方法で実装できます。

1. [!UICONTROL プラットフォームWeb SDK]または[!UICONTROL プラットフォームモバイルSDK]と[!UICONTROL エッジネットワーク]を使用する。
1. 従来のアプリケーション固有のSDK（AppMeasurement.jsなど）の使用

### 1.プラットフォームWeb/モバイルSDKとエッジアプローチ

<img src="assets/websdkflow.svg" alt="[!UICONTROLプラットフォームWeb SDK]または[!UICONTROLプラットフォームモバイルSDK]および[!UICONTROLエッジネットワーク]アプローチのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

### 2.アプリケーション固有のSDKアプローチ

<img src="assets/appsdkflow.png" alt="アプリケーション専用 SDK アプローチの参照アーキテクチャ" style="border:1px solid #4a4a4a" />

## 実装の前提条件

| アプリケーション／サービス | 必須ライブラリ | メモ |
|---|---|---|
| Adobe Target | [!UICONTROL プラットフォームWeb SDK]*、at.js 0.9.1以上、またはmbox.js 61+ | mbox.js は今後開発されないので、at.js をお勧めします。 |
| Adobe Audience Manager（オプション） | [!UICONTROL プラットフォームWeb SDK]*またはdil.js 5.0+ |  |
| Adobe Analytics（オプション） | [!UICONTROL プラットフォームWeb SDK]*またはAppMeasurement.js 1.6.4以降 | Adobe Analytics トラッキングは、地域データ収集（RDC）を使用する必要があります。 |
| Experience Cloud ID サービス | [!UICONTROL プラットフォームWeb SDK]*またはVisitorAPI.js 2.0以降 | （推奨）アプリケーション呼び出しの前に ID が設定されるように、Experience Platform Launch を使用して ID サービスをデプロイします |
| Experience Platform Mobile SDK（オプション） | 4.11 以上（iOS および Android™ 用） |  |
| Experience Platform Web SDK | 1.0、現在の Experience Platform SDK バージョンは、[Experience Cloud アプリケーションをまだサポートしていない様々なユースケースがあります](https://github.com/adobe/alloy/projects/5) |  |


## 実装手順

1. web またはモバイルアプリケーション用に [Adobe Target を実装](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ja)します
1. [Adobe Audience Manager を実装](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja)します（オプション）
1. [Adobe Analytics を実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)します（オプション）
1. [[!UICONTROL Experience Platform およびリアルタイム顧客プロファイルを実装]します](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=ja)
1. [Experience Cloud ID サービス](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=ja)または [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja) を実装します
   >[!NOTE]
   >
   >アプリケーション間のオーディエンス共有を許可するために、各アプリケーションは、Experience Cloud ID を使用し、同じ Experience Cloud 組織に属している必要があります。
1. [Experience Platform および Adobe Target 間のオーディエンス共有（共有オーディエンス）のプロビジョニングをリクエスト](https://www.adobe.com/go/audiences)します

## 関連ドキュメント

* [Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja)
* [Experience Platform セグメント化の概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja)
* [ストリーミングセグメント化](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Experience Platform セグメントビルダーの概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=ja)
* [Audience Manager ソースコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ja)
* [Adobe Audience Managerを通じたAdobe Analyticsセグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [Experience Platform Web SDK ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Cloud ID サービスドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)
* [Experience Platform Launch ドキュメント](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=ja)

## 関連するブログ投稿

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
