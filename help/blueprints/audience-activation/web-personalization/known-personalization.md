---
title: Web/モバイルPersonalizationの概要 – Adobe Targetと RTCDP
description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
landing-page-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
short-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 845655a275cdb6d4a9cd397ec7c3515cbf02d321
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 79%

---


# 既知の顧客データブループリントを使用した web/モバイルPersonalization

## ユースケース

* 既知の顧客データを使用したオンラインパーソナライズ機能
* ランディングページの最適化
* トランザクション、ロイヤリティ、CRM データ、およびモデル化されたインサイトなどのオフラインデータに加えて、以前の製品／コンテンツ表示、製品／コンテンツの親和性、環境属性、および人口統計に基づいたパーソナライズ機能
* Adobe Target を使用して、Real-time Customer Data Platform で定義されたオーディエンスを web サイトやモバイルアプリで共有、およびターゲット設定します。

## アプリケーション

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager（オプション）：サードパーティオーディエンスデータを追加
* Adobe Analytics または Customer Journey Analytics（オプション）：詳細なセグメント化を使用して、顧客の履歴データと行動データに基づいてセグメントを作成する機能を追加します。

### リファレンスドキュメント

* [Real-time Customer Data Platform 向け Adobe Target 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Edge データストリームを設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ja)
* [Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja)


## 統合パターン

| 統合パターン | 機能 | 前提条件 |
|---|---|---|
| Real-time Customer Data Platform から Target に共有される Edge に関するリアルタイムのセグメント評価 | <ul><li>Edge 上で同じまたは次のページのパーソナライズ機能に対して、リアルタイムでオーディエンスを評価します。</li><li>また、ストリーミングまたはバッチ方式で評価されるセグメントもすべて [!DNL Edge Network] エッジセグメントの評価とパーソナライゼーションに含める必要があります。</li></ul> | <ul><li>Web/Mobile SDK を実装する必要があります。または [!DNL Edge Network] サーバー API</li><li>Datastream は、Target と Experience Platform 拡張を有効にして Experience Edge で設定する必要があります。</li><li>Target の宛先は、Real-time Customer Data Platform で設定する必要があります。</li><li>Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。</li></ul> |
| Edge アプローチを通じて、Real-time Customer Data Platform から Target へのストリーミングおよびバッチオーディエンスを共有 | <ul><li>を使用して、Real-time Customer Data Platformから Target にストリーミングオーディエンスとバッチオーディエンスを共有する [!DNL Edge Network]. リアルタイムで評価されるオーディエンスには、Web SDK および [!DNL Edge Network] 実装。</li></ul> | <ul><li>ストリーミングおよびバッチ RTCDP オーディエンスを Target に共有するためには、Target の Web／Mobile SDK または Edge API 実装は必要ありませんが、上記で概説したリアルタイムのエッジセグメント評価を有効にする必要があります。</li><li>AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。</li><li>Edge 上でカスタム ID 名前空間を検索する場合は、Web SDK／API デプロイメントが必要です。また、各 ID を ID マップで ID として設定する必要があります。</li><li>Target の宛先は、Real-time Customer Data Platform の宛先で設定する必要があります。RTCDP のデフォルトの実稼働用サンドボックスのみがサポートされます。</li><li>Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。</li></ul> |
| オーディエンス共有サービスを介して、Real-time Customer Data Platform から Target および Audience Manager にストリーミングおよびバッチオーディエンスを共有 | <ul><li>この統合パターンは、サードパーティのデータやオーディエンスからの追加のエンリッチメントを Audience Manager で必要とする場合に利用できます。</li></ul> | <ul><li>Web／Mobile SDK は、Target へのストリーミングおよびバッチオーディエンスの共有には必要ありませんが、リアルタイムでのエッジセグメント評価を可能にするために必要です。</li><li>AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。</li><li>Edge 上でカスタム ID 名前空間を検索する場合は、Web SDK／API デプロイメントが必要です。また、各 ID を ID マップで ID として設定する必要があります。</li><li>オーディエンス共有サービスを介したオーディエンス投影は、プロビジョニングする必要があります。</li><li>Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。</li><li>デフォルトの実稼働用サンドボックスのオーディエンスのみが、オーディエンス共有コアサービスをサポートします。</li></ul> |

## リアルタイム、ストリーミングおよびバッチオーディエンスの Adobe Target への共有

アーキテクチャ

<img src="assets/RTCDP+Target.svg" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

シーケンスの詳細

<img src="assets/RTCDP+Target_flow.svg" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

概要アーキテクチャ

<img src="assets/personalization_with_apps.svg" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## 実装パターン

既知のお客様のパーソナライズ機能は、いくつかの実装方法でサポートされます。

### 実装パターン 1 - [!DNL Edge Network] Web/Mobile SDK または [!DNL Edge Network] API （推奨アプローチ）

* 使用， [!DNL Edge Network] Web/Mobile SDK を使用します。 リアルタイムのエッジセグメント化には、Web／Mobile SDK または Edge API 実装アプローチが必要です。
* [Experience Platformの Web および Mobile SDK ブループリントを参照してください。](../../experience-platform/deployment/websdk.md) SDK ベースの実装の場合。
* Mobile SDK で使用する場合、[Adobe Journey Optimizer - Decisioning 拡張機能](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer-decisioning)が Mobile SDK にインストールされている必要があります。
* [を参照してください。 [!DNL Edge Network] サーバー API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja) （Edge プロファイルを使用したAdobe Targetの API ベース実装の場合）。

### 実装パターン 2 - アプリケーション固有の SDK

従来のアプリケーション固有の SDK（AT.js や AppMeasurement.js など）を使用。リアルタイムエッジセグメント評価は、この実装方法ではサポートされていません。ただし、この実装アプローチでは、Experience Platform ハブからのストリーミングおよびバッチオーディエンス共有がサポートされます。

[Adobe Target Connector ドキュメントを参照してください。](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[アプリケーション固有の SDK ブループリントを参照してください](../../experience-platform/deployment/appsdk.md)

## 実装に関する考慮事項

ID の前提条件

* 前述ので概要を説明した実装パターン 1 を使用すると、任意のプライマリ ID を利用できます [!DNL Edge Network] と Web SDK。 最初のログインのパーソナライゼーションでは、パーソナライゼーションリクエストセットのプライマリ ID がReal-time Customer Data Platformからのプロファイルのプライマリ ID と一致する必要があります。

## 関連ドキュメント

### SDK ドキュメント

* [Experience Platform Web SDK ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Cloud ID サービスドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)

### セグメント化ドキュメント

* [Experience Platform セグメント化の概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja)
* [リアルタイムセグメント化](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ja)
* [ストリーミングセグメント化](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [Adobe Audience Manager を使用した Adobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [結合ポリシー設定](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=ja#create-a-merge-policy)

### チュートリアル

* [Real-Time CDP と Adobe Target を使用した、次のヒットのパーソナライズ機能](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ja)

### 関連するブログ投稿

* [アドビが、Adobe Target と Real-time Customer Data Platform を使用した同一ページ強化パーソナライズ機能を発表](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform's Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our "Customer Zero" Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
