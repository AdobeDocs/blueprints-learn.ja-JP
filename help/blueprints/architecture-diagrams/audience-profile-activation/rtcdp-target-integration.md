---
title: Adobe Real-Time CDPとAdobe Targetの統合
description: Real-Time Customer Data Platformのオーディエンスとプロファイルコンテキストが、Edge Networkを通じてAdobe Targetとどのように連携するかを理解します。
landing-page-description: Real-Time Customer Data Platformのオーディエンスとプロファイルコンテキストが、Edge Networkを通じてAdobe Targetとどのように連携するかを理解します。
short-description: Real-Time Customer Data Platformのオーディエンスとプロファイルコンテキストが、Edge Networkを通じてAdobe Targetとどのように連携するかを理解します。
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
    internal-label: Real-Time Customer Data Platform
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
    internal-label: Segmentation
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: ba929a52-9339-4154-9487-317dc875a3c7
    internal-label: Use cases
  - id: c132d929-fa62-4271-803e-b823be07b914
    internal-label: Profile
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
    internal-label: Implementation
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
    internal-label: Segments
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
    internal-label: B2B
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
    internal-label: Audiences
  - id: ee602049-8a18-43df-9299-a689a025a371
    internal-label: Use cases
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 17%
---
# Adobe Real-Time CDPとAdobe Targetの統合

このアーキテクチャは、[!DNL Real-Time Customer Data Platform]と[!DNL Adobe Target]がEdge Networkを通じてどのように統合されるかを示します。 エッジでのリアルタイムのオーディエンス評価と、Adobe Targetとストリーミングオーディエンスやバッチオーディエンスの共有のどちらかを選択できます。

## アプリケーション

* [!DNL Real-Time Customer Data Platform]
* [!DNL Adobe Target]
* [!DNL Experience Platform] Edge Network
* Experience Platform Web SDKまたはEdge Network Server API

## 統合アプローチの選択

### エッジでのリアルタイムのオーディエンス評価

このアプローチは、[!DNL Adobe Target]が同ページまたは次ページのパーソナライゼーションにエッジ評価オーディエンスとプロファイル属性を必要とする場合に使用します。 Web SDKまたはEdge Network Server APIを実装し、[!DNL Adobe Target]および[!DNL Experience Platform] サービスを有効にしてデータストリームを設定します。

### Adobe Targetへのストリーミングとバッチオーディエンス共有

このアプローチは、[!DNL Real-Time Customer Data Platform]で評価されたオーディエンスが、リアルタイムのエッジ評価なしで[!DNL Adobe Target]で利用できる必要がある場合に使用します。 デフォルトの実稼動サンドボックスで[!DNL Adobe Target]の宛先を設定します。 Web SDKまたはEdge Network Server APIの実装は、リアルタイムのエッジ評価またはカスタム ID名前空間参照にのみ必要です。

## アーキテクチャ図

この図は、データ収集、Edge Network、[!DNL Real-Time Customer Data Platform]および[!DNL Adobe Target]の主な統合ポイントを示しています。

![Real-Time Customer Data PlatformとAdobe Targetの統合のためのアーキテクチャ &#x200B;](assets/real_time_cdp_target.png){zoomable="yes"}

## データフロー図

このシーケンスは、クライアントリクエストがEdge Networkに到達し、オーディエンスとプロファイルコンテキストを評価し、パーソナライゼーションリクエストを[!DNL Adobe Target]に送信し、結果として得られるエクスペリエンスをクライアントに返す方法を示します。

![Real-Time Customer Data PlatformとAdobe Targetの統合のためのデータフロー](assets/real_time_cdp_target_data_flow_detail.png){zoomable="yes"}

## 実装に関する考慮事項

* [!DNL Adobe Target]と[!DNL Real-Time Customer Data Platform]は同じIMS組織を使用する必要があります。
* [!DNL Adobe Target]宛先は、[!DNL Real-Time Customer Data Platform]のデフォルトの実稼動サンドボックスをサポートしています。
* エッジでカスタム ID名前空間を検索するには、Web SDKまたはEdge Network Server APIを使用し、ID マップに各IDを含めます。
* at.jsを使用する場合、プロファイル統合はECID ID名前空間のみをサポートします。

## 関連ドキュメント

### 統合の設定

* [Adobe Real-Time CDPのAdobe Target Connection](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja)
* [Edge データストリーム設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ja)

### エッジでの実装

* [Experience Platform Web SDKのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja)
* [Experience Platform Tags ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Cloud ID サービスのドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)

### オーディエンスを評価

* [Experience Platformのセグメント化の概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja)
* [リアルタイムセグメンテーション](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ja)
* [ストリーミングセグメンテーション](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [結合ポリシー設定](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=ja#create-a-merge-policy)
