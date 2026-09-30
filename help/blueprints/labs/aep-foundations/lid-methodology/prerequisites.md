---
title: 前提条件
description: データモデリングラボを開始する前に、LID手法のトレーニングシナリオ、学習目標、必要なワークシートを確認します。
doc-type: article
solution: Experience Platform
exl-id: ba582b0b-37a8-4cbb-ba1d-43594f3dd17b
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%
---

# 前提条件

## 概要

これから実施するLID方法論ラボでは、関係データモデルをExperience PlatformのNoSQL データモデルに変換する際の考え方について説明します。  データ翻訳の実行方法だけでなく、より重要なのは、なぜそれらを実行する必要があるのか、デザインの検証のために必要な質問は何かということです。

このビデオでは、関係データをリアルタイム顧客プロファイルのXDM モデルに変換するために使用されるラベル、識別および非正規化の3段階のLID手法について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3459078/?quality=12&learn=on)



## 学習目標

1. トレーニングシナリオの顧客アーキテクチャ、データソース、ビジネスユースケースの説明
1. エンティティ関係図（ERD）の関係と基数タイプの1対多、多対1および1対1をXDMに変換する方法について説明します
1. XDM スキーマに関連するリアルタイム顧客プロファイルの構成を説明します
1. LID手法のステップと、各ステップをリレーショナルデータベースモデルに効果的に適用する方法を特定します



## ラボアセット

### トレーニングシナリオ

ラボを開始する前に、トレーニングシナリオを理解しておきましょう。 このビデオでは、Connection 5Gのビジネス目標、現在のマーケティングアーキテクチャ、LID手法ラボ全体で使用されるターゲットAdobe Experience Platformアーキテクチャについて説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3459080/?quality=12&learn=on)



### 参考資料

LID方法論の中で様々なラボを実行するには、次の資料が必要です。

- ペンまたは鉛筆
- LID Lab Worksheets.pdfを印刷する機能（以下リンク）
- Connection 5G Training Scenario.pdfのコピーをダウンロード（以下にリンク）



ファイルをダウンロード — [接続5G トレーニング Scenario.pdf](assets/connection-5g-training-scenario.pdf)

ファイルをダウンロード — [LID Lab Worksheets.pdf](assets/lid-lab-worksheets.pdf)

>[!NOTE]
>
>次のラボを完了するには、ダウンロード後にLID Lab Worksheets.pdfを印刷する必要があります。
