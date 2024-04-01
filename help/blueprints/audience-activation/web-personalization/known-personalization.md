---
title: Web/モバイルパーソナライゼーションの概要 — Adobe Target & RTCDP
description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
landing-page-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
short-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 89%

---


# 既知の顧客データブループリントを使用した Web/モバイルパーソナライゼーション

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

## 統合パターン

| 統合パターン | 機能 | 前提条件 |
|---|---|---|
| Real-time Customer Data Platform から Target に共有される Edge に関するリアルタイムのセグメント評価 | <ul><li>Edge 上で同じまたは次のページのパーソナライズ機能に対して、リアルタイムでオーディエンスを評価します。</li><li>さらに、ストリーミングまたはバッチ方式で評価されたセグメントも、 [!DNL Edge Network] エッジセグメントの評価とパーソナライゼーションに含める必要があります。</li></ul> | <ul><li>Web/モバイル SDK を実装するか、 [!DNL Edge Network] サーバー API</li><li>Datastream は、Target と Experience Platform 拡張を有効にして Experience Edge で設定する必要があります。</li><li>Target の宛先は、Real-time Customer Data Platform で設定する必要があります。</li><li>Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。</li></ul> |
| Edge アプローチを通じて、Real-time Customer Data Platform から Target へのストリーミングおよびバッチオーディエンスを共有 | <ul><li>を通じてReal-time Customer Data Platformから Target にストリーミングオーディエンスとバッチオーディエンスを共有します。 [!DNL Edge Network]. リアルタイムで評価されるオーディエンスには Web SDK が必要で、 [!DNL Edge Network] 実装。</li></ul> | <ul><li>ストリーミングおよびバッチ RTCDP オーディエンスを Target に共有するためには、Target の Web／Mobile SDK または Edge API 実装は必要ありませんが、上記で概説したリアルタイムのエッジセグメント評価を有効にする必要があります。</li><li>AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。</li><li>Edge 上でカスタム ID 名前空間を検索する場合は、Web SDK／API デプロイメントが必要です。また、各 ID を ID マップで ID として設定する必要があります。</li><li>Target の宛先は、Real-time Customer Data Platform の宛先で設定する必要があります。RTCDP のデフォルトの実稼働用サンドボックスのみがサポートされます。</li><li>Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。</li></ul> |
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

### 実装パターン 1 - [!DNL Edge Network] Web/Mobile SDK または [!DNL Edge Network] API（推奨されるアプローチ）

* の使用 [!DNL Edge Network] Web/Mobile SDK を使用します。 リアルタイムのエッジセグメント化には、Web／Mobile SDK または Edge API 実装アプローチが必要です。
* [Experience PlatformWeb およびモバイル SDK のブループリントを参照してください。](../../experience-platform/deployment/websdk.md) （SDK ベースの実装用）
* Mobile SDK で使用する場合、[Adobe Journey Optimizer - Decisioning 拡張機能](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer-decisioning)が Mobile SDK にインストールされている必要があります。
* [詳しくは、 [!DNL Edge Network] サーバー API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja) Edge プロファイルを使用したAdobe Targetの API ベース実装の場合。

### 実装パターン 2 - アプリケーション固有の SDK

従来のアプリケーション固有の SDK（AT.js や AppMeasurement.js など）を使用。リアルタイムエッジセグメント評価は、この実装方法ではサポートされていません。ただし、この実装アプローチでは、Experience Platform ハブからのストリーミングおよびバッチオーディエンス共有がサポートされます。

[アプリケーション固有の SDK ブループリントを参照](../../experience-platform/deployment/appsdk.md)

### 実装手順

1. Web またはモバイルアプリケーション用に [Adobe Target を実装](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ja)します
1. [Experience Platform および [!UICONTROL リアルタイム顧客プロファイルを実装]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=ja)すると、作成したオーディエンスは、該当する[結合ポリシー](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=ja#create-a-merge-policy)を Edge 上でアクティブに設定することにより、確実にアクティブ化できます。
1. 適切な拡張機能（Target または Adobe Journey Optimizer - Decisioning）がインストールされた [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja) または [Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/) を実装します。Experience Platform Web／Mobile SDK または EDGE API は、リアルタイムの Edge セグメント化には必要ですが、Real-time Customer Data Platform から Target へのストリーミングオーディエンスとバッチオーディエンスの共有には不要です。
1. [を設定します。 [!DNL Edge Network] Edge Datastream を使用](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ja)
1. [Real-time Customer Data Platform 内で Adobe Target を宛先として有効化](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja)
1. （オプション）[Adobe Audience Manager を実装](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja).
1. （オプション）[Experience Platform と Adobe Target（共有オーディエンス）間でのオーディエンス共有用のプロビジョニングをリクエスト](https://www.adobe.com/go/audiences)して、オーディエンスを Experience Platform から Target に共有します。

## ガードレール

[Web およびモバイルパーソナライズ機能ブループリントの概要ページのガードレールを参照してください。](overview.md)

* Edge プロファイルは、ユーザーが Edge 上でアクティブな場合にのみ作成されます。つまり、ユーザーのプロファイルには、Web/Mobile SDK または Edge Server API を介して Edge に送信されるストリーミングイベントがあります。これは通常、ユーザーが Web サイトまたはモバイルアプリでアクティブになっていることに対応します。
* エッジプロファイルには、14 日間のデフォルトの有効期間があります。ユーザーがアクティブな Edge イベントを収集していない場合、14 日間非アクティブ状態が続くと、プロファイルは Edge で期限切れになります。プロファイルはハブで有効なままであり、ユーザーが再びエッジでアクティブになると、エッジと同期されます。
* エッジで新しいプロファイルが作成されると、同期呼び出しがハブに対して非同期で行われ、宛先を介してエッジ投影用に設定されたオーディエンスと属性が取得されます。これは非同期プロセスであるため、ハブプロファイルがエッジに同期されるまでに 1 秒から数分かかる場合があります。したがって、最初のページエクスペリエンスで、新しいプロファイルがハブのプロファイルコンテキストを持つことを保証できません。これは、ハブに新しく収集されたデータにも適用されます。このデータはエッジに非同期で投影されるため、データが適切なエッジに到着するタイミングは、エッジアクティビティとは別になります。エッジでアクティブなプロファイルのみが、ハブから投影された属性とオーディエンスを保持します。

## 実装に関する考慮事項

ID の前提条件

* 上記で説明した実装パターン 1 を使用する場合、任意のプライマリ ID を利用できます ( [!DNL Edge Network] と Web SDK。 最初のログインパーソナライゼーションでは、パーソナライゼーションリクエストセットのプライマリ ID が、Real-time Customer Data Platform からのプロファイルのプライマリ ID と一致している必要があります。匿名デバイスと既知の顧客との間の ID ステッチは、ハブで処理され、その後エッジに投影されます。
* 消費者が Web サイトを訪問またはログインする前にハブにアップロードされたデータは、パーソナライゼーションにすぐに使用できないことに注意してください。ハブデータを同期するには、最初にアクティブな Edge プロファイルが存在する必要があります。Edge プロファイルが作成されると、ハブプロファイルと非同期で同期されるので、次ページのパーソナライゼーションが実行されます。
* Adobe Experience Platform から Adobe Target にオーディエンスを共有するには、上記の統合パターン 2 および 3 で概要を説明したように、オーディエンス共有サービスを使用する際に、ID として ECID を使用する必要があります。
* 代替 ID を使用して、Audience Manager を介して Experience Platform のオーディエンスを Adobe Target と共有することもできます。Experience Platform は、次のサポートされている名前空間を使用して、Audience Manager に対するオーディエンスをアクティブ化します。IDFA、GAID、AdCloud、Google、ECID、EMAIL_LC_SHA256。Audience Manager と Target は、ECID ID を介してオーディエンスのメンバーシップを解決するので、Adobe Target に消費者の最終的なオーディエンス共有を行うには、ECID が引き続き ID グラフ内にある必要があります。

## 関連ドキュメント

### SDK ドキュメント

* [Experience Platform Web SDK ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Cloud ID サービスドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)

### 接続のドキュメント

* [Real-time Customer Data Platform 向け Adobe Target 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja)
* [Edge データストリームを設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ja)
* [Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja)

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
