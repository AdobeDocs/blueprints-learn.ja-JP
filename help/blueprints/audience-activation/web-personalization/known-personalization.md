---
title: Web/モバイルPersonalizationの概要 – Adobe Targetと RTCDP
description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
landing-page-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
short-description: Web パーソナライズ機能を電子メールおよびその他の既知および匿名のチャネルパーソナライズ機能と同期します。
solution: Real-Time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
source-git-commit: 0d65ac8bcc8647683b6361a293d8c941869cd6b5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 33%

---


# 既知の顧客データブループリントを使用した web/モバイルPersonalization

## ユースケース

* 既知の顧客データを使用したオンラインパーソナライズ機能
* ランディングページの最適化
* トランザクション、ロイヤリティ、CRM データ、およびモデル化されたインサイトなどのオフラインデータに加えて、以前の製品／コンテンツ表示、製品／コンテンツの親和性、環境属性、および人口統計に基づいたパーソナライズ機能
* Adobe TargetまたはAdobe Journey Optimizer Decisioning を使用して、Web サイトおよびモバイルアプリ上の Real-time Customer Data Platform で定義されたオーディエンスを共有およびターゲット化します。

## アプリケーション

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Journey Optimizerの決定
* Adobe Audience Manager（オプション）：サードパーティオーディエンスデータを追加
* Adobe Analytics または Customer Journey Analytics（オプション）：詳細なセグメント化を使用して、顧客の履歴データと行動データに基づいてセグメントを作成する機能を追加します。

### リファレンスドキュメント

* [Real-time Customer Data Platform 向け Adobe Target 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Adobe Journey Optimizer決定 ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/gs-decision)
* [Edge データストリームを設定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ja)
* [Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja)

## アプローチ

Web/モバイルでの既知の顧客パーソナライゼーションのアプローチの 1 つは、Real-time Customer Data Platform をAdobe Targetと統合することです。 以下のガイドでは、Real-time Customer Data Platform を統合して、既知の顧客パーソナライゼーションをAdobe Targetで強化する方法について詳しく説明します。

既知のお客様の web/モバイルパーソナライゼーションは、Experience Platform リアルタイム顧客プロファイルとセグメント化をネイティブに活用するAdobe Journey Optimizer Decisioning を使用して実装することもできます。 [Adobe Journey Optimizer ガイド ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home) を参照してください。このガイドでは、[ コードベースのエクスペリエンス ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based) または [web チャネルエクスペリエンス ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web) のいずれかを使用できます。

アーキテクチャブループリントは、および [Journey Optimizer ブループリント ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/journey-optimizer) と [Journey Optimizer Decisioning ブループリント ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview) でも使用できます。

## 統合パターン

| 統合パターン | 機能 | 前提条件 |
|--------------------|------------|---------------|
| **Real-time Customer Data Platform から Target に共有される、Edgeのリアルタイムセグメント評価** | - オーディエンスをリアルタイムで評価し、Edgeで同じページや次のページのパーソナライゼーションを行います。 <br> - ストリーミングまたはバッチ方式で評価されたセグメントもEdge Networkに投影され、エッジセグメントの評価とパーソナライゼーションに含められます。 | - Web/モバイル SDKを実装するか、Edge Network Server API を実装する必要があります。 <br> - Experience Edgeで Target とExperience Platform拡張機能を有効にして、データストリームを設定する必要があります。 <br>- Target の宛先は、Real-time Customer Data Platform の宛先で設定する必要があります。 <br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。 |
| **Edge アプローチを使用した、Real-time Customer Data Platform から Target へのストリーミングとバッチオーディエンス共有** | - Edge ネットワークを通じて、Real-time Customer Data Platform から Target へのストリーミングおよびバッチオーディエンスを共有します。<br> - リアルタイムで評価されるオーディエンスには、Web SDKおよびEdge Networkの実装が必要です。 | - ストリーミングおよびバッチ RTCDP オーディエンスを Target に共有する場合は、Target の web/Mobile SDKまたはEdge API の実装は必要ありませんが、リアルタイムエッジセグメント評価を有効にする場合は必要です。 <br>- AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。<br>- Edgeでのカスタム ID 名前空間検索の場合、Web SDK/Edge API デプロイメントが必要で、各 ID は ID マップで ID として設定される必要があります。 <br> - Target 宛先は、Real-time Customer Data Platform Destinations で設定する必要があります。RTCDP のデフォルトの実稼動サンドボックスのみがサポートされます。 <br>- Target との統合には、Experience Platform インスタンスと同じ IMS Org が必要です。 |
| **オーディエンス共有サービスアプローチを使用した、Real-time Customer Data Platform から Target およびAudience Managerへのストリーミングおよびバッチオーディエンス共有** |  – この統合パターンは、Audience Managerでサードパーティのデータやオーディエンスを強化したい場合に利用できます。 | - Target へのストリーミングオーディエンスとバッチオーディエンスの共有には web/モバイル SDKは必要ありませんが、リアルタイムエッジセグメント評価を有効にするには必要です。 <br>- AT.js を使用する場合、ECID ID 名前空間に対するプロファイル統合のみがサポートされます。<br>- Edgeでのカスタム ID 名前空間検索の場合、Web SDK/Edge API デプロイメントが必要で、各 ID は ID マップで ID として設定される必要があります。 <br> - オーディエンス共有サービスを介したオーディエンスプロジェクションをプロビジョニングする必要があります。 <br> - Target との統合には、Experience Platform インスタンスと同じ IMS 組織が必要です。 <br> - デフォルトの実稼動サンドボックスのオーディエンスのみが、オーディエンス共有コアサービスをサポートします。 |

## リアルタイム、ストリーミングおよびバッチオーディエンスの Adobe Target への共有

アーキテクチャ

<img src="assets/RTCDP+Target.svg" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

シーケンスの詳細

<img src="assets/RTCDP+Target_flow.svg" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

概要アーキテクチャ

<img src="assets/personalization_with_apps.svg" alt="オンライン／オフライン web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## 実装パターン

既知のお客様のパーソナライズ機能は、いくつかの実装方法でサポートされます。

### 実装パターン 1 - Web/モバイルSDKまたは [!DNL Edge Network] API を使用した [!DNL Edge Network] ール（推奨アプローチ）

* Web/モバイルSDKでの [!DNL Edge Network] の使用。 リアルタイムのエッジセグメント化には、Web／Mobile SDK または Edge API 実装アプローチが必要です。
* SDK ベースの実装については、[Experience Platform Web およびモバイル SDK ブループリントを参照 ](../../experience-platform/deployment/websdk.md) してください。
* Mobile SDKで使用するには、[Adobe Journey Optimizer - Decisioning 拡張機能 ](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) をインストールする必要があります。
* [Edge プロファイルを使用したAdobe Targetの API ベースの実装については、 [!DNL Edge Network] Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja) を参照してください。

### 実装パターン 2 - アプリケーション固有の SDK

従来のアプリケーション固有の SDK（AT.js や AppMeasurement.js など）を使用。リアルタイムエッジセグメント評価は、この実装方法ではサポートされていません。ただし、この実装アプローチでは、Experience Platform ハブからのストリーミングおよびバッチオーディエンス共有がサポートされます。

[Adobe Target Connector ドキュメントを参照してください ](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection)
[ アプリケーション固有のSDK ブループリントを参照 ](../../experience-platform/deployment/appsdk.md)

## 実装に関する考慮事項

* 前述の [!DNL Edge Network] および Web SDKで説明された実装パターン 1 を利用する場合は、任意のプライマリ ID を利用できます。
* 以前に RTCDP に取り込まれた既知の顧客データを使用して最初にログインするパーソナライゼーションでは、Real-time Customer Data Platform の既知の顧客 ID グラフに一致するプライマリ ID がパーソナライゼーションリクエストに含まれている必要があります。 プライマリ ID が ECID に設定されている場合や、既知の顧客プロファイルでまだステッチされていない ID に設定されている場合、ID ステッチがエッジで実現され、エッジのパーソナライゼーションに以前に取り込まれた既知の顧客データが含まれるまで数分かかります。
* Edge プロファイルには現在、14 日の TTL があります。 したがって、ユーザーがエッジにログインしていない場合や、エッジで 14 日間アクティブであった場合、エッジ上のプロファイルの有効期限が切れる可能性があります。そのため、エッジは、履歴プロファイルビューをハブから取得して、以前に取り込んだプロファイル属性とセグメントを含むパーソナライゼーションを強化する必要があります。これにより、後続のページビューと最初のログインで発生したプロファイルの履歴ビューをパーソナライゼーションになります。

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
