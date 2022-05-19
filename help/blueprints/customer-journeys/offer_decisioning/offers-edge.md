---
title: エッジの Offer Decisioning
description: 複数のチャネルをまたいで、リアルタイムの Web エクスペリエンスやモバイルエクスペリエンスを含む、パーソナライズされたオファー顧客にを提供します。
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: 7f566536c4ff5a6af321d60058ad67c13c28bf64
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 93%

---

# Journey Optimizer — エッジの Offer Decisioning

決定管理について詳しくは、製品ドキュメントを参照してください。 [ここ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ja) とOffer decisioningの概要 [ここ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-overview.html)

アドビの判定管理は、Adobe Journey Optimizer の一部として提供されるサービスです。このブループリントは、アプリケーションのユースケースと技術的機能の概要を示し、Offer Decisioning を構成する様々なアーキテクチャコンポーネントと考慮事項について詳しく説明します。

判定管理は、2 つの方法のいずれかでデプロイすることができます。1 つは、単一のデータセンターアーキテクチャである Adobe Experience Platform Hub を通じて行う方法です。「ハブ」アプローチでは、オファーは 2 回目の遅延で実行、パーソナライズ、配信されます。したがって、ハブアーキテクチャは、1秒未満の遅延を必要としない顧客体験に最適です。たとえば、コールセンターや対面でのやり取りなど、キオスクやエージェント支援エクスペリエンスに提供されるオファー判定が含まれます。

2 つ目のアプローチは、Experience Edge ネットワークを介したものです。Experience Edge ネットワークは、地理的にグローバルに分散されたインフラストラクチャで、1 秒未満および 1 ミリ秒の高速なエクスペリエンスを提供します。レイテンシを最小限に抑えるために、消費者の地理的位置に最も近いエッジインフラストラクチャによって実行される最終消費者エクスペリエンス。Edge 上の判定管理は、リアルタイムの顧客体験を提供するように設計されています。これには、Web やモバイルのインバウンドパーソナライゼーションリクエストなどのエクスペリエンスが含まれます。

このブループリントでは、Edge 上での判定管理の詳細を説明します。

ハブ上での判定管理について詳しくは、[ハブ上での判定管理](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-hub.html) ブループリントを参照してください。

## エッジでの決定管理の使用例

* Web またはモバイルインバウンドエクスペリエンスを使用したオンラインパーソナライゼーション。
* クロスチャネルのジャーニー実行 — Adobe Journey Optimizer を通じて、Web、モバイル、電子メールおよびその他のインタラクションチャネル間の一貫性を提供します。

<br>

## アーキテクチャ

<img src="../assets/offers_edge.svg" alt="エッジブループリントの参照アーキテクチャ Offer Decisioning" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 統合パターン

| 統合 | 説明 |
| :-- | :--- |
| [Adobe Target を使用した Offer Decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=ja) | Offer Decisioning を Adobe Target と統合して、オファーを Target エクスペリエンスとしてテストおよび配信することができます。 |

## 前提条件

Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります。
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、を追加します エクスペリエンスイベントクラスベースのスキーマでは、ルールベースのイベントではないイベントをトリガーさせたい場合は「オーケストレーション eventID」フィールドグループを追加します。
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします

<br>

## ガードレール

* Journey Optimizer ガードレールに関しては、次の [Journey Optimizer ガードレール](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=ja)を参照してください。
* Offer Decisioning ガードレールに関しては、次の [Offer Decisioning 製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)を参照してください。

### データ取り込みガードレール

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:80%; border:1px solid #4a4a4a" />

<br>

### アクティベーションガードレール

<img src="../assets/ajo-activation-details-latency.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:80%; border:1px solid #4a4a4a" />

<br>

## 実装パターン

* Web サイトやモバイルアプリケーションにデプロイするために Web または Mobile SDK を使用して、SDK がデプロイされた Offer decisioning を実装します。
   * [Web／モバイル SDK ブループリント](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/data-ingestion/websdk.html?lang=ja)
   * [WebSDK](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html?lang=ja)
   * [MobileSDK](https://aep-sdks.gitbook.io/docs/)

または

* API サーバーからサーバーへのベースの実装の場合は、Edge Network Service API を使用して、Offer Decisioning の直接サーバー間実装を行います。
   * [Edge Network Server API ](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/deliver-offers.html?lang=ja)

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
* [Adobe Offer Decisioning 製品説明](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
