---
title: 失敗したデータフローの再試行
description: 失敗したデータフローの実行を再試行して、ソースデータを新しいデータフロー内の更新されたマッピングルールに対して再処理します。
doc-type: article
solution: Experience Platform
exl-id: 83ecf037-e524-4887-b833-5ed96af40419
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%
---

# 失敗したデータフローの再試行

ワークフローを再試行するには、次の操作を行います。

1. **ソース / データフロー/ \[ データフローの名前] -> \[実行に失敗しました]**&#x200B;に移動します
1. 右側のパネルを表示できなかったデータフロー実行をハイライト表示します。
1. **再試行**&#x200B;をクリックします。 再試行は、失敗した実行に関連付けられたデータのコピーを取得し、新しいマッピングルールを適用します

![右側のパネルから失敗したデータフロー実行を再試行しています](assets/retry-a-failed-dataflow.png)

>[!NOTE]
>
>失敗したデータフローを再試行すると、新しいデータフローが作成され、実行されます。 データフローのリストの上部に表示されます
