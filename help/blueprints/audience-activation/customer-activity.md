---
title: サポートとセールスのシナリオのためのリアルタイムのプロファイルアクセス
description: '[!UICONTROL リアルタイム顧客プロファイル]を検索し、担当者がサポートおよび販売を支援する際のコンテキストを提供します。'
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
TQID: https://experienceleague.adobe.com/Ci9pUbGCLQ9uhlQ9l1na7A2NiI9CpCRMLrUSN6lSOnU
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: ba929a52-9339-4154-9487-317dc875a3c7
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 368
ht-degree: 54%

---

# サポートとセールスのシナリオのためのリアルタイムのプロファイルアクセス

>[!TIP]
>このブループリントは、「オーディエンスの構築とアクティベーション」の下の[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md)としても利用できます。

サポートおよびセールス シナリオのリアルタイム プロファイル アクセス ブループリントでは、外部アプリケーションが[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;]を使用してAdobe Experience Platformにアクセスする方法を示します。

外部アプリケーションは、API GET リクエストを使用して、プロファイルにアクセスできます。 これにより、プロファイルに格納された属性、イベント、セグメントメンバーシップおよびモデル主導の機能を、外部のアドビ以外のアプリケーションで使用できます。

この機能によって、顧客がコールセンターに問い合わせる際にリッチコンテキストを表示できます。 サポート担当者は、例えば、顧客のライフタイムバリュー、チャーン傾向またはマーケティングキャンペーンのエクスポージャーなどを表示できます。 また、販売担当者は、より多くのコンテキストや顧客へのインサイトというメリットを得られます。

>[!NOTE]
>
>ハブでのプロファイル検索は、web/モバイルのインバウンドパーソナライゼーションなど、スループットが高く、低遅延のユースケースを対象としたものではありません。 ハブでのプロファイル検索は、エージェントによるサポートやセールスインタラクションなど、低遅延のシナリオを目的としています。 web/モバイルのパーソナライゼーションやリアルタイムのオファー決定など、低遅延で高スループットのシナリオの場合は、Edge プロファイルを活用する必要があります。 Edge プロファイルは、Real-time Customer Data Platformの[&#x200B; カスタム Personalization Connection](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization)を通じてリアルタイム アクセスを有効にします。

## ユースケース

* 担当者がサポートするインタラクションに、詳細な消費者コンテキスト（サポートおよび販売エクスペリエンスなど）を提供します。 Experience Platform のプロファイルルックアップを使用して、担当者は、最近の購入、キャンペーンインタラクション、傾向、オーディエンスメンバーシップ、リアルタイム顧客プロファイルに格納されたその他の属性およびインサイトなど、消費者に対するより詳細なコンテキストを受け取ることができます。

## アーキテクチャ

<img src="assets/customer_activity_hub.svg" alt="顧客アクティビティハブブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## ガードレール

* [[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] データのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

## 関連ドキュメント

* [Adobe Experience Platform アクティベーション製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ja)
* [プロファイルガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [プロファイル検索API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
