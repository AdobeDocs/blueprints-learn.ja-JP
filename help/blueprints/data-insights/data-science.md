---
title: プロファイルエンリッチメントのためのカスタムデータサイエンスブループリント
description: データサイエンスベースのインサイトをに取り込んでリア  [!DNL Experience Platform]  タイム顧客プロファイルを強化する方法について説明します。
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 69%

---

# プロファイルエンリッチメントのブループリントのカスタムデータサイエンス

プロファイルエンリッチメントのカスタムデータサイエンスのブループリントでは、データを使用してモデルのトレーニング、デプロイ、スコアリングを行い、データサイエンスや機械学習ツールを使用した [!DNL Experience Platform] と [!DNL Real-Time Customer Data Platform] のデータに関する機械学習のインサイトを提供する方法を示しています。

モデル化されたインサイトを [!DNL Experience Platform] に取り込んで、リアルタイム顧客プロファイルを強化できます。 機械学習インサイトの例には、ライフタイム値、スコアリング、製品およびカテゴリの親和性、コンバージョン傾向、チャーン傾向が含まれます。

## ユースケース

* 顧客データからインサイトを抽出し、パターンを発見し、このデータからモデルをトレーニングしてスコアを付けます。
* より詳細なパーソナライズ機能と最適化されたジャーニーのために、[!UICONTROL リアルタイム顧客プロファイル]をモデル主導のインサイトおよび属性でエンリッチメントします。
* 顧客のライフタイムバリュー、コンバージョン傾向やチャーン傾向、製品およびコンテンツの親和性、エンゲージメントスコアなどの顧客インサイトを判別するためのモデルをトレーニングおよびスコアリングします。

## アーキテクチャ

<img src="assets/data_science.svg" alt="プロファイルエンリッチメントのためのカスタムデータサイエンスブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

## ガードレール

* データサイエンスの結果を [!DNL Experience Platform] およびリアルタイム顧客プロファイルに取り込む際のガードレールとエンドツーエンドの待ち時間について詳しくは、[ デプロイメントガードレールのドキュメント ](../experience-platform/deployment/guardrails.md) で参照されているデータ取り込みガードレールと待ち時間の図を参照してください。

## 実装手順

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?lang=ja&recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. [ データの [!DNL Experience Platform] への取り込み ](https://experienceleague.adobe.com/?lang=ja&recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)。

モデル結果をリアルタイム顧客プロファイルに取り込む場合は、データを取り込む前に、必ず次の操作をおこなってください。

1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに[正しい ID および ID 名前空間を設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。

## 実装に関する考慮事項

* ほとんどの場合、モデルの結果はエクスペリエンスイベントではなく、プロファイル属性として取り込む必要があります。モデルの結果は、単純な属性文字列にすることができます。取り込むモデル結果が複数ある場合は、配列またはマップタイプのフィールドを使用することをお勧めします。
* 統合プロファイル属性データの毎日の書き出しである日別プロファイルスナップショットデータセットを利用して、プロファイル属性データに関するモデルのトレーニングをおこなうことができます。プロファイルスナップショットデータセットのドキュメントに[ここから](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=ja#profile-attribute-datasets)アクセスすることができます。
* [!DNL Experience Platform] からデータを抽出するには、次の方法を使用できます
   * データアクセス SDK
      * データは生のファイル形式です
      * プロファイルエクスペリエンスのイベントデータは、未統合の未統合の未処理の状態のままです。
   * RTCDP の宛先
      * プロファイル属性とセグメント メンバーシップは、取り出すことができます。

## 関連ドキュメント

* [Adobe [!DNL Experience Platform]  インテリジェンス製品の説明 ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe [!DNL Experience Platform]  クエリサービス ](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja)

## 関連するブログ投稿

* [コンテンツ AI とコマース AI：コンテンツインテリジェンスを使用した顧客とのインタラクションのパーソナライズ](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Adobeに関する探索的データ分析の紹介  [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [アドビのエクスペリエンス製品をまたいだ機械学習によるユーザーエクスペリエンスの向上](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Segmentation.AI:Adobeでのサービスとしての自動オーディエンスクラスタリング  [!DNL Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)