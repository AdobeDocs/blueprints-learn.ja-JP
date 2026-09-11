---
title: データレイク上のイベントの検証
description: データレイクをクエリして、ストリーミングされたweb イベントが正しいデータセットに書き込まれていることを確認する方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: 14445089-aa3c-4cce-9d33-80032b6f9868
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# データレイク上のイベントの検証

## 学習目標

Web イベントがExperience Platform Data Lakeに書き込まれていることを確認します。

## イベントの検証

>[!NOTE]
>
>最終的に、データはデータレイクに表示されます。  **これには最大60分かかる場合があります**。  データセットがプロファイルに対して有効になっているので、イベントによってプロファイルフラグメントが作成されます。
>
>Web データセットを検索してクエリできます。

1. **クエリ**&#x200B;および&#x200B;**クエリの作成**&#x200B;に移動します

   ![ クエリセクションでクエリ画面を作成](assets/validate-event-on-data-lake-create-query.png)

2. このSQLをコピーしてクエリに貼り付けます

   ```sql
   SELECT identityMap['email'][0].id, * FROM dep_web
   where identityMap['email'][0].id = 'henry.creel@emailsim.io'
   ```

3. **実行** クエリ

>[!NOTE]
>
>**覚えておいてください**：最終的にデータはデータレイクに表示されます。  **これには最大60分かかる場合があります**。
>
>表示されるのを待つ必要はありません。 このステップに戻って、後で確認してください。



![ データレイク内のストリーミング web イベントを示すクエリ結果](assets/validate-event-on-data-lake-query-results.png)

## まとめ

イベントレコードが適切なデータセットに表示されます。
