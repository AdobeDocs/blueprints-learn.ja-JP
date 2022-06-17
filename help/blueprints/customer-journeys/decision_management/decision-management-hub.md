---
title: ハブでの決定管理
description: キオスク、エージェント支援エクスペリエンス、電子メールやその他のアウトバウンド配信など、さまざまなチャネルで消費者にパーソナライズされたオファーを配信します。
solution: Experience Platform, Journey Optimizer
exl-id: 5a386e18-bbac-4216-a35f-0a5016785e4a
source-git-commit: 5b2f7531cc05178127fb08d3fdafcbce70192ecd
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 70%

---

# Journey Optimizer — ハブでの意思決定管理

決定管理について詳しくは、製品ドキュメントを参照してください。 [ここ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja) と決定管理の概要 [ここ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-overview.html)

アドビの判定管理は、Adobe Journey Optimizer の一部として提供されるサービスです。このブループリントは、アプリケーションの使用例と技術的機能の概要を示し、判定管理を構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

Journey Optimizerは、あらゆるタッチポイントにわたって適切なタイミングで顧客に最適なオファーとエクスペリエンスを提供するために使用されます。 決定管理を使用すると、マーケティングオファーの一元化されたライブラリと、Adobe Experience Platformが作成したリッチでリアルタイムなプロファイルにルールと制約を適用する決定エンジンによって、適切なオファーを適切なタイミングで顧客に送信できます。

判定管理は、2 つの方法のいずれかでデプロイすることができます。1 つは、単一のデータセンターアーキテクチャである Adobe Experience Platform Hub を通じて行う方法です。「ハブ」アプローチでは、オファーは、500 ミリ秒を超えるレイテンシで実行、パーソナライズ、配信されます。したがって、ハブアーキテクチャは、1秒未満の遅延を必要としない顧客体験に最適です。たとえば、コールセンターや対面でのやり取りなど、キオスクやエージェント支援エクスペリエンスに提供されるオファー判定が含まれます。電子メールやアウトバウンドキャンペーンに挿入されるオファーも、ハブアプローチを利用します。

2 つ目のアプローチは、Experience Edge ネットワークを介したものです。Experience Edge ネットワークは、地理的にグローバルに分散されたインフラストラクチャで、1 秒未満および 1 ミリ秒の高速なエクスペリエンスを提供します。レイテンシを最小限に抑えるために、消費者の地理的位置に最も近いエッジインフラストラクチャによって実行される最終消費者エクスペリエンス。Edge 上の判定管理は、Web やモバイルのインバウンドパーソナライゼーションリクエストなどのリアルタイムの顧客体験を提供するように設計されています。

このブループリントは、ハブ上での判定管理の詳細をカバーします。

ハブ上での判定管理について詳しくは、[ハブ上での判定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-edge.html)ブループリントを参照してください。

## ハブでの決定管理の使用例

* キオスクおよびストアエクスペリエンスに関してパーソナライズされたオファー。
* コールセンターやセールスインタラクションなど、エージェントの支援によってパーソナライズされたオファー。
* E メール、SMS、モバイルプッシュ通知、その他のアウトバウンドインタラクションに含まれるオファー。
* 外部の ESP およびメッセージングシステムに配信用のオファーを提供します。
* クロスチャネルのジャーニー実行 — Adobe Journey Optimizer を通じて、Web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

<br>

## アーキテクチャ

<img src="../assets/offers_hub.svg" alt="エッジブループリント上の参照アーキテクチャ決定管理" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 前提条件

Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります。
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、を追加します エクスペリエンスイベントクラスベースのスキーマでは、ルールベースのイベントではないイベントをトリガーさせたい場合は「オーケストレーション eventID」フィールドグループを追加します。
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします

<br>

## ガードレール

* Journey Optimizer ガードレールに関しては、次の [Journey Optimizer ガードレール](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=ja)を参照してください。
* 決定管理ガードレールについては、次を参照してください。 [決定管理製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html).
* 1 秒あたりのリクエスト数= 2000
* 応答の待ち時間（500 ミリ秒未満）。
* オーディエンスメンバーシップ、属性、エクスペリエンスイベントを含む、完全なリアルタイム顧客プロファイルへのアクセス。


### データ取り込みガードレール

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:80%; border:1px solid #4a4a4a" />

<br>

### アクティベーションガードレール

<img src="../assets/ajo-activation-details-latency.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:80%; border:1px solid #4a4a4a" />

<br>

## 実装パターン

* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/offers-e2e.html?lang=ja) との直接統合により、電子メール、SMS、アウトバウンドチャネルで実装。
* 決定管理のサーバー API ベースの実装の場合、 [判定 API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/decisioning-vs-edge-apis.html?lang=ja).
* メッセージ配信アプリケーションにオファーを一括で配信するバッチベースの判定を実装するには、 [バッチ判定 API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/batch-decisioning-api.html?lang=ja) を使用します。
* エッジベースのリアルタイムエクスペリエンスの場合は、Web/モバイル SDK または Edge Decisioning API を使用します ( [エッジブループリントの決定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-edge.html).
<br>

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. ジャーニー使用状況用のセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)

## 関連ドキュメント

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
* [Adobe Journey Optimizer 判定管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe判定管理製品の説明](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)