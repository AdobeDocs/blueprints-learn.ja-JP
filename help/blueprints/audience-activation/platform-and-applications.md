---
title: Experience Cloudアプリケーションのブループリントを使用したオーディエンスとプロファイルのアクティベーション
description: Experience Platform でプロファイルおよびオーディエンスを管理し、Experience Cloud アプリケーションを使用して共有します。
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services
kt: 7722
exl-id: f36014e8-170d-47e1-b4ec-10c0ea70612d
source-git-commit: 5110ee2a7a079945475055cbcfdabf7cdcaa0ab5
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 75%

---

# Experience Cloudアプリケーションのブループリントを使用したオーディエンスとプロファイルのアクティベーション

Experience Platform でプロファイルおよびオーディエンスを管理し、Experience Cloud アプリケーションを使用して共有します。Experience Platform でリッチな顧客セグメントおよびインサイトを構築および共有し、Experience Cloud アプリケーションを使用して共有します。

Experience Cloudアプリケーションを使用したアクティベーションは、 [既知の顧客アクティベーションブループリント](known.md).

## 使用例

* Experience Cloud による顧客インタラクションチャネルをまたいでパーソナライズおよびターゲット設定します。
* Experience Platform と Experience Cloud アプリケーションの間でオーディエンスおよびプロファイルデータを共有します。
* オンラインの行動データやデータサイエンスモデルなどのマルチチャネルデータから豊富な洞察を構築して、Experience Cloud アプリケーションと共有できる Experience Platform のリアルタイム顧客プロファイルを充実させます。

## アプリケーション

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]
* Experience Platform Activation
* Experience Cloud アプリケーション
   * Adobe Audience Manager
   * Adobe Target
   * Adobe Campaign
   * Journey Optimizer
   * Marketo Engage
   * Adobe Commerce
   * Customer Journey Analytics

## アーキテクチャ

Experience Platform と Experience Cloud アプリケーションの統合に関する追加のアーキテクチャ図については、[Experience Platform およびアプリケーションアーキテクチャの節](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=ja)を参照してください。

### Experience Cloudアプリを使用したオーディエンスとプロファイルのアクティベーション

<img src="../experience-platform/assets/aep+apps_horizontal.svg" alt="Experience Cloudアプリケーションを使用したオーディエンスとプロファイルのアクティベーションのリファレンスアーキテクチャ" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />
<br>

## ガードレール

[オーディエンスとプロファイルのアクティベーションの概要ページのガードレール](overview.md)および[デプロイメントガードレール](../experience-platform/deployment/guardrails.md)のページを参照してください。

## 実装に関する考慮事項

* プロファイルデータを宛先に共有するには、宛先ペイロードの宛先で使用される特定の ID 値を含める必要があります。ターゲットの宛先に必要な ID は、Platform に取り込まれ、[!UICONTROL リアルタイム顧客プロファイル]の ID として設定される必要があります。

### Real-time Customer Data PlatformからAudience Managerへのオーディエンスの共有

* 詳しくは、次のドキュメントを参照してください。[Audience Manager およびその他の Experience Cloud ソリューションを使用した Experience Platform セグメント共有](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ja).

* RT-CDP のオーディエンスメンバーシップは、セグメント評価が完了し、セグメント評価がバッチで行われたかストリーミングで行われたかに関わらず、リアルタイム顧客プロファイルに書き込まれるとすぐに、ストリーミング方式で Audience Manager に共有されます。
* 選定されたプロファイルに、関連するプロファイルデバイスの地域ルーティング情報が含まれる場合、RTCDP からのオーディエンスメンバーシップは、関連する Audience Manager エッジ上でストリーミング方式で選定されます。地域ルーティング情報が過去 14 日間のタイムスタンプを持つプロファイルに適用された場合、ストリーミングの Audience Manager Edge エッジで評価されます。RTCDP からのプロファイルに地域ルーティング情報が含まれていない場合、または地域ルーティング情報が 14 日以上前のものである場合、RTCDP オーディエンスメンバーシップは、バッチベースの評価とアクティブ化のために Audience Manager ハブロケーションに送信されます。
* 地域ルーティング情報により、これらのプロファイルはエッジのアクティベーションの対象となり、RTCDP からのセグメント認定の数分以内にアクティベートされます。エッジのアクティベーションの対象とならないプロファイルは Audience Manager ハブで選定され、処理に12～24 時間かかる場合があります。
* Audience Manager プロファイルが保存されている Edge の地域ルーティング情報は、Audience Manager、Visitor ID サービス、Analytics、Launch、または web SDK から直接、XDM フィールドグループ「データキャプチャ地域情報」を使用して、個別のプロファイルレコードクラスのデータセットとして Experience Platform に収集することが可能です。詳しくは、地域情報の取得に関するドキュメントを、こちらの[リンク](https://experienceleague.adobe.com/docs/id-service/using/reference/regions.html?lang=ja)から参照してください。
* Experience Platform から Audience Manager にオーディエンスが共有されるアクティベーションシナリオでは、次の ID が自動的に共有されます。ECID、IDFA、GAID、ハッシュ化されたメールアドレス（EMAIL_LC_SHA256）、AdCloud ID。現在、カスタムの名前空間は共有されません。
* 必須の宛先 ID が[!UICONTROL リアルタイム顧客プロファイル]に含まれている場合、または[!UICONTROL リアルタイム顧客プロファイル]内の ID が Audience Manager でリンクされる必須の宛先 ID と関連付けられる場合、Experience Platform からのオーディエンスは、Audience Manager 宛先を使用して共有できます。

### Real-time Customer Data Platformから Target へのオーディエンスの共有

* 詳しくは、 [既知の顧客のパーソナライゼーション — Target および RTCDP ブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/known-personalization.html?lang=ja) を参照してください。

### Real-time Customer Data Platformから Campaign およびJourney Optimizerへのオーディエンスの共有

* 詳しくは、 [顧客ジャーニーのブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=ja) を参照してください。

### Real-time Customer Data PlatformからMarketo Engageへのオーディエンスの共有

* 詳しくは、 [B2B アクティベーションブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=ja) Real-time Customer Data PlatformからMarketo Engageへのプロファイルとオーディエンスの共有に関する詳細

### Real-time Customer Data PlatformからCustomer Journey Analyticsへのオーディエンスの共有

* 詳しくは、 [RTCDP オーディエンスがCustomer Journey Analyticsと共有](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=ja) Real-time Customer Data PlatformオーディエンスのCustomer Journey Analyticsへの共有に関する追加情報

## 関連ドキュメント

* [[!UICONTROL Real-time Customer Data Platform] 製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連するビデオとチュートリアル

* [[!UICONTROL Real-time Customer Data Platform] 概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [のデモ [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)
