---
title: プライマリ IDの作成
description: スキーマレジストリ APIを使用して、顧客アカウントスキーマのプライマリ顧客ID ID ID記述子を作成します。
doc-type: article
solution: Experience Platform
exl-id: db690081-e857-4875-8bb9-7ac197d73cab
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# プライマリ IDの作成

1. `XDM Schema Lab -> Create Identity Descriptors` フォルダーの`Step 1 - Create Primary Identity for Customer Account Schema` API リクエストをクリックします

   ![手順1 – お客様のアカウント スキーマのプライマリ IDの作成Postman リクエスト ](assets/create-primary-identity-step-1-postman-request.jpeg "手順1 – お客様のアカウント スキーマのプライマリ IDの作成")

   >[!CAUTION]
   >
   >まだリクエストを実行しないでください



1. [ スキーマの作成](../build-schema/create-schema.md) ラボステップから保存した`$id`を使用して、リクエストの本文の`xdm:sourceSchema`値を更新します

1. リクエスト本文の`xdm:isPrimary`値を`true`に更新します

   例のみ

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/_devbc/customerID",
     "xdm:namespace": "customerID",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": true
   }
   ```

   >[!NOTE]
   >
   >上記のテナント名（\_devbc）を独自の名前で更新することを忘れないでください



1. `Save` ボタンを使用し続ける前に、リクエストを保存してください

1. `Send` ボタンをクリックしてAPIを実行します。 次のような`201 Created`応答が表示されます

![201 プライマリ ID記述子の作成後に応答を作成しました](assets/create-primary-identity-201-created-response.png " プライマリ ID記述子の作成に成功しました")

>[!TIP]
>
>おめでとうございます。  スキーマでプライマリ ID記述子を作成したばかりです
