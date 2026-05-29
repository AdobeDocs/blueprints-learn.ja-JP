---
title: Adobe Targetを使用した既知のCustomer Personalization
description: RTCDP のプロファイルとオーディエンスを Adobe Target と統合します。
landing-page-description: RTCDP のプロファイルとオーディエンスを Adobe Target と統合します。
short-description: RTCDP のプロファイルとオーディエンスを Adobe Target と統合します。
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
source-git-commit: 213e2d7d73d91fa7b487289dfe62685bc32d5029
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 33%

---


# Adobe Targetを使用した既知のCustomer Personalization

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

![ オンライン/オフライン Web Personalization ブループリントの参照アーキテクチャ ](/help/blueprints/audience-activation/assets/RTCDP+Target.png)

シーケンスの詳細

![ オンライン/オフライン Web Personalization ブループリントの参照アーキテクチャ ](/help/blueprints/audience-activation/assets/RTCDP+Target_flow.png)

概要アーキテクチャ

![ オンライン/オフライン Web Personalization ブループリントの参照アーキテクチャ ](/help/blueprints/audience-activation/assets/personalization_with_apps.png)

## 実装パターン

既知のお客様のパーソナライズ機能は、いくつかの実装方法でサポートされます。

### Web/Mobile SDKまたは[!DNL Edge Network] APIを使用した実装パターン 1 - [!DNL Edge Network] （推奨されるアプローチ）

* Web/Mobile SDKで[!DNL Edge Network]を使用しています。 リアルタイムのエッジセグメント化には、Web／Mobile SDK または Edge API 実装アプローチが必要です。
* [SDK ベースの実装については、Experience Platform Webおよびモバイル SDK ブループリント ](/help/blueprints/experience-platform/deployment/websdk.md)を参照してください。
* モバイル SDKで使用するには、[Adobe Journey Optimizer - Decisioning拡張機能](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/)をインストールする必要があります。
* [Edge プロファイルを使用したAdobe TargetのAPI ベースの実装については、 [!DNL Edge Network] Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)を参照してください。

### 実装パターン 2 - アプリケーション固有の SDK

従来のアプリケーション固有の SDK（AT.js や AppMeasurement.js など）を使用。 リアルタイムエッジセグメント評価は、この実装方法ではサポートされていません。 ただし、この実装アプローチでは、Experience Platform ハブからのストリーミングおよびバッチオーディエンス共有がサポートされます。

[Adobe Target Connector ドキュメントを参照してください](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[ アプリケーション固有のSDK ブループリントを参照](/help/blueprints/experience-platform/deployment/appsdk.md)

## 実装に関する考慮事項

* 上記の[!DNL Edge Network]およびWeb SDKで説明した実装パターン 1を使用する場合、任意のプライマリ IDを活用できます。
* RTCDPに以前に取り込まれた既知の顧客データを使用したファーストログインパーソナライゼーションでは、パーソナライゼーションリクエストに、Real-Time Customer Data Platformの既知の顧客ID グラフと一致するプライマリ IDが必要です。 プライマリ IDがECIDに設定されている場合、またはIDがまだ既知の顧客プロファイルにステッチされていない場合、ID ステッチがエッジで実現され、エッジのパーソナライゼーションに以前に取り込まれた既知の顧客データが含まれるまで数分かかります。
* 現在、Edge プロファイルには14日間のTTLがあります。 したがって、ユーザーがエッジでログインしていないか14日間アクティブになっていない場合、エッジ上のプロファイルは期限切れになる可能性があるため、エッジはハブからプロファイルを取得して、以前に取り込まれたプロファイル属性とセグメントを含むパーソナライゼーションを強化するために履歴プロファイルビューを取得する必要があります。これにより、後続のページビューと最初のログインで発生するプロファイルの履歴ビューがパーソナライズされます。

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
