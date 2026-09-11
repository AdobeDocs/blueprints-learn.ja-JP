---
title: カスタムフィールドグループの作成
description: スキーマレジストリ APIを使用して、カスタム顧客アカウントの詳細フィールドグループを作成し、後のスキーマで使用するために$idを保存します。
doc-type: article
solution: Experience Platform
exl-id: d3262db9-7c0b-476a-843f-1a2c224ee792
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# カスタムフィールドグループの作成

## フィールドグループ構造

フィールドグループは、常に次のフィールドで構成されます。 これは次のステップのリクエストに表示されます。

| 必須の値 | 説明 |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| title | スキーマレジストリ内で作成するフィールドグループの名前。 名前は一意である必要があります。 |
| description | フィールドグループの目的についての簡単な説明 |
| タイプ | 常にオブジェクト |
| meta\:intendedToExtend | フィールドグループで使用できるクラスを定義します。 クラスは常に`$id`値で参照されます |
| allOf | フィールドグループに含めることができるリソースについて説明します。 カスタム定義フィールドの場合、パスは常に`#/definitions/customFields`です |
| definitions.customFields... | これは、カスタムフィールドグループの作成に必要なデフォルトのJSON スキーマ構造です。 上の`allOf`と一致する必要があります |
| \&lt;TENANT\_NAME> | テナント名（一意の名前）は、プロビジョニングプロセス中に作成されます。 これにより、行われたカスタマイズが、既存または将来のAdobe スキーマレジストリの変更と競合しないようにします |



## 「顧客アカウント詳細を作成」フィールドグループ

1. `XDM Schema Lab -> Create Schema` フォルダーのリクエスト `Step 2 - Create Customer Account Details Field Group` API呼び出しをクリックします



![ ステップ 2 – 顧客アカウント詳細フィールド グループ API リクエストの作成](assets/create-custom-field-groups-step-2-field-group-request.png " ステップ 2 – 顧客アカウント詳細フィールド グループの作成")



実行する前に、リクエストの本文を確認します。 フィールドグループの構造セクションで説明されている必須フィールドは、次のように表示されます。

![ リクエスト本文](assets/create-custom-field-groups-field-group-structure.png " フィールドグループ構造")に示すように、カスタムフィールドグループの必須フィールド



![ カスタムフィールド定義パスを参照するallOf プロパティ ](assets/create-custom-field-groups-field-group-structure-allof.png " フィールドグループ構造allOf")

>[!NOTE]
>
>`allOf`の上の右側の画像で「/definitions/customFields」のパスを参照する方法に注意してください。  これは、XDM システムにカスタム作成オブジェクトの場所を伝えるために、スキーマで定義された構造（左側の画像）と一致する必要があります。
>
>![allOf パスがカスタムフィールド定義パスと一致する必要があることを示す比較](assets/create-custom-field-groups-allof-path-highlighted.png)



また、マッピングシートの各特定のフィールドがXDM JSON構造内でどのように実証されるかにも注目してください。



![ シート計画ドット表記法をXDM JSON構造に変換](assets/create-custom-field-groups-plan-dot-notation-to-xdm-json.png "計画ドット表記法をXDM JSONに変換")



![ シートのアカウントと顧客IDのドット表記をXDMに変換](assets/create-custom-field-groups-account-customer-id-dot-notation-to-xdm.png " アカウントと顧客IDのドット表記をXDM")に変換



2. 次の形式を使用して、フィールドグループの`title`と`description`を更新します：`Customer Account Details - Sandbox <your number here>`



   ![ カスタムフィールドグループに入力されたタイトルと説明の例](assets/create-custom-field-groups-field-group-title-description-example.png " フィールドグループのタイトルと説明の例")



3. 「`Send`」ボタンをクリックして実行します。  以下のスクリーンショットのような応答が表示されるはずです。

4. 新しく作成した顧客アカウントの詳細フィールドグループの`$id`値をコピーします。

![ カスタムフィールドグループを作成した後のAPI応答が成功しました](assets/create-custom-field-groups-step-2-create-custom-field-group-success.png "手順2 - カスタムフィールドグループの成功の作成")

>[!WARNING]
>
>`$id`をどこかに保存するまで続行しないでください。  顧客アカウントスキーマを作成するには、後で必要になります
>
>
