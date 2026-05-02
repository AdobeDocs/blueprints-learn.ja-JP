---
title: プロファイルエンリッチメントのためのカスタムデータサイエンスブループリント
description: データ サイエンスに基づくインサイトを [!DNL Experience Platform] に取り込んで、リアルタイム顧客プロファイルを強化する方法について説明します。
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 52%

---

# プロファイルエンリッチメントのブループリントのためのカスタムデータサイエンス

>[!TIP]
>このブループリントは、「オーディエンスの構築とアクティベーション」の下の[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/audience-building-activation/data-science-profile-enrichment.md)としても利用できます。

プロファイル エンリッチメント ブループリントのカスタム データ サイエンスでは、データを使用してモデルをトレーニング、デプロイ、スコアリングし、データ サイエンスおよび機械学習ツールから[!DNL Experience Platform]と[!DNL Real-Time Customer Data Platform]に関する機械学習インサイトを提供する方法を示します。

モデル化されたインサイトを[!DNL Experience Platform]に取り込んで、リアルタイムの顧客プロファイルを強化できます。 機械学習インサイトの例には、ライフタイム値、スコアリング、製品およびカテゴリの親和性、コンバージョン傾向、チャーン傾向が含まれます。

## ユースケース

* 顧客データからインサイトを抽出し、パターンを発見し、このデータからモデルをトレーニングしてスコアを付けます。
* より詳細なパーソナライズ機能と最適化されたジャーニーのために、[!UICONTROL リアルタイム顧客プロファイル]をモデル主導のインサイトおよび属性でエンリッチメントします。
* 顧客のライフタイムバリュー、コンバージョン傾向やチャーン傾向、製品およびコンテンツの親和性、エンゲージメントスコアなどの顧客インサイトを判別するためのモデルをトレーニングおよびスコアリングします。

## アーキテクチャ

<img src="assets/data_science.svg" alt="プロファイルエンリッチメントのためのカスタムデータサイエンスブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

## ガードレール

* データサイエンスの結果を[!DNL Experience Platform]に取り込む際のガードレールとエンドツーエンドの遅延について詳しくは、[&#x200B; デプロイメントガードレール ドキュメント &#x200B;](../experience-platform/guardrails.md)で参照されているデータ取り込みガードレールとレイテンシ図を参照してください。

## 関連ドキュメント

* [Adobe [!DNL Experience Platform] Intelligence製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe [!DNL Experience Platform]  クエリサービス](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja)

## 関連するブログ投稿

* [コンテンツとCommerceのAI：コンテンツインテリジェンスで顧客とのやり取りをパーソナライズ](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Adobeでの探索的データ分析の概要 [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [マシンラーニング（機械学習）を利用して、Adobe Adobeのエクスペリエンスを改善](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Segmentation.AI: Adobe [!DNL Experience Platform]のAutomated Audience-Clustering-as-a-Service](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
