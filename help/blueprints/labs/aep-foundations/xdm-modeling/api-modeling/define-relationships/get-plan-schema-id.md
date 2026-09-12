---
title: プラン スキーマ IDを取得
description: テナントスキーマレジストリ APIをクエリして、リレーションシップ記述子で使用するプラン検索スキーマの$idを検索して保存します。
doc-type: article
solution: Experience Platform
exl-id: f66e0483-b5b3-4493-b752-c4e00211a8bd
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# プラン スキーマ IDを取得

## すべてのテナントスキーマのリスト

1. `XDM Schema Lab -> Create Relationship Descriptors` フォルダーの`Step 1 - Get Lookup Schemas` API リクエストをクリックします
1. `Send` ボタンをクリックしてAPIを実行します

![手順1 - ルックアップスキーマ API リクエストを取得](assets/get-plan-schema-id-step-1-get-lookup-schemas.jpeg "手順1 - ルックアップスキーマを取得")

>[!NOTE]
>
>このGET呼び出しは、スキーマレジストリの「テナント」部分内に存在するすべてのスキーマ（カスタム作成されたスキーマなど）を取得します。 **プラン** スキーマを検索するだけで、顧客アカウントスキーマに関連付けることができます。



## プランスキーマの特定

1. 呼び出し応答で`dep: Plan [Lookup] ` スキーマを検索します
1. スキーマの`$id`をコピーし、後で参照できるように保存します

![Dep: プラン検索スキーマ $id （API応答に含まれる） &#x200B;](assets/get-plan-schema-id-dep-lookup-plan-schema-sid.png "dep: ルックアップ プラン スキーマ $id")

>[!NOTE]
>
>このスキーマは、既にサンドボックスにデプロイされている必要があります

>[!WARNING]
>
>スキーマの`$id`をどこかに保存するまで続行しないでください。  関係記述子を作成するには、後で必要になります
