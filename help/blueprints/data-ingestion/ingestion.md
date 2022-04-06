---
title: データ準備と取り込みブループリント
description: このブループリントは、Adobe Experience Platform でデータを取り込んで準備するためのすべての方法を示しています。
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1
source-git-commit: 798dec7767938b85d0b8c41438a0782ef179bf68
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 100%

---

# データ準備と取り込みブループリント

データ準備と取り込みブループリントは、データを準備して Adobe Experience Platform に取り込むためのすべての方法を網羅しています。

データ準備には、エクスペリエンスデータモデル（XDM）スキーマへのソースデータのマッピングが含まれます。また、データ変換（日付形式、フィールドの分割／連結／コンバージョン、レコードの結合／キー更新など）の実行も含まれます。データ準備は、顧客データを統合して、集計／フィルタリングされた分析を提供するのに役立ちます。これには、レポート作成や顧客プロファイルの組み立て／データサイエンス／アクティベーションのためのデータ準備が含まれます。

## アーキテクチャ

<img src="../experience-platform/assets/aep_data_flow.svg" alt="データ準備と取り込みブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

## データ取り込みガードレール

次の図は、Adobe Experience Platform にデータを取り込む際の平均パフォーマンスのガードレールとレイテンシを示しています。

<img src="../experience-platform/assets/aep_data_flow_guardrails.svg" alt="Experience Platform データフロー" style="border:1px solid #4a4a4a" width="90%" />

## データ取り込み方法

| 取り込みの方法 | 説明 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Web／Mobile SDK | レイテンシ：<ul><li>リアルタイム - Edge Network への同じページの収集</li><li>プロファイルへのストリーミングの取り込み 最大 1 分</li><li>データレイクへのストリーミングの取り込み（マイクロバッチ 最大 15 分）</ul>ドキュメント： <ul><li>[Web SDK](https://experienceleague.adobe.com/docs/web-sdk.html?lang=ja)</li><li>[Web SDK を使用した Adobe Experience Cloud の実装チュートリアル](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ja)</li><li>[Mobile SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)</li><li>[モバイルアプリでの Adobe Experience Cloud の実装のチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=ja)</li></ul> |
| ストリーミングソース | レイテンシ：<ul><li>リアルタイム - Edge Network への同じページの収集</li><li>プロファイルへのストリーミングの取り込み 最大 1 分</li><li>データレイクへのストリーミングの取り込み（マイクロバッチ 最大 15 分）</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja#connectors) |
| ストリーミング API | レイテンシ：<ul><li>リアルタイム - Edge Network への同じページの収集</li><li>プロファイルへのストリーミングの取り込み 最大 1 分</li><li>データレイクへのストリーミングの取り込み（マイクロバッチ 最大 15 分）</li><li>7 GB/時間</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=ja#what-can-you-do-with-streaming-ingestion%3F) |
| ETL ツール | Experience Platform に取り込む前に、ETL ツールを使用してエンタープライズデータを変更および変換します。<br><br>レイテンシ：<ul><li>タイミングは外部 ETL ツールのスケジュールに依存し、その後、取り込みに使用される方法に基づいて、標準的な取り込みガードレールが適用されます。</li></ul> |
| バッチソース | ソースからのスケジュールされた取得<br>レイテンシ：最大 200 GB/時間<br><br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html?lang=ja) |
| バッチ API | レイテンシ：<ul><li>プロファイルへのバッチ取り込みはサイズおよびトラフィックの負荷に依存 最大 45 分</li><li>データレイクへのバッチ取り込みはサイズおよびトラフィックの負荷に依存</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=ja#batch) |
| アドビアプリケーションコネクタ | Adobe Experience Cloud アプリケーションから供給されるデータを自動的に取り込みます<ul><li>Adobe Analytics：[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ja#connectors)および[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=ja)</li><li>Audience Manager：[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ja#connectors)および[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html?lang=ja)</li></ul> |


## データ準備方法

| データ準備の方法 | 説明 |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!UICONTROL Data Science Workspace] - データ準備 | モデル主導の変換、スクリプト化された変換。<br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=ja) |
| 外部 ETL ツール（[!DNL Snaplogic]、[!DNL Mulesoft]、[!DNL Informatica] など） | ETL ツールで複雑な変換を実行し、標準 Experience Platform [!UICONTROL フローサービス] API またはソースコネクタを使用して、結果のデータを取り込みます。 |
| [!UICONTROL クエリサービス] - データ準備 | 結合、分割、結合、変換、クエリ、フィルターの各データを新しいデータセットにまとめます。Create Table as Select（CTAS）<br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja#sql)の使用 |
| XDM マッパーとデータ準備機能（ストリーミングとバッチ） | Experience Platform の取り込み時に、CSV 形式または JSON 形式のソース属性を XDM 属性にマップします。<br>取り込まれたデータに対して、関数を計算します（データの形式、分割、連結など）。<br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=ja) |

## 関連するブログ投稿

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform’s Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
