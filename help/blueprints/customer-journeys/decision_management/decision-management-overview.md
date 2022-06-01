---
title: 決定管理の概要
description: カスタマージャーニーをまたいでパーソナライズされたオファーを配信する。
solution: Experience Platform, Journey Optimizer
source-git-commit: 5b2f7531cc05178127fb08d3fdafcbce70192ecd
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 40%

---

# Journey Optimizer — 決定管理の概要

判定管理について詳しくは、製品ドキュメントを参照してください。 [ここをクリック](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja)

アドビの判定管理は、Adobe Journey Optimizer の一部として提供されるサービスです。このブループリントは、アプリケーションの使用例と技術的機能の概要を示し、判定管理を構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

Journey Optimizerは、あらゆるタッチポイントにわたって適切なタイミングで顧客に最適なオファーとエクスペリエンスを提供するために使用されます。 決定管理を使用すると、マーケティングオファーの一元化されたライブラリと、Adobe Experience Platformが作成したリッチでリアルタイムなプロファイルにルールと制約を適用する決定エンジンによって、適切なオファーを適切なタイミングで顧客に送信できます。

決定管理機能は、次の 2 つの主要なコンポーネントで構成されます。

* 一元化オファーライブラリ：オファーを構成する様々な要素を作成および管理し、そのルールと制約を定義するインターフェイスです。
* オファー決定エンジンは、オファーを配信する適切な時間、顧客、チャネルを選択するために、Adobe Experience Platformのデータとリアルタイム顧客プロファイル、およびオファーライブラリを利用します。

<img src="../assets/offers_overview.png" alt="決定管理" style="width:100%; border:1px solid #4a4a4a" />

決定管理は、エッジ上またはハブを介して、2 つの方法のいずれかでデプロイできます。 これらの各メソッドには、以下に示す各ブループリントで概要を説明するように、サービスを動作させるための特定のインターフェイスとプロトコルのセットがあります。 追加の詳細は、決定管理ドキュメントでも入手できます [ここ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## ハブでの決定管理

1 つは、単一のデータセンターアーキテクチャである Adobe Experience Platform Hub を通じて行う方法です。「ハブ」アプローチでは、オファーは、500 ミリ秒を超えるレイテンシで実行、パーソナライズ、配信されます。したがって、ハブアーキテクチャは、1秒未満の遅延を必要としない顧客体験に最適です。たとえば、コールセンターや対面でのやり取りなど、キオスクやエージェント支援エクスペリエンスに提供されるオファー判定が含まれます。E メール、SMS メッセージ、プッシュ通知などのアウトバウンドキャンペーンに挿入されるオファーも、ハブアプローチを利用します。 ハブ上での判定管理について詳しくは、[ハブ上での判定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-hub.html?lang=en) ブループリントを参照してください。

* オファーの適格要件は、すべての属性やエクスペリエンスイベントを含む、完全なリアルタイム顧客プロファイルに対して操作できます

### ハブでの決定管理の使用例

* キオスクおよびストアエクスペリエンスに関してパーソナライズされたオファー。
* コールセンターやセールスインタラクションなど、エージェントの支援によってパーソナライズされたオファー。
* 電子メール、SMS、またはその他のアウトバウンドインタラクションに含まれるオファー。
* クロスチャネルのジャーニー実行 — Adobe Journey Optimizer を通じて、Web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

### ハブでの意思決定管理に関する技術上の考慮事項

* 1 秒あたりのリクエスト数= 2000
* 応答の待ち時間（500 ミリ秒未満）。
* オーディエンスメンバーシップ、属性、エクスペリエンスイベントを含む、完全なリアルタイム顧客プロファイルへのアクセス。

## エッジでの決定管理

2 つ目のアプローチは、Experience Edge ネットワークを介したものです。Experience Edge ネットワークは、地理的にグローバルに分散されたインフラストラクチャで、1 秒未満および 1 ミリ秒の高速なエクスペリエンスを提供します。レイテンシを最小限に抑えるために、消費者の地理的位置に最も近いエッジインフラストラクチャによって実行される最終消費者エクスペリエンス。Edge 上の判定管理は、Web やモバイルのインバウンドパーソナライゼーションリクエストなどのリアルタイムの顧客体験を提供するように設計されています。ハブ上での判定管理について詳しくは、[ハブ上での判定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-edge.html?lang=en)ブループリントを参照してください。

### エッジでの決定管理の使用例

* Web またはモバイルインバウンドエクスペリエンスを使用したオンラインパーソナライゼーション。
* クロスチャネルのジャーニー実行 — Adobe Journey Optimizer を通じて、Web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

### エッジに関する技術上の考慮事項に関する決定管理

* 1 秒あたりのリクエスト数= 5000
* 応答の待ち時間（250 ミリ秒未満）。
* エッジのリアルタイムプロファイルにアクセスします。 プロファイルで使用できるのは、エッジから推定されたオーディエンスとプロファイル属性のみです。
* 初めてのエクスペリエンスでパーソナライゼーションが必要な場合は、フルプロファイルを利用できるので、ハブが最適です。 初めてのエッジエクスペリエンスでは、エッジプロファイルがハブから同期する必要があります。 したがって、エッジからの最初のエクスペリエンスには、以前にハブにアップロードされたプロファイルデータは含まれません。

## 関連ドキュメント

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
* [Adobe Journey Optimizer 判定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe判定管理製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)