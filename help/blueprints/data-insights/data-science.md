---
title: プロファイルエンリッチメントブループリント用のカスタムデータサイエンス
description: このブループリントは、データサイエンスに基づくインサイトを Experience Platform に取り込んで、リアルタイム顧客プロファイルをエンリッチメントする方法を示します。
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 802507291f54dc3f253d469e7a64d78e34b75c6a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# プロファイルエンリッチメントブループリント用のカスタムデータサイエンス

プロファイルエンリッチメントのためのカスタムデータサイエンスブループリントは、データを使用して、モデルをトレーニング、デプロイ、スコアリングし、Experience Platform と Real-time Customer Data Platform に関する機械学習のインサイトを、データサイエンスおよび機械学習ツールから提供する方法を示します。モデル化されたインサイトを Experience Platform に取り込んで、リアルタイム顧客プロファイルをエンリッチメントすることができます。機械学習インサイトの例には、ライフタイム値、スコアリング、製品およびカテゴリの親和性、コンバージョン傾向、チャーン傾向が含まれます。

## 使用例

* 顧客データからインサイトを抽出し、パターンを発見し、このデータからモデルをトレーニングしてスコアを付けます。
* より詳細なパーソナライズ機能と最適化されたジャーニーのために、[!UICONTROL リアルタイム顧客プロファイル]をモデル主導のインサイトおよび属性でエンリッチメントします。
* 顧客のライフタイムバリュー、コンバージョン傾向やチャーン傾向、製品およびコンテンツの親和性、エンゲージメントスコアなどの顧客インサイトを判別するためのモデルをトレーニングおよびスコアリングします。

## アーキテクチャ

<img src="assets/data_science.svg" alt="プロファイルエンリッチメントのためのカスタムデータサイエンスブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

## ガードレール

* ガードレールの詳細と、データ サイエンスの結果を Experience Platform およびリアルタイム顧客プロファイルに取り込む際のエンドツーエンドのの遅延については、[デプロイメントガードレールドキュメント](../experience-platform/deployment/guardrails.md)を参照してください。

## 実装の手順

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. Experience Platform に[データを取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)。

モデル結果をリアルタイム顧客プロファイルに取り込む場合は、データを取り込む前に、必ず次の操作をおこなってください。

1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに[正しい ID および ID 名前空間を設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。

## 実装に関する考慮事項

* ほとんどの場合、モデルの結果はエクスペリエンスイベントではなく、プロファイル属性として取り込む必要があります。モデルの結果は、単純な属性文字列にすることができます。取り込むモデル結果が複数ある場合は、配列またはマップタイプのフィールドを使用することをお勧めします。
* 統合プロファイル属性データの毎日の書き出しである日別プロファイルスナップショットデータセットを利用して、プロファイル属性データに関するモデルのトレーニングをおこなうことができます。プロファイルスナップショットデータセットのドキュメントに[ここから](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=ja#profile-attribute-datasets)アクセスすることができます。
* データからデータを抽出するには、次の Experience Platform を使用することができます
   * データアクセス SDK
      * データは生のファイル形式です
      * プロファイルエクスペリエンスのイベントデータは、未統合の未統合の未処理の状態のままです。
   * RTCDP の宛先
      * プロファイル属性とセグメント メンバーシップは、取り出すことができます。

## 関連ドキュメント

* [Adobe Experience Platform インテリジェンス製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe Experience Platform クエリサービス](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja)

## 関連するブログ投稿

* [[!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence]](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [[!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)