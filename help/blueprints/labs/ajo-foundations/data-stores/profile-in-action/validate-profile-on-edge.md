---
title: Edgeでのプロファイルの検証
description: Edge プロファイルストアとオーディエンスメンバーシップ タブを確認して、Edge ネットワーク上のプロファイルのステータスを確認する方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: f82ceba7-6916-49ff-8776-2d0238560df8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%
---

# Edgeでのプロファイルの検証

## 学習目標

プロファイルがEdge network profile storeに存在しないことを確認します。

## Edge プロフィールを確認する

1. 「**属性**」タブと「**Edge**」ラジオボタンをクリックすると、Edge プロファイルが表示されます

   ![属性タブに表示されるEdge プロファイル ](assets/validate-profile-on-edge-attributes-tab.png)

   >[!NOTE]
   >
   >時間がどのくらい経過したかによって、IDのみで構成されるプロファイルの「ストリップダウン」バージョンが表示される可能性があります。



2. 「Audience Membership」タブをクリックします。  **blank**&#x200B;になります。

Edge プロファイルの「![空のオーディエンスメンバーシップ」タブ ](assets/validate-profile-on-edge-empty-audience-membership-tab.png)

>[!NOTE]
>
>**なぜEdge メンバーシップが存在しないのですか？**
>
>**dep: Event Edgeが（1時間以内に）**&#x200B;の条件を満たす必要はありませんか？
>
>「Edgeの評価基準を満たすオーディエンスがあるとしても、そのオーディエンスはEdgeには存在しません。そこに理由がないからです。
>
>そのオーディエンス（例：決定や宛先）を使用する場合、オーディエンスルールはEdgeにプッシュされ、次回イベントがEdgeにストリーミングされると、そのオーディエンスが評価されます。
>
>また、Edgeのセグメンテーションサービスもオンにしていませんでした。



## まとめ

プロファイルはEdgeに存在しません（まだ）
