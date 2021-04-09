---
title: データの準備と取り込みのBlueprint
description: この設計図は、Adobe Experience Platformでデータを取り込み、調製する方法をすべて示しています。
solution: Experience Platform,Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1,5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# データの準備と取り込みのBlueprint

データの準備と取り込みのブループリントには、データを準備し、Adobe Experience Platformに取り込むためのすべての方法が含まれます。

データの準備には、ソースデータとエクスペリエンスデータモデル(XDM)スキーマとのマッピングが含まれます。 また、日付形式、フィールド分割/連結/変換、レコードの結合/結合/再入力など、データに対する変換も実行されます。 データの準備は、顧客データの統合を支援し、レポートや顧客プロファイルの分析/データ科学/アクティベーションのためのデータを含む、集計/フィルタリングされたを提供します。

## 建築

<img src="assets/dataingest.svg" alt="データの準備と取り込みに関するBlueprintのリファレンス・アーキテクチャ" style="border:1px solid #4a4a4a" />

## データ取り込み方法

| 取り込み方法 | 説明 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Web/モバイルSDK | 待ち時間：<ul><li>リアルタイム — Edge Networkに対する同じページコレクション</li><li>プロファイルへのストリーミング取り込み：1分</li><li>データレークへのストリーミング取り込み（マイクロバッチから15分）</ul>ドキュメント： <ul><li>[Web SDK](https://experienceleague.corp.adobe.com/docs/web-sdk.html)</li><li>[モバイルSDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en)</li></ul> |
| ストリーミングソース | 待ち時間：<ul><li>リアルタイム — Edge Networkに対する同じページコレクション</li><li>プロファイルへのストリーミング取り込み：1分</li><li>データレークへのストリーミング取り込み（マイクロバッチから15分）</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors) |
| ストリーミングAPI | 待ち時間：<ul><li>リアルタイム — Edge Networkに対する同じページコレクション</li><li>プロファイルへのストリーミング取り込み：1分</li><li>データレークへのストリーミング取り込み（マイクロバッチから15分）</li><li>7 GB/時</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en#what-can-you-do-with-streaming-ingestion%3F) |
| ETLツール | ETLツールを使用して、企業データを変更し、Experience Platformに取り込む前に変換します。<br><br>待ち時間：<ul><li>タイミングは外部のETLツールのスケジュールに依存し、次に、標準のインジェストガードレールが、インジェストに使用される方法に基づいて適用されます。</li></ul> |
| バッチソース | ソースからのスケジュールされたフェッチ<br>遅延：～ 200 GB/時<br><br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[ビデオTutorials](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html) |
| バッチAPI | 待ち時間：<ul><li>サイズとトラフィックの負荷に応じて、プロファイルへのバッチ取り込みが45分以内に行われる</li><li>サイズとトラフィックの負荷に応じて、データレークへのバッチ取り込み</li></ul>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en#batch) |
| AdobeのApplication Connectors | Adobe Experience Cloudアプリケーションをソースとするデータを自動的に取り込む<ul><li>Adobe Analytics:[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en#connectors)と[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)</li><li>Audience Manager:[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en#connectors)と[ビデオチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html)</li></ul> |


## データの準備方法

| データの作成の方法 | 説明 |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!UICONTROL Data Science Workspace]  — データ準備 | モデル駆動変換、スクリプト変換。<br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en) |
| 外部ETLツール（[!DNL Snaplogic]、[!DNL Mulesoft]、[!DNL Informatica]など） | ETLツールで複雑な変換を実行し、標準Experience Platform[!UICONTROL フローサービス]APIまたはソースコネクタを使用して結果のデータを取り込みます。 |
| [!UICONTROL クエリサービス]  — データ準備 | 結合、分割、結合、変換、クエリ、フィルタの各データを新しいデータセットにまとめます。 テーブルを選択として作成(CTAS) <br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en#sql)の使用 |
| XDMマッパーとデータ準備機能（ストリーミングとバッチ） | Experience Platformの取り込み時に、CSV形式またはJSON形式のソース属性をXDM属性にマップします。<br>データの取り込み時に関数を計算するつまり、データの形式設定、分割、連結などを行います。<br>[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=en) |

## 関連するブログ投稿

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform’s Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
