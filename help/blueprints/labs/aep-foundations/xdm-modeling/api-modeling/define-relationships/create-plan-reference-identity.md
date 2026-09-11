---
title: プラン参照IDの作成
description: スキーマレジストリ APIを使用して、参照スキーマに参照ID記述子を作成し、バッチセグメント化で使用できるようにします。
doc-type: article
solution: Experience Platform
exl-id: b3b8f480-af3b-4bf8-b74e-3842f59691b6
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# プラン参照IDの作成

1. `XDM Schema Lab -> Create Relationship Descriptors` フォルダーの`Step 3 - Reference Descriptor for Plan` API リクエストをクリックします

   >[!CAUTION]
   >
   >リクエストを実行しないでください…まだ

   ![ ステップ 3 - プラン スキーマ API リクエストの参照記述子](assets/create-plan-reference-identity-step-3-descriptor-request.jpeg " ステップ 3 - プラン スキーマの参照記述子")



2. API呼び出しの本文で次のプロパティを更新します。

- `xdm:sourceSchema` プロパティの値を、[ スキーマの作成](../build-schema/create-schema.md) ステップから保存した`Customer Account` スキーマの`$id`に更新します
- `xdm:sourceProperty`の値を`Customer Account` スキーマの`planID` フィールドのパスに更新します

>[!NOTE]
>
>`dep: Lookup Plan` スキーマの`planId` フィールドのドット表記値を使用し、`.`を`/`に置き換えます
>
>先頭の`/`を忘れないでください（😄）

例のみ

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:identityNamespace": "planID"
}
```

>[!NOTE]
>
>上記のテナント名（\_devbc）を独自の名前で更新することを忘れないでください



3. `Save` ボタンを使用し続ける前に、リクエストを保存してください

4. `Send` ボタンをクリックしてAPIを実行します

次のような`201 Created`応答が表示されます

![201 Depを作成した後に応答を作成しました：プラン参照ID記述子](assets/create-plan-reference-identity-dep-plan-descriptor-result.png "dep: プラン参照ID記述子")

>[!NOTE]
>
>参照ID記述子は常にルックアップスキーマ（つまりsourceSchema）で定義されます

>[!NOTE]
>
>参照ID記述子は、スキーマ UIから関係を作成する際に、バックエンドで自動的に作成されます。 **APIを使用してスキーマを作成する場合にのみ、明示的に作成する必要があります**

>[!TIP]
>
>すごいですね！ `dep: Lookup Plan` スキーマを`Customer Account` スキーマに関連付けるために必要なすべての記述子を作成し、バッチセグメント化中に参照できるようにしました
