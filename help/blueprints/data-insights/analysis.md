---
title: データ分析とインテリジェンスブループリント
description: Adobe [!DNL Experience Platform]  （AEM）を使用して、データレイク内のデータに関する探索的クエリと分析を実行します。
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 59%

---

# データ分析とインテリジェンスのブループリント

データ分析とインテリジェンスには、データレイク内に存在するデータの探索的クエリと分析を実行する [!DNL Experience Platform] ークフロー内の機能が含まれます。

[!DNL Experience Platform] の [!UICONTROL &#x200B; クエリサービス &#x200B;] を使用すると、データに対して SQL クエリを実行できます。

[!DNL Experience Platform] を使用すると、サードパーティの SQL クライアント、インターフェイス、およびBusiness Intelligence（BI）ツールとの接続が、[!DNL PostgreSQL] プロトコルを使用して、[!DNL Experience Platform] 内のデータに直接接続し、アクセスし、クエリを実行できます。

## ユースケース

* インタラクティブクエリとデータの集計
* 調査および検証用に取り込まれたデータに対する行および列アクセス
* ビジネスインテリジェンスツールを使用したデータのダッシュボード表示およびビジュアライゼーション

クエリサービスのその他の一般的な使用例については、[クエリサービスのユースケース](https://experienceleague.adobe.com/docs/experience-platform/query/use-cases/abandoned-browse.html?lang=ja)で概要を説明します

## アプリケーション

* アドビ [!DNL Experience Platform]

## アーキテクチャ

<img src="assets/data_exploration.svg" alt="エンタープライズデータ調査およびレポートブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

## ガードレール

ベストプラクティスとガードレールについての詳細は、クエリサービス製品ドキュメントを参照してください。[クエリサービスガイダンス](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ja)

## 実装手順

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. [ データの [!DNL Experience Platform] への取り込み ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)。
1. データが[[!UICONTROL クエリサービス]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=ja)で使用可能であることを確認します。
1. [ビジュアライゼーション、データクエリおよび調査用に、ビジネスインテリジェンスツールおよび SQL クライアントを[!UICONTROL クエリサービス]](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=ja)に接続します。

## 関連ドキュメント

* [Adobe [!DNL Experience Platform]  インテリジェンス製品の説明 ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL クエリサービス]ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja)
