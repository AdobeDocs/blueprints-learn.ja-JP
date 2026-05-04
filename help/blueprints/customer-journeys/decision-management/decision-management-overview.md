---
title: 意思決定管理のブループリント
description: カスタマージャーニーをまたいでパーソナライズされたオファーを配信します。
solution: Experience Platform, Journey Optimizer
exl-id: 1bc9335c-5321-4d0c-939e-4f402e2e8f51
TQID: https://experienceleague.adobe.com/FWKq0QzEzCXp8TrfECmhY4E3ocA4zZkTGyHrrKQCOBw
product_v2: id: cb954087-f4fc-4456-afb9-e939cabcdc79id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: d998adac-2f81-400b-a669-d07bb196e4ebid: daec7ead-f475-492a-a3b3-02ae08565d6fid: df64005d-8f9a-422e-ba4d-c6f6dc3454b4id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2: id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74id: fa683eda-48de-4558-af32-2673edcd44fe
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d00e9f03-e50b-4162-b143-0c0817c937c2id: e0eb8757-182f-49f3-94a4-1587d16f5094id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 731
ht-degree: 76%

---

# Journey Optimizer – 意思決定管理ブループリント

[意思決定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)については、次のドキュメントを参照してください

意思決定管理に関連するガードレールについては、次のドキュメントを参照してください。 [意思決定管理ガードレール ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails#decision-management.html)

アドビの意思決定管理は、Adobe Journey Optimizer の一部として提供されるサービスです。 このブループリントは、アプリケーションのユースケースと技術的機能の概要を示し、意思決定管理を構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

Journey Optimizer は、あらゆるタッチポイントにわたり、適切なタイミングで、顧客に最適なオファーとエクスペリエンスを提供するために使用されます。 意思決定管理では、さまざまなオファーを一元管理するライブラリと、Adobe Experience Platformで作成されたリアルタイムプロファイルにルールと定義を適用する意思決定エンジンを利用して、容易にパーソナライズできます。 これにより、適切なタイミングで適切なオファーを簡単に送信できるようになります。

意思決定管理機能は、次の 2 つの主要なコンポーネントで構成されます。

* 一元化オファーライブラリは、オファーを構成する様々な要素を作成および管理し、そのルールと制約を定義するインターフェイスです。
* オファー決定エンジンは、オファーを配信する適切な時間、顧客、チャネルを選択するために、Adobe Experience Platform のデータとリアルタイム顧客プロファイルおよびオファーライブラリを利用します。

<img src="images/offers_overview.png" alt="意思決定管理" style="width:100%; border:1px solid #4a4a4a" />

意思決定管理は、エッジ上またはハブを介して、2 つの方法のいずれかでデプロイできます。 これらのメソッドのそれぞれには、以下に示す各ブループリントで概要を説明するように、サービスを動作させるための特定のインターフェイスとプロトコルのセットがあります。 追加の詳細は、[意思決定管理ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html?lang=ja)でも入手することができます。

## ハブでの意思決定管理

1 つは、単一のデータセンターアーキテクチャである Adobe Experience Platform Hub を通じて行う方法です。 ハブアーキテクチャは、低遅延や高スループットが要求されないが、顧客プロファイルを詳細に把握する必要がある顧客体験に最適です。たとえば、キオスクや担当者が支援するエクスペリエンス（コールセンターや対面でのやり取りなど）に提供されるオファー決定事項などがあります。 電子メール、SMS メッセージ、プッシュ通知やアウトバウンドキャンペーンに挿入されるオファーも、ハブアプローチを利用します。 ハブでの意思決定管理について詳しくは、[ハブでの意思決定管理](decision-management-hub.md)ブループリントを参照してください。

* オファーの適格性は、すべての属性とエクスペリエンスイベントを含む、完全なリアルタイム顧客プロファイルに対して機能します。

### ハブでの意思決定管理のユースケース

* キオスクおよびストアエクスペリエンスに関してパーソナライズされたオファー。
* コールセンターやセールスインタラクションなど、エージェントの支援によってパーソナライズされたオファー。
* 電子メール、SMS、またはその他のアウトバウンドインタラクションに含まれるオファー。
* クロスチャネルのジャーニーの実行 - Adobe Journey Optimizer を通じて、web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

### ハブでの意思決定管理に関する技術上の考慮事項

* オーディエンスメンバーシップ、属性、エクスペリエンスイベントを含む、完全なリアルタイム顧客プロファイルへのアクセス。

## エッジでの意思決定管理

2つ目のアプローチは、エクスペリエンス [!DNL Edge Network]を介したもので、これはグローバルに分散された地理的に配置されたインフラストラクチャであり、高速なサブセカンドおよびミリ秒単位のエクスペリエンスを提供します。 レイテンシを最小限に抑えるために、消費者の地理的位置に最も近いエッジインフラストラクチャによって実行される最終消費者エクスペリエンス。 Edge 上の意思決定管理は、web やモバイルのインバウンドパーソナライズ機能リクエストなどのリアルタイムの顧客体験を提供するように設計されています。 ハブの意思決定管理について詳しくは、[ハブの意思決定管理](decision-management-edge.md)ブループリントを参照してください。

### エッジでの意思決定管理のユースケース

* Web またはモバイルインバウンドエクスペリエンスを使用したオンラインパーソナライズ機能。
* クロスチャネルのジャーニーの実行 - Adobe Journey Optimizer を通じて、web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

### エッジに関する技術上の考慮事項に関する意思決定管理

* エッジの Real-time Profile にアクセスします。 プロファイルで使用できるのは、エッジから推定されたオーディエンスとプロファイル属性のみです。

## 関連ドキュメント

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
* [Adobe Journey Optimizer 意思決定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)
* [Adobe Journey Optimizerの製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe Decision Managementの製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)
