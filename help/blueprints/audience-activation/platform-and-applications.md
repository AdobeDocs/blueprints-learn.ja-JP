---
title: Experience Cloud アプリケーションを使用したオーディエンスとプロファイルのアクティベーションブループリント
description: Experience Platform でプロファイルおよびオーディエンスを管理し、Experience Cloud アプリケーションを使用して共有します。
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services
kt: 7722
exl-id: f36014e8-170d-47e1-b4ec-10c0ea70612d
source-git-commit: 094591020413933932356cb8c393bf569bcfca50
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 95%

---

# Experience Cloud アプリケーションを使用したオーディエンスとプロファイルのアクティベーションブループリント

Experience Platform でプロファイルおよびオーディエンスを管理し、Experience Cloud アプリケーションを使用して共有します。Experience Platform でリッチな顧客セグメントおよびインサイトを構築および共有し、Experience Cloud アプリケーションを使用して共有します。

Experience Cloud アプリケーションを使用したアクティベーションは、[既知の顧客アクティベーションブループリント](known.md)と密接に連携しています。

## ユースケース

* Experience Cloud による顧客インタラクションチャネルをまたいでパーソナライズおよびターゲット設定します。
* Experience Platform と Experience Cloud アプリケーションの間でオーディエンスおよびプロファイルデータを共有します。

## アプリケーション

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]
* Experience Platform Activation
* Experience Cloud アプリケーション
   * Adobe Audience Manager
   * Adobe Target
   * Adobe Campaign
   * Journey Optimizer

## アーキテクチャ

Experience Platform と Experience Cloud アプリケーションの統合に関する追加のアーキテクチャ図については、[Experience Platform およびアプリケーションアーキテクチャの節](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=ja)を参照してください。

### Experience Cloud アプリケーションを使用したオーディエンスとプロファイルのアクティベーション

<img src="../experience-platform/assets/aep+apps_horizontal.svg" alt="Experience Cloud アプリケーションを使用したオーディエンスとプロファイルのアクティベーションの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />
<br>

## ガードレール

[オーディエンスとプロファイルのアクティベーションの概要ページのガードレール](overview.md)を参照してください

## 実装に関する考慮事項

* プロファイルデータを宛先に共有するには、宛先ペイロードの宛先で使用される特定の ID 値を含める必要があります。ターゲットの宛先に必要な ID は、Platform に取り込まれ、[!UICONTROL リアルタイム顧客プロファイル]の ID として設定される必要があります。

### Real-time Customer Data Platform から Audience Manager へのオーディエンスの共有

* 詳しくは、次のドキュメントを参照してください。[Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja).

* RT-CDP のオーディエンスメンバーシップは、セグメント評価が完了し、セグメント評価がバッチで行われたかストリーミングで行われたかに関わらず、リアルタイム顧客プロファイルに書き込まれるとすぐに、ストリーミング方式で Audience Manager に共有されます。選定されたプロファイルに、関連するプロファイルデバイスの地域ルーティング情報が含まれる場合、RTCDP からのオーディエンスメンバーシップは、関連する Audience Manager エッジ上でストリーミング方式で選定されます。地域ルーティング情報が過去 14 日間のタイムスタンプを持つプロファイルに適用された場合、ストリーミングの Audience Manager Edge エッジで評価されます。RTCDP からのプロファイルに地域ルーティング情報が含まれていない場合、または地域ルーティング情報が 14 日以上前のものである場合、プロファイルのメンバーシップは、バッチベースの評価とアクティブ化のために Audience Manager ハブロケーションに送信されます。エッジのアクティベーションの対象となるプロファイルは、RTCDP のセグメントの選定から数分以内にアクティブ化され、エッジのアクティベーションの対象とならないプロファイルは Audience Manager ハブで選定され、12～24 時間の処理期間を持つ場合があります。

* Audience Manager プロファイルが保存されている Edge の地域ルーティング情報は、Audience Manager、Visitor ID サービス、Analytics、Launch、または Web SDK から直接、XDM フィールドグループ「データキャプチャ地域情報」を使用して、個別のプロファイルレコードクラスのデータセットとして Experience Platform に収集することが可能です。

* Experience Platform から Audience Manager にオーディエンスが共有されるアクティベーションシナリオでは、次の ID が自動的に共有されます。ECID、IDFA、GAID、ハッシュ化されたメールアドレス（EMAIL_LC_SHA256）、AdCloud ID。現在、カスタムの名前空間は共有されません。

* 必須の宛先 ID が[!UICONTROL リアルタイム顧客プロファイル]に含まれている場合、または[!UICONTROL リアルタイム顧客プロファイル]内の ID が Audience Manager でリンクされる必須の宛先 ID と関連付けられる場合、Experience Platform からのオーディエンスは、Audience Manager 宛先を使用して共有できます。

### Real-time Customer Data Platform から Target へのオーディエンスの共有

* 詳しくは、 [既知の顧客のパーソナライゼーション — Target および RTCDP ブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/known-personalization.html) を参照してください。

### Real-time Customer Data Platform から Campaign および Journey Optimizer へのオーディエンスの共有

* Real-time Customer Data Platform から Campaign および Journey Optimizer へのプロファイルとオーディエンスの共有に関する詳細は、[カスタマージャーニーのブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=ja)を参照してください。

## 関連ドキュメント

* [[!UICONTROL Real-time Customer Data Platform] 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [[!UICONTROL Real-time Customer Data Platform] の概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL Real-time Customer Data Platform] のデモ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)
