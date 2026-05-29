---
title: Adobe Targetを使用した既知のCustomer Personalization
description: RTCDP のプロファイルとオーディエンスを Adobe Target と統合します。
landing-page-description: RTCDP のプロファイルとオーディエンスを Adobe Target と統合します。
short-description: RTCDP のプロファイルとオーディエンスを Adobe Target と統合します。
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3aid: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: adee20bd-51f4-461d-b9db-d215f8756eebid: ba929a52-9339-4154-9487-317dc875a3c7id: c132d929-fa62-4271-803e-b823be07b914id: c93393a4-e558-47e1-992e-c91ed4d480ceid: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16id: d1823595-9241-4128-8a33-e4ac3bf08773id: ee602049-8a18-43df-9299-a689a025a371id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 213e2d7d73d91fa7b487289dfe62685bc32d5029
workflow-type: tm+mt
source-wordcount: 735
ht-degree: 37%

---

# Adobe Targetを使用した既知のCustomer Personalization

>[!TIP]
>このブループリントは、Personalizationの[ ユースケースパターン ](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md)としても利用できます。

## ユースケース

* 既知の顧客データを使用したオンラインパーソナライズ機能
* ランディングページの最適化
* トランザクション、ロイヤリティ、CRM データ、およびモデル化されたインサイトなどのオフラインデータに加えて、以前の製品／コンテンツ表示、製品／コンテンツの親和性、環境属性、および人口統計に基づいたパーソナライズ機能
* Adobe Targetを使用して、web サイトやモバイルアプリ上で、Adobe Real-Time CDPで定義されたオーディエンスを共有およびターゲティングできます

## アプリケーション

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target

### リファレンスドキュメント

* [Adobe Real-Time CDPのAdobe Target Connection](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Edge データストリーム設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ja)

## 統合パターン

| 統合パターン | 機能 | 前提条件 |
|--------------------|------------|---------------|
| **Real-time Customer Data PlatformからTargetに共有されたEdgeのリアルタイム セグメント評価** | - Edge上で同じページまたは次のページのパーソナライゼーションをリアルタイムで評価します。 <br>- ストリーミングまたはバッチ方式で評価されたすべてのセグメントも、Edge Networkに投影され、エッジセグメントの評価とパーソナライゼーションに含まれます。 | - Web/Mobile SDKを実装するか、Edge Network Server APIを実装する必要があります。 <br>- TargetおよびExperience Platform拡張機能を有効にして、Experience Edgeでデータストリームを設定する必要があります。 <br>- ターゲットの宛先は、Real-time Customer Data Platformの宛先で設定する必要があります。 <br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。 |
| **Adobe Edgeを利用して、Adobe Real-Time CDPからAdobe Targetにオーディエンスをストリーミングおよびバッチで共有** | - Edge ネットワークを通じて、Real-time Customer Data Platform から Target へのストリーミングおよびバッチオーディエンスを共有します。 <br>- リアルタイムで評価されるオーディエンスには、Web SDKとEdge Networkの実装が必要です。 | - Adobe TargetのWeb/Mobile SDKまたはEdge APIの実装は、ストリーミングおよびバッチ RTCDP オーディエンスをAdobe Targetと共有するために必要ではありませんが、リアルタイムのエッジセグメント評価を有効にするために必要です。 <br>- AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。 <br>- Edgeでカスタム ID名前空間を検索するには、Web SDK/Edge APIのデプロイメントが必要です。各IDはID マップでIDとして設定する必要があります。 <br>- ターゲットの宛先はReal-time Customer Data Platform Destinationsで設定する必要がありますが、RTCDPのデフォルトの実稼動サンドボックスのみがサポートされています。 <br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。 |
| **Audience Sharing Service アプローチを使用して、Real-time Customer Data PlatformからTargetおよびAudience Managerへのストリーミングとバッチ オーディエンスの共有** |  – この統合パターンは、Audience Managerのサードパーティデータとオーディエンスからの追加のエンリッチメントが必要な場合に活用できます。 | - Web/Mobile SDKは、ストリーミングおよびバッチオーディエンスをTargetに共有するために必要ではありませんが、リアルタイムのエッジセグメント評価を有効にするために必要です。 <br>- AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。 <br>- Edgeでカスタム ID名前空間を検索するには、Web SDK/Edge APIのデプロイメントが必要です。各IDはID マップでIDとして設定する必要があります。 <br>- オーディエンス共有サービスを介したオーディエンス予測をプロビジョニングする必要があります。 <br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。 <br>- デフォルトの実稼動サンドボックスのオーディエンスのみが、オーディエンス共有コアサービスをサポートします。 |

## リアルタイム、ストリーミングおよびバッチオーディエンスの Adobe Target への共有

アーキテクチャ

![ オンライン/オフライン Web Personalization ブループリントの参照アーキテクチャ ](assets/RTCDP+Target.png)

シーケンスの詳細

![ オンライン/オフライン Web Personalization ブループリントの参照アーキテクチャ ](assets/RTCDP+Target_flow.png)

概要アーキテクチャ

![ オンライン/オフライン Web Personalization ブループリントの参照アーキテクチャ ](assets/personalization_with_apps.png)

## 関連ドキュメント

### SDK ドキュメント

* [Experience Platform Web SDKのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja)
* [Experience Platform Tags ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Cloud ID サービスのドキュメント](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)

### セグメント化ドキュメント

* [Experience Platformのセグメント化の概要](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja)
* [リアルタイムセグメンテーション](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ja)
* [ストリーミングセグメンテーション](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [Adobe Audience ManagerによるAdobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [結合ポリシー設定](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=ja#create-a-merge-policy)

### チュートリアル

* [Real-Time CDPとAdobe Targetによる次のヒットのパーソナライゼーション](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ja)
