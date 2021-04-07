---
title: データ分析とインテリジェンスのブループリント
description: この設計図は、Adobe Experience Platform内で、データレーク内に存在するデータの調査クエリと分析を実行する機能を示しています。
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: 77ddc003d4328074ad269de5837a02f5e6d6add5
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# データ分析とインテリジェンスのブループリント

データ分析とインテリジェンスは、Adobe Experience Platform内でデータレーク内のデータの探索クエリと分析を実行する機能を備えています。

Experience Platformのクエリサービスを使用すると、SQLクエリをデータに対して実行できます。 Data Science Workspaceを使用すると、データ調査、データ科学、および機械学習のワークロードをデータに対して実行できます。

さらに、Experience Platformは、サードパーティのSQLクライアント、インタフェース、およびBusiness Intelligence(BI)ツールとの接続を、PostgreSQLプロトコルを使用して、Experience Platform内のデータに直接接続し、アクセスし、クエリすることを可能にします。

シナリオの詳細に示すように、クエリのタイムアウトと、クエリ結果に含まれるデータ量に適用されるガードレールもあります。

## 使用例

* データのインタラクティブなクエリと集計
* 取り込んだデータに対する行と列のアクセス（調査と検証のため）
* Business Intelligenceツールを使用したデータのダッシュボーディングと視覚化

## アプリ

* Adobe Experience Platform

## シナリオ

| シナリオ | 説明 | Experience Cloudアプリケーション/サービス |
|---|---|---|
| **データ調査 — データの生クエリ** | <ul><li>対話型クエリ・ユーザー・インタフェースまたは接続されたSQLクライアントを使用して、データ・レークでSQLクエリを書き込み、実行します。 Data Science Workspaceは、Experience Platform内の生のデータをクエリし、インサイトを得るためにも使用できます。</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |
| **Enterprise Dashboarding** | <ul><li>Business IntelligenceツールをExperience Platformに接続して、ダッシュボーディングおよびレポートの使用例に応じてデータを視覚化します。</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |

## 建築

<img src="assets/dataexplore.svg" alt="企業データ調査およびレポートのブループリントのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* インタラクティブクエリの10分の制限時間
* UIに100レコードの制限が返されました
* SQLコネクタを介して返される50,000レコードの制限

## 導入手順

1. データレークにデータを取り込むためのデータセットとスキーマを設定します。
1. データを取り込みます。
1. データが、生のアクセスとクエリのためにクエリサービスとデータサイエンスワークスペースで使用できることを確認します。
1. Business IntelligenceツールとSQLクライアントをクエリサービスに接続して、視覚化、データクエリ、調査を行います。

## 関連ドキュメント

* [Adobe Experience Platformインテリジェンス製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [クエリサービスドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
