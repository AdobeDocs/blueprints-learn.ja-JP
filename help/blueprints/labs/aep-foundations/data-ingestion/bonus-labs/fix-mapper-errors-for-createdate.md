---
title: CreateDateのMAPPER エラーの修正
description: 不適切な形式のcreateDate値が空のフィールドに変換されたことが原因で発生するMAPPER エラーをトラブルシューティングして解決します。
doc-type: article
solution: Experience Platform
exl-id: e3f7ef23-6fd1-4f7a-8dc7-db82445322b0
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%
---

# CreateDateのMAPPER エラーの修正

この演習では、バッチ取り込みラボで見たMAPPER エラーを削除する方法を説明する必要があります。 createDateは必須フィールドではありませんが、誤ってフォーマットされた日付が空のフィールドに変換されるため、レコードは引き続き取り込まれるため、エラーを修正する必要があります。

![createDate値に無効な形式が含まれていると、MAPPER エラーが発生します](assets/fix-mapper-errors-for-createdate-invalid-format-mapper-error.png)
