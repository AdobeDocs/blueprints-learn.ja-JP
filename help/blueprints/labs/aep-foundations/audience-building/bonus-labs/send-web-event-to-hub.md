---
title: Web イベントをHubに送信
description: Postmanを使用してWeb イベントをHubに直接送信し、プロファイルに到達し、ストリーミングセグメントに適格であることを検証する方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: a8343499-b4d5-4540-8fe1-7497bc20e437
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# Web イベントをHubに送信

## Postmanを開く

コンピューターでpostmanを起動し、次のAPI呼び出しに移動します。

1. **Postman左サイドバー** —> `Collections`
1. **コレクション** —> `AEP Foundations Bootcamps (labs)`
1. **フォルダー** —> プロファイルラボ
1. **API リクエスト** —> `Create Web Event`

![PostmanでCreate Web Event API リクエストを開く](assets/send-web-event-to-hub-create-web-event-api-request.png)


## API リクエストを変更

サンプル API リクエストを作成するには、API リクエストの本文に次の部分を入力する必要があります。

まず、次の値を収集します。



## アカウントストリーミングエンドポイントの検索

1. 左側のパネルの&#x200B;**ソース**&#x200B;に移動し、上部のナビゲーションの&#x200B;**アカウント**&#x200B;をクリックします
1. **dep: HTTP API \[raw]**&#x200B;を検索し、行を強調表示して、**ストリーミングエンドポイント**&#x200B;の値を後で参照できる場所にコピーして保存します

 アカウントを作成し、そのストリーミングエンドポイントをコピーします&rbrack; （assets/send-order-event-to-hub-http-api-raw-streaming-endpoint.png &quot;dep: HTTP API \[raw]&quot;）

## Web データフローIDの検索

1. **HTTP API \[raw]** アカウントをクリックします
1. **dep: Web （stream）**&#x200B;というデータフロー行を検索して選択します
1. 右側のパネルのコピーで、**データフローID**&#x200B;値を後で参照できる場所に保存します

>[!NOTE]
>
>行の空のスペースをクリックします。  青いリンクをクリックしないでください。

![詳細：Web （ストリーム） データフロー](assets/send-web-event-to-hub-web-stream-dataflow-id.png "Web データフローID")のデータフローIDをコピーします

## 最終的なAPI リクエストの作成

前の手順で保存した値を、以下に強調表示されている場所にコピーします。

- **赤** —> `Streaming Endpoint URL`
- **緑** —> `Dataflow ID`

最終的なAPI リクエストは、次のようになります

>[!CAUTION]
>
>まだ実行しないでください。

![&#x200B; ストリーミングエンドポイントとデータフローIDが](assets/send-web-event-to-hub-final-web-api-request.png)に入力されたWeb イベント APIの作成リクエストを完了しました

## APIの実行

1. **保存** ボタンをクリックして、API呼び出しを保存します
1. **送信** ボタンをクリックして、リクエストを実行します

呼び出しが成功すると、次の応答が返されます…

![Web イベントを送信した後、API応答が成功しました](assets/send-web-event-to-hub-successful-api-response.png)

## 検証

1. プロファイルに移動し、プロファイルを検索して、イベントがプロファイルに取り込まれていることを確認します。  秒単位で表示されます。
   1. 電話でメールを使用してプロファイルを検索する
1. 最後にイベントで送信してから時間が長くなっても、新しいセグメントの対象にはならない場合があります。 それ以外の場合は、以下を参照できます。
   1. Any Event Edge（15分以内）
      1. 覚えておいてほしいのは、Edgeの評価で保存されたすべてのオーディエンスは、ストリーミングデータが入ってきたときにHubでも評価されるということです
   2. dep：任意のイベントストリーミング（時間内）
1. 新しいセグメントがない場合、Webhookに何も表示されない場合があります。
1. イベント転送は何も送信しません。
   1. なぜでしょうか？ このイベントはEdgeではなくハブに送信されたため、イベント転送の対象として表示されず、Assuranceにも表示されません。
1. 少なくとも30分後には、次のデータセットを確認することもできます。
   1. 下のテーブル名をサンドボックスのテーブル名に変更します。  見つけるには、データセット リストに移動し、「`dest`」でフィルターを実行し、データセットを開いて、右側のパネルにテーブル名をコピーします。

```sql
SELECT * FROM profile_export_for_destination_merge_policy_xxx
WHERE extSourceSystemAudit.LASTREFERENCEDDATE >= CURRENT_DATE
AND identitymap['email'][0].ID in ('depche.mode@dep.com')
ORDER BY extSourceSystemAudit.LASTREFERENCEDDATE DESC
LIMIT 10
```
