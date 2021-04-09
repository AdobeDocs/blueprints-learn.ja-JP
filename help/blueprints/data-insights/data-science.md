---
title: プロファイルエンリッチメント設計図のカスタムデータサイエンス
description: この青写真は、Adobe Experience PlatformのData Science WorkspaceがExperience Platform内のデータをどのように使用して、モデルをトレーニング、導入、スコア化し、データから機械学習のインサイトを得るかを示しています。
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
translation-type: tm+mt
source-git-commit: 2343151a1ed5374c299fb9317f6282c232d5d23b
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# プロファイルエンリッチメント設計図のカスタムデータサイエンス

Custom Data Science forプロファイルエンリッチメントBlueprintは、Adobe Experience Platformのデータを[!UICONTROL Data Science Workspace]でどのように使用して、機械学習の洞察を提供するモデルのトレーニング、展開、スコアリングを行えるかを説明しています。 これらのモデルは、[!UICONTROL リアルタイム顧客プロファイル]に対して有効なデータセットに直接出力し、顧客プロファイルをさらに強化できます。 これらのインサイトは、パーソナライゼーションのためにアクションを付けることができます。 機械学習インサイトの例としては、ライフタイム値スコア、製品とカテゴリのアフィニティ、コンバージョンする傾向、傾向から傾向などがあります。

## 使用例

* Experience Platform内の顧客データからインサイトと発見のパターンを抽出します。 このデータからモデルをトレーニングし、スコアを作成します。
* より詳細なパーソナライゼーションと最適化されたジャーニーを実現するため、[!UICONTROL リアルタイム顧客プロファイル]を、モデルに基づくインサイトと属性で強化します。
* モデルをトレーニングおよびスコアして、顧客のライフタイム値、コンバージョンや傾向、商品やコンテンツのアフィニティ、エンゲージメントスコアなどの顧客インサイトを判断します。

## 建築

<img src="assets/datascience.svg" alt="プロファイルエンリッチメント設計図のカスタムデータサイエンスのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## 導入手順

1. スキーマとデータセットを作成します。
1. データをExperience Platformに取り込みます。
1. DSWノートブックを作成します。
1. 言語を選択します。 PythonとPySparkがサポートされています。
1. ノートブックに作成者モデル
1. モデルをトレーニングします。
1. モデルにスコアを付け、ターゲットデータを使用した予測を生成します。
1. モデル結果を[!UICONTROL リアルタイム顧客プロファイル]にプッシュする場合は、プロファイル用にモデル結果データセットを有効にします。

## 関連ドキュメント

* [Adobe Experience Platformインテリジェンス製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL Data Science ] Workspaceのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [[!UICONTROL Data Science ] Workspaceのチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## 関連するブログ投稿

* [[!DNL Simplifying the Data Science Lifecycle with Adobe Platform Experience]](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [[!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence]](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [[!DNL Gaining a Deeper Understanding of Churn Using Data Science Workspace]](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [[!DNL Understanding Data Science In Adobe Experience Platform]](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [[!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [[!DNL Reimagining Jupyter Notebooks for Enterprise Scale]](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [[!DNL Accelerate Intelligent Insights with Adobe Experience Platform Data Science Workspace]](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [[!DNL A Preview of Time Series Forecasting with Adobe Experience Platform]](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
