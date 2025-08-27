---
title: エッジでの意思決定管理のブループリント
description: 複数のチャネルをまたいで、リアルタイムの web エクスペリエンスやモバイルエクスペリエンスを含むパーソナライズされたオファーを顧客に提供します。
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: b24b1200e605914c501c0f98562ca40beee1138e
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 68%

---

# Journey Optimizer - Edge ブループリントの [!DNL Decision Management]

[!DNL Decision Management] は、[!DNL Journey Optimizer] の一部として提供されるサービスです。 このブループリントは、アプリケーションのユースケースと技術的機能の概要を示し、意思決定管理を構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

>[!MORELIKETHIS]
>
>[!DNL Decision Management] について詳しくは、[ ブループリントの概要 ](decision-management-overview.md) または [ 製品ドキュメント ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja) を参照してください。

[!DNL Decision Management] は、2 つの方法のいずれかでデプロイできます。 1 つ目は、単一のデータセンターアーキテクチャである [!DNL Experience Platform] Hub を介する方法です。 「ハブ」アプローチでは、オファーは 2 回目の待ち時間で実行、パーソナライズ、配信されます。したがって、ハブアーキテクチャは、1 秒未満の待ち時間を必要としない顧客体験に最適です。例えば、コールセンターや対面でのやり取りなど、キオスクやエージェント支援エクスペリエンスに提供されるオファー判定が含まれます。

2 つ目のアプローチは、Experience Platform [!DNL Edge Network] を介した方法です。これは、世界中に分散された地理的に配置されたインフラストラクチャであり、秒未満とミリ秒の高速なエクスペリエンスを提供します。 エンドユーザーのエクスペリエンスは、待ち時間を最小限に抑えるために、消費者の位置情報に最も近いEdge インフラストラクチャによって実行されています。 Edgeの [!DNL Decision Management] は、リアルタイムのカスタマーエクスペリエンスを提供するように設計されています。 これには、Web やモバイルのインバウンドパーソナライズ機能リクエストなどのエクスペリエンスが含まれます。

このブループリントでは、Edge 上での意思決定管理の詳細を説明します。

ハブでの意思決定管理について詳しくは、[ハブでの意思決定管理](decision-management-hub.md)ブループリントを参照してください。

## エッジでの意思決定管理のユースケース

* プロファイルコンテキストの待ち時間が 15 分の待ち時間より厳密に低く、意思決定管理の実行が 1 秒未満のストリーミングのユースケース。
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

[ ガードレールとエンドツーエンドの待ち時間のガイダンス ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html)

## 関連ドキュメント

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
* [Adobe Journey Optimizer 意思決定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe 意思決定管理製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)
