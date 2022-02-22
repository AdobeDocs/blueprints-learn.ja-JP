---
title: オンラインとオフラインのデータを使用した Web／モバイルのパーソナライゼーション
description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
landing-page-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 91db73c9fb14d461ee62444199c3d053bd094639
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 70%

---

# オンラインとオフラインのデータを使用した Web／モバイルのパーソナライゼーション

Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。

## ユースケース

* ランディングページの最適化
* 行動およびオフラインプロファイルターゲット設定
* オフラインインサイト（トランザクション、ロイヤリティおよび CRM データなど）およびモデル化されたインサイトに加えて、以前の製品／コンテンツ表示、製品／コンテンツの親和性、環境属性、サードパーティオーディエンスデータおよび人口統計に基づいたパーソナライズ機能
* Adobe Target を使用して、Real-time Customer Data Platform で定義されたオーディエンスを Web サイトやモバイルアプリで共有、およびターゲット設定します。

## アプリケーション

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager（オプション）:サードパーティのオーディエンスデータ、Co-op ベースのデバイスグラフ、Adobe AnalyticsでReal-time Customer Data Platformのオーディエンスを表示する機能、Real-time Customer Data PlatformでAdobe Analyticsのオーディエンスを表示する機能を追加します。
* Adobe Analytics（オプション）：Adobe Analytics データからの履歴行動データおよび詳細なセグメント化に基づいてセグメントを作成する機能を追加

## 統合パターン

<table class="tg" style="undefined;table-layout: fixed; width: 790px">
<colgroup>
<col style="width: 20px">
<col style="width: 276px">
<col style="width: 229px">
<col style="width: 265px">
</colgroup>
<thead>
  <tr>
    <th class="tg-y6fn">#</th>
    <th class="tg-f7v4">統合パターン</th>
    <th class="tg-y6fn">機能</th>
    <th class="tg-f7v4">前提条件</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0lax">1</td>
<td class="tg-73oq">Target に共有される Edge に対するReal-time Customer Data Platformのリアルタイムセグメント評価</td>
    <td class="tg-0lax">- Edge 上で同じまたは次のページのパーソナライゼーションに対して、リアルタイムでオーディエンスを評価します。</td>
    <td class="tg-73oq"> — ターゲットの宛先は、Real-time Customer Data Platform Destinations で設定する必要があります。<br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。<br>- WebSDK を実装する必要があります。<br>- Mobile SDK および API ベースの実装は、現在使用できません</td> 
  </tr>
  <tr>
    <td class="tg-0lax">2</td>
    <td class="tg-73oq">Edge アプローチを使用した Target へのReal-time Customer Data Platformストリーミングおよびバッチオーディエンス共有</td>
    <td class="tg-0lax">- Edge ネットワークを通じて、Real-time Customer Data Platformから Target へのストリーミングおよびバッチオーディエンスを共有します。 リアルタイムで評価される Audience には、WebSDK と、統合パターン 1 で概要を説明したリアルタイムのオーディエンス評価が必要です。</td>
    <td class="tg-73oq"> — ターゲットの宛先は、Real-time Customer Data Platform Destinations で設定する必要があります。<br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。<br>WebSDK は不要です。<br>- AT.js を使用する場合、ECID に対するプロファイル参照のみがサポートされます。<br>- Edge 上でカスタム ID 名前空間を検索する場合は、WebSDK デプロイメントが必要です。また、各 ID を ID マップで ID として設定する必要があります。</td>
  </tr>
  <tr>
    <td class="tg-0lax">3</td>
    <td class="tg-73oq"><span style="font-weight:400;font-style:normal">オーディエンス共有サービスのアプローチを使用した、Target およびAudience Managerに対するReal-time Customer Data Platformのストリーミングおよびバッチオーディエンス共有</span></td>
    <td class="tg-0lax"><span style="font-weight:400;font-style:normal"> — オーディエンス共有サービスを使用して、Real-time Customer Data Platformから Target にストリーミングオーディエンスとバッチオーディエンスを共有し、Audience Managerを行います。 リアルタイムで評価される Audience には、WebSDK と、統合パターン 1 で概要を説明したリアルタイムのオーディエンス評価が必要です。</span></td>
    <td class="tg-73oq"> - オーディエンス共有サービスを介したオーディエンス投影は、プロビジョニングする必要があります。<br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。<br>- Target がアクションを実行するためには、ID を ECID 向けに解決して、Edge と共有する必要があります。<br> - この統合には WebSDK のデプロイメントは不要です。</td>
  </tr>
</tbody>
</table>


## アーキテクチャ

詳細アーキテクチャ

<img src="assets/RTCDP+Target.png" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a" />

シーケンス図

<img src="assets/RTCDP+Target_flow.png" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a" />

<br>

<img src="assets/RTCDP+Target_sequence.png" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a" />


概要アーキテクチャ

<img src="assets/personalization_with_apps.png" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a"/>

## ガードレール

[Web およびモバイルパーソナライズ機能ブループリントの概要ページのガードレールを参照してください。](overview.md)

## 実装パターン

Web／モバイルパーソナライズ機能ブループリントは、以下に説明する方法で実装できます。

1. [!UICONTROL Platform Web SDK] または [!UICONTROL Platform Mobile SDK] と[!UICONTROL エッジネットワーク]を使用。[Experience Platform Web および Mobile SDK のブループリントを参照してください。](../data-ingestion/websdk.md)
1. 従来のアプリケーション固有 SDK（AppMeasurement.js など）を使用
<img src="assets/app_sdk_flow.png" alt="アプリケーション固有 SDK アプローチの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a" />

## 実装に関する考慮事項

ID の前提条件

* Edge ネットワークおよび WebSDK で前述した統合パターン 1 を利用する場合は、任意のプライマリ ID を利用できます。 最初のログインパーソナライゼーションでは、パーソナライゼーションリクエストセットのプライマリ ID が、Real-time Customer Data Platformからのプロファイルのプライマリ ID と一致している必要があります。 匿名デバイスと既知の顧客との ID ステッチは、ハブで処理され、その後エッジに投影されます。 したがって、プライマリ ID がデバイス識別子として設定されている場合、既知の顧客データは、匿名プロファイルと既知のプロファイルが統合された後続のセッションまで適用されません。
* Adobe Experience PlatformからAdobe Targetにオーディエンスを共有するには、前述の統合パターン 3 で概要を説明したように、オーディエンス共有サービスを使用する際に、ECID を ID として使用する必要があります。
* 代替 ID を使用して、Audience Manager を介して Experience Platform のオーディエンスを Adobe Target と共有することもできます。Experience Platform は、次のサポートされている名前空間を使用して、Audience Manager に対するオーディエンスをアクティブ化します。IDFA、GAID、AdCloud、Google、ECID、EMAIL_LC_SHA256。Audience Manager と Target は、ECID ID を介してオーディエンスメンバーシップを解決するので、Adobe Target に対する最終的なオーディエンス共有を行うには、ECID が引き続き必要です。

## 実装手順

1. Web またはモバイルアプリケーション用に [Adobe Target を実装](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ja)します
1. [Adobe Audience Manager を実装](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja)します（オプション）
1. [Adobe Analytics を実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)します（オプション）
1. [Experience Platform および [!UICONTROL Real-time Customer Profile] を実装します](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=ja)
1. [Experience Cloud ID サービス](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=ja)または [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja) を実装します.Experience PlatformWeb SDK は、リアルタイムのエッジセグメント化には必要ですが、Real-time Customer Data Platformから Target へのストリーミングオーディエンスとバッチオーディエンスの共有には不要です。 現在、Mobile SDK と API を使用したリアルタイムセグメント化のサポートは利用できません。
1. [Real-time Customer Data Platform 内の宛先として](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja)、またはオーディエンス共有アプローチ用に Adobe Target を有効にする [Experience Platform と Adobe Target 間のオーディエンス共有（共有オーディエンス）のプロビジョニングをリクエスト](https://www.adobe.com/go/audiences)して、Experience Platform から Target へオーディエンスを共有します。

## 関連ドキュメント

### ドキュメント

* [Real-time Customer Data Platform 向け Adobe Target 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=en)
* [Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja)
* [Experience Platform Web SDK ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Cloud ID サービスドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)
* [Experience Platform セグメント化の概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja)
* [ストリーミングセグメント化](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [Experience Platform セグメントビルダーの概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=ja)
* [Audience Manager ソースコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ja)
* [Adobe Audience Manager を使用した Adobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)

### チュートリアル

* [Real-Time CDP と Adobe Target を使用した、次のヒットのパーソナライゼーション](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ja)

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
