---
title: 標準フィールドグループを取得
description: グローバルスキーマレジストリ APIをクエリして、顧客プロファイルスキーマの構築に必要な標準XDM フィールドグループの$idを検索して保存します。
doc-type: article
solution: Experience Platform
exl-id: 62017ece-eef2-4785-afed-5c690c00ed02
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# 標準フィールドグループを取得

>[!NOTE]
>
>**「フィールドグループ」**&#x200B;は、以前は&#x200B;**「Mixin」**&#x200B;と呼ばれていたため、これらの用語は、API リクエストとガイド全体で同じ意味で使用される場合があります。



## XDM標準フィールドグループのリクエスト

1. `XDM Schema Lab -> Create Schema` フォルダーの`Step 1 - Get XDM Standard Field Groups` API呼び出しをクリックします
1. `Send` ボタンをクリックして呼び出しを実行します



**リクエスト**

![&#x200B; ステップ 1 - XDM標準フィールドグループ API リクエストを取得](assets/get-standard-field-groups-step-1-request.jpeg " ステップ 1 - リクエスト ")

>[!NOTE]
>
>以下のリクエスト URLで`global`値を使用することに注意してください。
>
>https\://platform.adobe.io/data/foundation/schemaregistry/**global**/mixins
>
>`global`は、XDM標準コンポーネント（この場合はフィールドグループ/mixin）のみをリクエストするために使用されます。 Experience Platform XDM レジストリには、Adobeとテナント（カスタム）の2種類の所有者があります。
>
>- Adobeが作成したオブジェクトは、XDMのリストまたはルックアップリクエストで常に`global`という単語を使用します
>- テナントが作成したオブジェクト（カスタム）は、XDMのリストまたはルックアップ呼び出しで常に`tenant`という単語を使用します



**応答**

![XDM標準フィールドグループを一覧表示するAPI応答](assets/get-standard-field-groups-step-1-response.png "手順1応答")


## 必要なXDM標準フィールドグループの特定

スキーマは、常に1つ以上のフィールドグループとクラスで構成されます。  Connection 5G Individual Profile スキーマの場合、スキーマに必要な標準XDM フィールドグループを見つけます。

- デモグラフィック情報
- 個人の連絡先詳細
- 同意と環境設定の詳細



1. 呼び出しの応答で`Demographic Details` フィールドグループを検索します
1. フィールドグループの`$id`をコピーし、後で参照できるように保存します
1. 上記の他の2つのフィールドグループについて、手順1と2を繰り返します

![API応答にあるデモグラフィックの詳細フィールドグループ &#x200B;](assets/get-standard-field-groups-demographic-details-field-group.png)

>[!WARNING]
>
>3つすべて（3） `$ids`をどこかに保存するまで続行しないでください。  顧客アカウントスキーマを作成するには、後で必要になります
