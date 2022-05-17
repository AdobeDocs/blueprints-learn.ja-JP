---
title: offer decisioningの概要
description: カスタマージャーニーをまたいでパーソナライズされたオファーを配信する。
solution: Experience Platform, Journey Optimizer
exl-id: f6271802-faab-4ffc-92d6-4c4d7d423ed4
source-git-commit: 8842b8637a30151577a93653c16b4d37e2cf7c27
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# Journey Optimizer -Offer decisioningの概要

決定管理について詳しくは、製品ドキュメントを参照してください。 [ここ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

Adobe判定管理は、Adobe Journey Optimizerの一部として提供されるサービスです。 このブループリントは、アプリケーションの使用例と技術的機能の概要を示し、Offer decisioningを構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

Journey Optimizerは、あらゆるタッチポイントにわたって適切なタイミングで顧客に最適なオファーとエクスペリエンスを提供するために使用されます。 offer decisioningは、マーケティングオファーの一元化されたライブラリと、Adobe Experience Platformが作成するリッチなリアルタイムプロファイルにルールと制約を適用する決定エンジンを使用して、適切なオファーを適切なタイミングで顧客に送信します。

決定管理機能は、次の 2 つの主要なコンポーネントで構成されます。

* 一元化オファーライブラリ：オファーを構成する様々な要素を作成および管理し、そのルールと制約を定義するインターフェイスです。
* オファー決定エンジンは、オファーを配信する適切な時間、顧客、チャネルを選択するために、Adobe Experience Platformのデータとリアルタイム顧客プロファイル、およびオファーライブラリを利用します。

<img src="../assets/offers_overview.png" alt="offer decisioning" style="width:100%; border:1px solid #4a4a4a" />

決定管理は、エッジ上またはハブを介して、2 つの方法のいずれかでデプロイできます。 これらの各メソッドには、以下に示す各ブループリントで概要を説明するように、サービスを動作させるための特定のインターフェイスとプロトコルのセットがあります。 追加の詳細は、決定管理ドキュメントでも入手できます [ここ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## ハブでの決定管理

1 つ目は、中央のデータセンターアーキテクチャであるAdobe Experience Platformハブを通じて行う方法です。 「ハブ」アプローチでは、オファーは、500 ミリ秒を超える待ち時間で実行、パーソナライズ、配信されます。 したがって、ハブアーキテクチャは、1 秒未満の待ち時間を要求しない顧客体験に最適です。例えば、コールセンターや人とのやり取りなど、キオスクやエージェントが支援するエクスペリエンスに提供するオファーの決定などです。 E メール、SMS メッセージ、プッシュ通知などのアウトバウンドキャンペーンに挿入されるオファーも、ハブアプローチを利用します。 ハブでの決定管理について詳しくは、 [ハブでの決定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-hub.html?lang=en) ブループリント。

### ハブでの決定管理の使用例

* キオスクおよびストアエクスペリエンスでパーソナライズされたオファー。
* コールセンターやセールスインタラクションなど、エージェントの支援によってパーソナライズされたオファー。
* E メール、SMS、またはその他のアウトバウンドインタラクションに含まれるオファー。
* クロスチャネルのジャーニー実行 — Adobe Journey Optimizerを通じて、Web、モバイル、E メールおよびその他のインタラクションチャネル間の一貫性を提供します。

## エッジでの決定管理

2 つ目のアプローチは、Experience Edge ネットワークを介して行われます。Experience Edge ネットワークは、地理的にグローバルに分散されたインフラストラクチャで、2 秒および 1 ミリ秒の高速なエクスペリエンスを提供します。 待ち時間を最小限に抑えるために、消費者の地域に最も近いエッジインフラストラクチャによって実行されるエンドコンシューマーエクスペリエンス。 Edge 上の決定管理は、Web やモバイルのインバウンドパーソナライゼーションリクエストなどのリアルタイムのコンシューマーエクスペリエンスを提供するように設計されています。 エッジでの決定管理について詳しくは、 [エッジでの決定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-edge.html?lang=en) ブループリント。

### エッジでの決定管理の使用例

* Web またはモバイルインバウンドエクスペリエンスを使用したオンラインパーソナライゼーション。
* クロスチャネルのジャーニー実行 — Adobe Journey Optimizerを通じて、Web、モバイル、E メールおよびその他のインタラクションチャネル間の一貫性を提供します。

## 関連ドキュメント

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer Decision Management](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Adobe Journey Optimizer Product Description](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [AdobeOffer decisioningの製品説明](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
