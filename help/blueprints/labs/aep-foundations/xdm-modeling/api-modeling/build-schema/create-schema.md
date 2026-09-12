---
title: スキーマの作成
description: スキーマレジストリ APIを使用して、プロファイルクラスと標準およびカスタムフィールドグループ参照から顧客スキーマを組み立てます。
doc-type: article
solution: Experience Platform
exl-id: 78ebc5b8-d088-48e9-857f-87085a87a280
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# スキーマの作成

## APIの本文を変更する

>[!CAUTION]
>
>**呼び出しを実行しません…まだ**

1. `XDM Schema Lab -> Create Schema` フォルダーの`Step 4 - Create Customer Account Schema` API呼び出しをクリックします。

   ![手順4 - Postman コレクションでCustomer Account Schema API呼び出しを作成する](assets/create-schema-click-on-the-step-4-create-customer-account-schema.png)



2. 呼び出しの本文を開き、スキーマの定義方法の構造を表示します。 スキーマは、常に1つの（1）クラスと1つ以上のフィールドグループのみで構成されます。

3. スキーマの本文の`title`および`description` フィールドに次の情報を入力します。

   - タイトル -> `Sample Customer Schema - <your sandbox number>`
   - 説明 – > `Sample Customer Schema - <your sandbox number>`

4. 完了した以前のラボセクションから保存した`$ids`を`$ref` フィールドに入力します。[&#x200B; カスタムフィールドグループの作成](./create-custom-field-groups.md)と[&#x200B; プロファイルクラスの取得](./get-profile-class.md)。 次の項目ごとに$idを設定する必要があります。

   - クラス -> XDM個人プロファイル
   - フィールドグループ -> デモグラフィックの詳細
   - フィールドグループ/個人の連絡先の詳細
   - フィールドグループ/同意と環境設定の詳細
   - フィールドグループ（カスタム）/顧客アカウントの詳細

   クラスおよびフィールドグループ参照を追加する前に![空のスキーマリクエスト本文](assets/create-schema-empty-schema-api-body.png "空のスキーマ API本文")



5. 最終的な本文を確認し、このようになっていることを確認します

![&#x200B; タイトル、説明、およびすべての$ref値が入力されたスキーマリクエスト本文を完了しました](assets/create-schema-example-of-final-body-payload.png "最終本文ペイロードの例")

>[!NOTE]
>
>`$refs`の順序は問題ではなく、本体内の`title`と`description`の位置も問題ではありません。



## APIの実行

1. 続行する前に、API リクエストに変更を保存します。
1. `Send` ボタンをクリックしてAPIを実行します

スキーマを作成するための応答が成功すると、`201 Created` ステータスになり、次の画像のようになります

>[!WARNING]
>
>成功した場合は、リクエストを再実行しないでください

![201 ステップ 4 APIを介してスキーマを正常に作成した後に応答を作成しました](assets/create-schema-sample-response-from-executing-the-step-4-api.png " ステップ 4 APIの実行による応答のサンプル ")


## スキーマ $idを見つけて保存します

1. API リクエストを実行したら、応答から`$id`と`$meta:altId`をコピーします
1. 値をどこかに保存して、後で再利用できるようにします

>[!WARNING]
>
>`$id`と`$meta:altId`をどこかに保存するまで続行しないでください。  これらは今後のラボステップで必要になります

>[!TIP]
>
>**おめでとうございます！ API**&#x200B;のみを使用してスキーマを作成しました
