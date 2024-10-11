---
title: ハブでの意思決定管理のブループリント
description: キオスク、エージェント支援エクスペリエンス、電子メールやその他のアウトバウンド配信など、様々なチャネルで消費者にパーソナライズされたオファーを配信します。
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
source-git-commit: f6c4a0f39acdc177ac23c4314d2f50f793cbf270
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 80%

---

# ハブでの意思決定管理のブループリント

意思決定管理について詳しくは、製品ドキュメントの[こちら](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)と、意思決定管理の概要の[こちら](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=ja)を参照してください。

アドビの意思決定管理は、Adobe Journey Optimizer の一部として提供されるサービスです。このブループリントは、アプリケーションのユースケースと技術的機能の概要を示し、意思決定管理を構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

Journey Optimizer は、あらゆるタッチポイントにわたり、適切なタイミングで、顧客に最適なオファーとエクスペリエンスを提供するために使用されます。意思決定管理により、マーケティングオファーの一元化されたライブラリと、Adobe Experience Platform が作成するリッチなリアルタイムプロファイルにルールと制約を適用する決定エンジンを使用して、パーソナライズが容易になり、適切なオファーを適切なタイミングで顧客に送信することができます。

意思決定管理は、2 つの方法のいずれかでデプロイすることができます。1 つは、単一のデータセンターアーキテクチャである Adobe Experience Platform Hub を通じて行う方法です。「ハブ」アプローチでは、オファーは、500 ミリ秒を超える待ち時間で実行、パーソナライズ、配信されます。したがって、ハブアーキテクチャは、1 秒未満の待ち時間を必要としない顧客体験に最適です。例えば、コールセンターや対面でのやり取りなど、キオスクやエージェント支援エクスペリエンスに提供されるオファー判定が含まれます。電子メールやアウトバウンドキャンペーンに挿入されるオファーも、ハブアプローチを利用します。

2 つ目のアプローチは Experience [!DNL [!DNL Edge Network]] を介した方法です。これは、高速な秒未満およびミリ秒のエクスペリエンスを提供する、グローバルに分散した地理的に配置されたインフラストラクチャです。 レイテンシを最小限に抑えるために、消費者の地理的位置に最も近いエッジインフラストラクチャによって実行される最終消費者エクスペリエンス。Edge 上の意思決定管理は、web やモバイルのインバウンドパーソナライズ機能リクエストなどのリアルタイムの顧客体験を提供するように設計されています。

このブループリントは、ハブでの意思決定管理の詳細をカバーします。

ハブの意思決定管理について詳しくは、[ハブの意思決定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=ja)ブループリントを参照してください。

## ハブでの意思決定管理のユースケース

* プロファイルコンテキストの待ち時間が厳密でないストリーミングのユースケース - 15 分以上の待ち時間。
* キオスクおよびストアエクスペリエンスに関してパーソナライズされたオファー。
* コールセンターやセールスインタラクションなど、エージェントの支援によってパーソナライズされたオファー。
* 電子メール、SMS、モバイルプッシュ通知、またはその他のアウトバウンドインタラクションに含まれるオファー。
* 外部の ESP およびメッセージングシステムに、配信用のオファーを提供します。
* クロスチャネルのジャーニーの実行 - Adobe Journey Optimizer を通じて、web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

>[!IMPORTANT]
>
>追加情報およびコンテキストのためにプロファイルへのアクセスを必要とするオファーおよびジャーニーのユースケース用。 決定時に使用できるように、ハブ上のプロファイルにデータを取り込む際の関連する待ち時間を考慮することが重要です。 コンテキストがストリーミングまたはプロファイルに取り込まれ、オファーまたはジャーニーがオファーの決定から数秒または数分以内にそのコンテキストを使用可能にする必要がある場合、これらのシナリオはEdgeの意思決定管理で提供するのが最適です。

## アーキテクチャ

<img src="../assets/offers_hub.svg" alt="エッジでの意思決定管理のブループリント参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## ガードレール

* Journey Optimizer ガードレールに関しては、次の [Journey Optimizer ガードレール](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=ja)を参照してください。
* 意思決定管理ガードレールについては、次の[意思決定管理製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)を参照してください。

[ ガードレールとエンドツーエンドの待ち時間のガイダンス ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 実装パターン

* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html?lang=ja) との直接統合により、電子メール、SMS、アウトバウンドチャネルで実装。
* サーバー API ベースの意思決定管理の実装の場合、[判定 API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html?lang=ja) を使用します。
* メッセージ配信アプリケーションにオファーを一括で配信するバッチベースの判定を実装するには、 [バッチ判定 API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html?lang=ja) を使用します。
* エッジベースのリアルタイムエクスペリエンスの場合は、[エッジブループリントの意思決定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-edge.html?lang=ja)で概説されているように、Web／Mobile SDK またはエッジ判定 API を使用します。

## 関連ドキュメント

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
* [Adobe Journey Optimizer 意思決定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe 意思決定管理製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)
