---
title: サンドボックスアクセス
description: ラボを開始する前に、Postman環境が割り当てられたExperience Platform サンドボックスを正常に取得できることを確認します。
doc-type: article
solution: Experience Platform
exl-id: c841e497-a695-4d3f-85e6-d653478cad1e
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# サンドボックスアクセス

続行する前に、アクセスが正当なものであることを再確認してください。 次の手順を実行します。

1. 「`Check Sandbox Access`」というタイトルのフォルダーを開き、「`Retrieve Your Sandbox`」というタイトルの呼び出しをクリックします
1. Postmanの右上隅に環境ドロップダウンボックスが表示されます。  `AEP Bootcamp`環境を選択してください
1. `Send` ボタンをクリックして呼び出しを実行します

送信前にサンドボックス呼び出しを取得するための![Postman リクエストペイン &#x200B;](assets/sandbox-access-check-sandbox-request.png " サンドボックス API呼び出しを取得")



成功した応答は次のようになります。

割り当てられたサンドボックスの正常な取得を確認する![200 OK応答](assets/sandbox-access-successful-response.png "200 OK正常なサンドボックスリクエスト ")

>[!NOTE]
>
>**name**&#x200B;値は、postman環境のsandbox\_name変数と一致する必要があります

>[!TIP]
>
>おめでとうございます。  Experience Platform APIを使用する準備ができました
