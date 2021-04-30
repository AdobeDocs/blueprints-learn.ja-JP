---
title: データ準備と取り込みブループリント
description: このブループリントは、Adobe Experience Platform でデータを取り込んだり準備したりするためのあらゆる方法を示します。
solution: Experience Platform,Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1,5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
translation-type: tm+mt
source-git-commit: 9e0954334e8b8a8c5bf52651611e7afa165f6d21
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 84%

---

# データ準備と取り込みブループリント

データ準備と取り込みブループリントは、データを準備したり Adobe Experience Platform に取り込んだりするためのあらゆる方法を網羅しています。

データの準備には、ソースデータとエクスペリエンスデータモデル(XDM)スキーマとのマッピングが含まれます。 また、データ変換（日付形式、フィールドの分割／連結／コンバージョン、レコードの結合／キー更新など）の実行も含まれます。データ準備は、顧客データを統合して、集計／フィルタリングされた分析を提供するのに役立ちます。これには、レポート作成や顧客プロファイルの組み立て／データサイエンス／アクティベーションのためのデータ準備が含まれます。

## 構造

<img src="assets/data_ingestion.svg" alt="データ準備と取り込みブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />

## データ取り込み方法

| 取り込みの方法 | 説明 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| web／Mobile SDK | 待ち時間：<ul><li>リアルタイム - Edge Network への同じページの収集</li><li>プロファイルへのストリーミングの取り込み ～ 1 分</li><li>データレイクへのストリーミングの取り込み（マイクロバッチ ～ 15 分）</ul>ドキュメント： <ul><li>[Web SDK](https://experienceleague.corp.adobe.com/docs/web-sdk.html)</li><li>[Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)</li></ul> |
| ストリーミングソース | 待ち時間：<ul><li>リアルタイム - Edge Network への同じページの収集</li><li>プロファイルへのストリーミングの取り込み ～ 1 分</li><li>データレイクへのストリーミングの取り込み（マイクロバッチ ～ 15 分）</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja#connectors) |
| ストリーミング API | 待ち時間：<ul><li>リアルタイム - Edge Network への同じページの収集</li><li>プロファイルへのストリーミングの取り込み ～ 1 分</li><li>データレイクへのストリーミングの取り込み（マイクロバッチ ～ 15 分）</li><li>7 GB/時間</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=ja#what-can-you-do-with-streaming-ingestion%3F) |
| ETL ツール | Experience Platform に取り込む前に、ETL ツールを使用してエンタープライズデータを変更および変換します。<br><br>待ち時間：<ul><li>タイミングは外部 ETL ツールのスケジュールに依存し、その後、取り込みに使用される方法に基づいて、標準的な取り込みガードレールが適用されます。</li></ul> |
| バッチソース | ソースからのスケジュールされた取得<br>待ち時間：～ 200 GB/時間<br><br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html?lang=ja) |
| バッチ API | 待ち時間：<ul><li>プロファイルへのバッチ取り込みはサイズおよびトラフィックの負荷に依存 ～45 分</li><li>データレイクへのバッチ取り込みはサイズおよびトラフィックの負荷に依存</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=ja#batch) |
| アドビアプリケーションコネクタ | Adobe Experience Cloud アプリケーションから供給されるデータを自動的に取り込みます<ul><li>Adobe Analytics：[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ja#connectors)および[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=ja)</li><li>Audience Manager：[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ja#connectors)および[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html?lang=ja)</li></ul> |


## データ準備方法

| データ準備の方法 | 説明 |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!UICONTROL Data Science Workspace]  — データ準備 | モデル主導の変換、スクリプト化された変換。<br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=ja) |
| 外部ETLツール（[!DNL Snaplogic]、[!DNL Mulesoft]、[!DNL Informatica]など） | ETLツールで複雑な変換を実行し、標準Experience Platform[!UICONTROL フローサービス]APIまたはソースコネクタを使用して結果のデータを取り込みます。 |
| [!UICONTROL クエリサービス]  — データ準備 | 結合、分割、結合、変換、クエリ、フィルタの各データを新しいデータセットにまとめます。 テーブルを選択として作成(CTAS) <br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja#sql)の使用 |
| XDMマッパーとデータ準備機能（ストリーミングとバッチ） | Experience Platformの取り込み時に、CSV形式またはJSON形式のソース属性をXDM属性にマップします。<br>取り込まれたデータに対して、関数を計算します（データの形式、分割、連結など）。<br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=ja) |

## 関連するブログ投稿

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform’s Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
