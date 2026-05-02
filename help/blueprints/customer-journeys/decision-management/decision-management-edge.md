---
title: エッジでの意思決定管理のブループリント
description: 複数のチャネルをまたいで、リアルタイムの web エクスペリエンスやモバイルエクスペリエンスを含むパーソナライズされたオファーを顧客に提供します。
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
TQID: https://experienceleague.adobe.com/SwjKOJIL5WidXtVuLCNbBpNz3mhe0EvD93IhMfxI1oY
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: df64005d-8f9a-422e-ba4d-c6f6dc3454b4
  - id: fe338112-e2ce-4876-8989-fc4d497613f1
subfeature_v2:
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c18d9e03-ac7d-4811-9c92-3e92ddc70ade
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 492
ht-degree: 67%

---

# Journey Optimizer - Edge ブループリントの[!DNL Decision Management]

>[!TIP]
>このブループリントは、Personalizationの[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)としても利用できます。

[!DNL Decision Management]は[!DNL Journey Optimizer]の一部として提供されるサービスです。 このブループリントは、アプリケーションのユースケースと技術的機能の概要を示し、意思決定管理を構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

>[!MORELIKETHIS]
>
>[!DNL Decision Management]について詳しくは、[&#x200B; ブループリントの概要](decision-management-overview.md)を参照するか、[製品ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)を参照してください。

[!DNL Decision Management]は、2つの方法のいずれかでデプロイできます。 1つ目は、[!DNL Experience Platform] ハブ経由です。これは、単一のデータセンターアーキテクチャです。 「ハブ」アプローチでは、オファーは 2 回目の待ち時間で実行、パーソナライズ、配信されます。 したがって、ハブアーキテクチャは、1 秒未満の待ち時間を必要としない顧客体験に最適です。例えば、コールセンターや対面でのやり取りなど、キオスクやエージェント支援エクスペリエンスに提供されるオファー判定が含まれます。

2つ目のアプローチは、Experience Platform [!DNL Edge Network]を介したもので、これはグローバルに分散された地理的に配置されたインフラストラクチャであり、高速なサブ秒およびミリ秒単位のエクスペリエンスを提供します。 消費者の位置情報に最も近いEdge インフラストラクチャによって実行されるエンドコンシューマーエクスペリエンスは、待ち時間を最小限に抑えます。 Edgeの[!DNL Decision Management]は、リアルタイムの消費者体験を提供するように設計されています。 これには、Web やモバイルのインバウンドパーソナライズ機能リクエストなどのエクスペリエンスが含まれます。

このブループリントでは、Edge 上での意思決定管理の詳細を説明します。

ハブでの意思決定管理について詳しくは、[ハブでの意思決定管理](decision-management-hub.md)ブループリントを参照してください。

## エッジでの意思決定管理のユースケース

* プロファイルコンテキストの待ち時間が15分未満で、意思決定管理の実行が2秒以下のストリーミングユースケース。
* Web またはモバイルインバウンドエクスペリエンスを使用したオンラインパーソナライズ機能。
* クロスチャネルのジャーニーの実行 - Adobe Journey Optimizer を通じて、web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

## アーキテクチャ

<img src="images/offers_edge.svg" alt="エッジでの意思決定管理のブループリント参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 統合パターン

| 統合 | 説明 |
| :-- | :--- |
| [Adobe Target を使用した意思決定管理](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=ja) | 意思決定管理を Adobe Target と統合して、オファーを Target エクスペリエンスとしてテストおよび配信することができます。 |

## ガードレール

* Journey Optimizer ガードレールに関しては、次の [Journey Optimizer ガードレール](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=ja)を参照してください。

* 意思決定管理ガードレールについては、次の[意思決定管理製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)を参照してください。

[ガードレールとエンドツーエンドのレイテンシーガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=ja)

## 関連ドキュメント

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
* [Adobe Journey Optimizer 意思決定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)
* [Adobe Journey Optimizerの製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe Decision Managementの製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)
