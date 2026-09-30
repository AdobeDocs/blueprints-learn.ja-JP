---
title: 他のIDを作成
description: スキーマレジストリ APIを使用して、顧客アカウントスキーマ用の非プライマリメールアドレス ID記述子を作成します。
doc-type: article
solution: Experience Platform
exl-id: 22c40299-fb93-4d41-a23b-f8629df3e7b9
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%
---

# 他のIDを作成

1. `XDM Schema Lab -> Create Identity Descriptors` フォルダーの`Step 2 - Create Email Address Identity for Customer Account Schema` API呼び出しをクリックします

   >[!CAUTION]
   >
   >リクエストを実行しないでください…まだ

   ![ ステップ 2 - Customer Account Schema Postman リクエストの電子メールアドレス IDの作成](assets/create-other-identities-step-2-postman-request.jpeg " ステップ 2 – 電子メールアドレス ID記述子の作成")



1. [ スキーマの作成](../build-schema/create-schema.md) ラボステップから保存した`$id`を使用して、リクエストの本文の`xdm:sourceSchema`値を更新します

1. リクエスト本文の`xdm:isPrimary`値を`false`に更新します

   例のみ

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/personalEmail/address",
     "xdm:namespace": "Email",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": false
   }
   ```

   >[!NOTE]
   >
   >上記のテナント名（\_devbc）を独自の名前で更新することを忘れないでください



1. `Save` ボタンを使用し続ける前に、リクエストを保存してください

1. `Send` ボタンをクリックしてAPIを実行します。 次のような`201 Created`応答が表示されます

![201電子メールアドレス ID記述子の作成に成功した後に応答を作成しました](assets/create-other-identities-201-created-response.png "電子メールアドレスのID記述子が正常に作成されました")
