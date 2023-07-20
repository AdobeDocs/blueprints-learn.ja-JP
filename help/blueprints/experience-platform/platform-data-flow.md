---
title: Adobe Experience Platform データフローアーキテクチャ図
description: このアーキテクチャ図に、データがどのように Adobe Experience Platform に入り、出て行くのかを示します。
solution: Data Collection
kt: 7198
thumbnail: null
exl-id: 5016f657-dd55-4ab7-859d-c97bc5edff76
source-git-commit: 70e7bfb3a6d7bad858bd72b6329602bdfb822505
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 100%

---

# Adobe Experience Platform データフローアーキテクチャ図

## データフロー図

次の図に、Adobe Experience Platform のデータの取り込みおよび送り出しの様々なパスを示します。

<img src="assets/aep_data_flow.svg" alt="Experience Platform データフロー" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## データの入出力パターン

すべてのデータ取り込み、収集、取り込みの各パターンの詳細なリストについては、[データ準備と取り込みのブループリント](../data-ingestion/ingestion.md)を参照してください。

データの送り出しとアクセスパターンのすべての詳細なリストについては、[データアクセスと書き出しのブループリント](../data-ingestion/egress.md)を参照してください。

## データ取り込みガードレール

以下の図に、Adobe Experience Platform にデータを取り込む際の平均パフォーマンスのガードレールと待ち時間を示します。

<img src="deployment/assets/aep_data_flow_guardrails.svg" alt="Experience Platform データフロー" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" class="modal-image" />