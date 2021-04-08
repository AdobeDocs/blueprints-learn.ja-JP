---
title: プロファイルエンリッチメント設計図のカスタムデータサイエンス
description: この青写真は、Adobe Experience PlatformのData Science WorkspaceがExperience Platform内のデータをどのように使用して、モデルをトレーニング、導入、スコア化し、データから機械学習のインサイトを得るかを示しています。
solution: Experience Platform,Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
translation-type: tm+mt
source-git-commit: e9e8473f62fa222e483f7aeed33148433f1ec427
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# プロファイルエンリッチメント設計図のカスタムデータサイエンス

Custom Data Science for Data Science forプロファイルエンリッチメントBlueprintは、Adobe Experience PlatformのデータをData Science Workspaceで使用して、機械学習の洞察を提供するモデルのトレーニング、展開、スコアリングを行う方法を説明しています。 これらのモデルは、リアルタイム顧客プロファイルが有効なデータセットに直接出力し、顧客プロファイルをさらに強化できます。 これらのインサイトは、パーソナライゼーションのためにアクションを付けることができます。 機械学習インサイトの例としては、ライフタイム値スコア、製品とカテゴリのアフィニティ、コンバージョンする傾向、傾向から傾向などがあります。

## 使用例

* Experience Platform内の顧客データからインサイトと発見のパターンを抽出します。 このデータからモデルをトレーニングし、スコアを作成します。
* より詳細なパーソナライゼーションと最適化されたジャーニーを実現するために、リアルタイム顧客プロファイルをモデルに基づくインサイトと属性で強化します。
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
1. モデル結果をリアルタイム顧客プロファイルにプッシュする場合は、プロファイルのためのモデル結果データセットを有効にします。

## 関連ドキュメント

* [Adobe Experience Platformインテリジェンス製品の説明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Data Science Workspaceドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [Data Science Workspaceのチュートリアル](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## 関連するブログ投稿

* [Adobeプラットフォームの使用経験を活用したデータ科学ライフサイクルの簡素化](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [コンテンツとコマースAI:コンテンツインテリジェンスを通して顧客との対話をパーソナライズ](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Data Science Workspaceを使用したchurnについての理解の深め](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [Adobe Experience Platformのデータ科学について](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [Adobe Experience Platformの探索的データ分析の前置き](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [機械学習によるAdobe Experience製品の横断的な高度なユーザーエクスペリエンスの実現](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Adobe Experience Platformでデータ科学のXDMデータを大規模にモデリングする](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [Segmentation.AI:Adobe Experience Platformのオーディエンス・クラスタリングをサービスとして自動化](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [企業規模向けのジャピター・ノートブックの再イメージ](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [Adobe Experience Platform・データ・サイエンス・ワークスペースでインテリジェントなインサイトを加速](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [Adobe Experience Platformとの時系列予測のプレビュー](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [機械学習によるAdobe Experience製品の横断的な高度なユーザーエクスペリエンスの実現](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
