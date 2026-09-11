---
hold: true
title: スキーマの表示
description: スキーマ UIとスキーマ取得APIの両方を使用して、顧客アカウントスキーマとプランスキーマとの検索関係を表示します。
doc-type: article
solution: Experience Platform
exl-id: dae48ef4-f762-4173-8564-c1ad40c0109b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# スキーマの表示

## UI経由で表示

1. ブラウザーを開き、`Schema -> Browse` セクションに戻ります。
1. スキーマ `Sample Customer Schema - <your sandbox number>`を検索
1. `dep: Plan [Lookup]`との関係が定義されていることに注意してください

詳細：プランの参照の関係を示すExperience Platform UIの![ サンプル顧客スキーマ ](assets/view-schema-relationship-to-plan-lookup-schema.png)


## API経由で表示

1. `Step 4 - Get Customer Account Schema and its descriptors` APIをクリックして選択

![ ステップ 4 – 顧客アカウントスキーマとその記述子の取得API呼び出し](assets/view-schema-step-4-get-schema-and-descriptors.png " ステップ 4 – 顧客アカウントスキーマとその記述子の取得")



2. リクエストのURLで、`<replace me>`を前のセクション [ スキーマの作成](../build-schema/create-schema.md)から保存した`$meta:altId`に置き換えます（下図を参照）

![ メタデータ :altIdをURL](assets/view-schema-final-step-4-request.png "最後のステップ 4 リクエスト ")に追加したステップ 4 リクエスト



3. `Save` ボタンを使用してリクエストを保存します

4. `Send` ボタンをクリックしてリクエストを実行します

これで`200 OK`応答が表示され、作成したスキーマの最後まで参照して、XDM JSON構造のレンズを通じてIDを確認できるようになります



顧客アカウントスキーマ JSON](assets/view-schema-relationship-descriptor.png "関係記述子")に表示される![関係記述子



![顧客アカウントスキーマ JSON](assets/view-schema-reference-identity-descriptor.png "参照ID記述子")に表示される参照ID記述子
