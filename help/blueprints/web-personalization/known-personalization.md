---
title: Web/Mobile Personalizationの概要
description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
landing-page-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 4d0313e079a6f0f48f9c958f598f0fd02b90fd5f
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 62%

---


# Web/Mobile Personalizationと既知の顧客データ

## ユースケース

* 既知の顧客データを使用したオンラインパーソナライゼーション
* ランディングページの最適化
* トランザクション、ロイヤリティ、CRM データ、およびモデル化されたインサイトなどのオフラインデータに加えて、以前の製品／コンテンツ表示、製品／コンテンツの親和性、環境属性、および人口統計に基づいたパーソナライズ機能
* Adobe Target を使用して、Real-time Customer Data Platform で定義されたオーディエンスを Web サイトやモバイルアプリで共有、およびターゲット設定します。

## アプリケーション

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager（オプション）:サードパーティのオーディエンスデータ、Co-op ベースのデバイスグラフを追加します。
* Adobe Analytics（オプション）：Adobe Analytics データからの履歴行動データおよび詳細なセグメント化に基づいてセグメントを作成する機能を追加

## 統合パターン

| 統合パターン | 機能 | 前提条件 |
|---|---|---|
| Real-time Customer Data Platform から Target に共有される Edge に関するリアルタイムのセグメント評価 | <ul><li>Edge 上で同じまたは次のページのパーソナライゼーションに対して、リアルタイムでオーディエンスを評価します。</li><li>さらに、ストリーミングまたはバッチ方式で評価されたセグメントも Edge Network に投影され、エッジセグメントの評価とパーソナライゼーションに含められます。</li></ul> | <ul><li>Web/Mobile SDK を実装する必要があります。</li><li>Datastream は、Target と DataStream 拡張を有効にして Experience Edge で設定する必要があります。</li><li>Target の宛先は、Real-time Customer Data Platform Destinations で設定する必要があります。</li><li>Target との統合には、統合インスタンスと同じ IMS Org が必要です。Experience Platformインスタンス。</li></ul> |
| - Edge アプローチを通じて、Real-time Customer Data Platform から Target へのストリーミングおよびバッチオーディエンスを共有 | <ul><li>Edge ネットワークを通じて、Real-time Customer Data Platformから Target へのストリーミングオーディエンスとバッチオーディエンスを共有します。 リアルタイムで評価されるオーディエンスには、WebSDK および Edge ネットワークの実装が必要です。</li></ul> | <ul><li>Web/Mobile SDK は、ストリーミングオーディエンスとバッチオーディエンスを Target に共有する場合には必要ありませんが、リアルタイムのエッジセグメント評価を有効にする必要があります。</li><li>AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。</li><li>Edge 上でカスタム ID 名前空間を検索する場合は、WebSDK デプロイメントが必要です。また、各 ID を ID マップ内の ID として設定する必要があります。</li><li>Target の宛先は、Real-time Customer Data Platform Destinations で設定する必要があります。</li><li>Target との統合には、統合インスタンスと同じ IMS Org が必要です。Experience Platformインスタンス。</li></ul> |
| オーディエンス共有サービスを介して、Real-time Customer Data Platform から Target および Audience Manager にストリーミングおよびバッチオーディエンスを共有 | <ul><li>この統合パターンは、サードパーティのデータやオーディエンスからの追加のエンリッチメントをAudience Managerで必要とする場合に利用できます。</li></ul> | <ul><li>Web/Mobile SDK は、ストリーミングオーディエンスとバッチオーディエンスを Target に共有する場合には必要ありませんが、リアルタイムのエッジセグメント評価を有効にする必要があります。</li><li>AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。</li><li>Edge 上でカスタム ID 名前空間を検索する場合は、WebSDK デプロイメントが必要です。また、各 ID を ID マップ内の ID として設定する必要があります。</li><li>オーディエンス共有サービスを介したオーディエンス投影は、プロビジョニングする必要があります。</li><li>Target の宛先は、Real-time Customer Data Platform Destinations で設定する必要があります。</li><li>Target との統合には、統合インスタンスと同じ IMS Org が必要です。Experience Platformインスタンス。</li></ul> |

## Adobe Targetへのリアルタイム、ストリーミングおよびバッチオーディエンス共有

アーキテクチャ

<img src="assets/RTCDP+Target.png" alt="オンライン／オフライン Web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

シーケンスの詳細

<img src="assets/RTCDP+Target_flow.png" alt="オンライン／オフライン Web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

概要アーキテクチャ

<img src="assets/personalization_with_apps.png" alt="オンライン／オフライン Web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a"/>

## 実装パターン

既知のお客様のPersonalizationは、いくつかの実装方法でサポートされます。

### 実装パターン 1 - Web/Mobile SDK を使用した Edge ネットワーク（推奨されるアプローチ）

Web/Mobile SDK での Edge Network の使用. リアルタイムのエッジセグメント化には、Web/モバイル SDK または Edge API 実装アプローチが必要です。

[Experience Platform Web および Mobile SDK のブループリントを参照してください。](../data-ingestion/websdk.md)

### 実装パターン 2 — アプリケーション固有の SDK

従来のアプリケーション固有の SDK（AT.js や AppMeasurement.js など）を使用する。 リアルタイムエッジセグメント評価は、この実装方法ではサポートされていません。 ただし、この実装アプローチでは、Experience Platformハブからのストリーミングおよびバッチオーディエンス共有がサポートされます。

[アプリケーション固有の SDK ブループリントを参照してください。](../data-ingestion/appsdk.md)

### 実装手順

1. Web またはモバイルアプリケーション用に [Adobe Target を実装](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ja)します
1. [Experience Platform および[!UICONTROL Real-time Customer Profile の実装]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=ja)すると、作成したオーディエンスは、該当する[結合ポリシー](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=ja#create-a-merge-policy)を Edge 上でアクティブに設定することにより、確実にアクティブ化することができます。
1. [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja)を実装します。Experience Platform Web SDK は、リアルタイムの Edge セグメント化には必要ですが、Real-time Customer Data Platform から Target へのストリーミングオーディエンスとバッチオーディエンスの共有には不要です。現在、Mobile SDK と API を使用したリアルタイムセグメント化のサポートは利用できません。
1. [Edge データストリームを使用して Edge ネットワークを設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ja)
1. [Real-time Customer Data Platform 内で Adobe Target を宛先として有効化](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja)
1. （オプション） [Adobe Audience Managerの実装](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja).
1. （オプション） [Experience PlatformとAdobe Target（共有オーディエンス）間でのオーディエンス共有用のプロビジョニングをリクエストします](https://www.adobe.com/go/audiences) を使用して、オーディエンスをExperience Platformから Target に共有できます。

## ガードレール

[Web およびモバイルパーソナライズ機能ブループリントの概要ページのガードレールを参照してください。](overview.md)

## 実装に関する考慮事項

ID の前提条件

* Edge ネットワークおよび WebSDK で概説した統合パターン 1 を利用する場合は、任意のプライマリ ID を利用できます。最初のログインパーソナライゼーションでは、パーソナライゼーションリクエストセットのプライマリ ID が、Real-time Customer Data Platform からのプロファイルのプライマリ ID と一致している必要があります。匿名デバイスと既知の顧客との間の ID ステッチは、ハブで処理され、その後エッジに投影されます。
* Adobe Experience Platform から Adobe Target にオーディエンスを共有するには、上記の使用例のシナリオ 3 で概要を説明したように、オーディエンス共有サービスを使用する際に、ID として ECID を使用する必要があります。
* 代替 ID を使用して、Audience Manager を介して Experience Platform のオーディエンスを Adobe Target と共有することもできます。Experience Platform は、次のサポートされている名前空間を使用して、Audience Manager に対するオーディエンスをアクティブ化します。IDFA、GAID、AdCloud、Google、ECID、EMAIL_LC_SHA256。Audience Manager と Target は、ECID ID を介してオーディエンスメンバーシップを解決するので、Adobe Target に対する最終的なオーディエンス共有を行うには、ECID が引き続き必要です。

## 関連ドキュメント

### SDK ドキュメント

* [Experience Platform Web SDK ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Cloud ID サービスドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)

### 接続のドキュメント

* [Real-time Customer Data Platform 向け Adobe Target 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Edge データストリームを設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)
* [Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja)

### セグメント化ドキュメント

* [Experience Platform セグメント化の概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja)
* [リアルタイムセグメント化](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ja)
* [ストリーミングセグメント化](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [Adobe Audience Manager を使用した Adobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [結合ポリシー設定](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=en#create-a-merge-policy)

### チュートリアル

* [Real-Time CDP と Adobe Target を使用した、次のヒットのパーソナライズ機能](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ja)

### 関連するブログ投稿

* [アドビが、Adobe Target と Real-time Customer Data Platform を使用した同一ページ強化パーソナライズ機能を発表](https://blog.adobe.com/en/publish/2021/10/05/adobe-announces-same-page-enhanced-personalization-with-adobe-target-real-time-customer-data-platform)
* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
