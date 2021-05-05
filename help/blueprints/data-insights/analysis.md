---
title: データ分析とインテリジェンスのブループリント
description: このブループリントは、Adobe Experience Platform 内の機能を示し、データレイクに存在するデータの探索的クエリおよび分析を実行します。
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: 6365fa00a77ba22774b2d6de3e882a3e09dcae0f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 29%

---

# データ分析とインテリジェンスのブループリント

データ分析とインテリジェンスは、Adobe Experience Platform内でデータレーク内のデータの探索クエリと分析を実行する機能を備えています。

Experience Platformの[!UICONTROL クエリサービス]では、SQLクエリをデータに対して実行できます。 [!UICONTROL Data Science ] Workspaceを使用すると、データ調査、データ科学、および機械学習のワークロードをデータに対して実行できます。

また、Experience Platformでは、サードパーティのSQLクライアント、インターフェイス、およびBusiness Intelligence(BI)ツールとの接続を[!DNL PostgreSQL]プロトコルを使用して、Experience Platform内のデータに直接接続し、アクセスし、クエリできます。

設計図の詳細に示すように、クエリのタイムアウトと、クエリ結果に含まれるデータ量に適用されるガードレールもあります。

## ユースケース

* インタラクティブクエリとデータの集計
* 調査および検証用に取り込まれたデータに対する行および列アクセス
* ビジネスインテリジェンスツールを使用したデータのダッシュボード表示およびビジュアライゼーション

## アプリケーション

* Adobe Experience Platform

## 構造

<img src="assets/data_exploration.svg" alt="エンタープライズデータ調査およびレポートブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

ベストプラクティスとガードレールの詳細については、『クエリサービス製品ドキュメント』を参照してください。
[クエリサービスガイダンス](https://experienceleague.adobe.com/docs/experience-platform/query/best-practices/writing-queries.html?lang=en#best-practices)

## 実装手順

1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) スキーマを作成します。
1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) データセットを作成します。
1. [データをプラットフォームに取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)。
1. データが、[!UICONTROL クエリサービス]および[!UICONTROL データサイエンスワークスペース]で生のアクセスとクエリに使用できることを確認します。
1. Business IntelligenceツールとSQLクライアントを[!UICONTROL クエリサービス]に接続して、視覚化、データクエリ、調査を行います。

## 関連ドキュメント

* [Adobe Experience Platform インテリジェンス製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [クエリサービスドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja)
