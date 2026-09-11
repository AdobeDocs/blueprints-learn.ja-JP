---
hold: true
title: 初期マッピング
description: 計算フィールド式を使用して、エクスペリエンスイベントデータセットの必須_id フィールドとタイムスタンプフィールドを手動でマッピングします。
doc-type: article
solution: Experience Platform
exl-id: 4052d104-bf0c-4b2d-a298-8075279aeaf8
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# 初期マッピング

前の演習と同様に、マッピングを検証し、場合によっては変更する必要があります。

## マシンラーニングのレコメンデーションの検証

1. マッピングステップでは、マシンラーニングレコメンデーションはほとんどの属性を自動的にマッピングします。 しかし、いくつかのエラーもあります。 最初の画面は以下のようになります。

![&#x200B; マッピング画面に表示される_idとタイムスタンプは、マッピングされていないフィールドとしてML](assets/initial-mappings-id-timestamp-unmapped-fields.png "_idで推奨されていません。タイムスタンプは、ML Recommenderが")のマッピングを生成しない2つのフィールドです

>[!NOTE]
>
>Experience Event データセットを初めてマッピングするので、**\_id**&#x200B;と&#x200B;**timestamp**&#x200B;はExperience Eventsにデフォルトで推奨またはマッピングされないことに注意してください。 手動でこれらを正しくマッピングする必要があります。

## Map \_id, timestamp and order.\_devbc.acqSource fields

1. **\_id、**&#x200B;をマッピングするには、次の計算フィールド式を記述し、「プレビュー」をクリックします

```none
concat(orderID, "-", lastOrderStatusUpdate)
```

![&#x200B; マッピング _idの計算フィールド、保存の準備](assets/initial-mappings-calculated-field-for-id-mapping.png " マッピング _idの計算フィールドは、これに似ています。 「保存」をクリックして、計算フィールドを保存します")

![計算フィールドを_id属性にマッピング &#x200B;](assets/initial-mappings-map-calculated-field-to-id.png "計算フィールドを_id")にマッピング

1. ターゲットスキーマの&#x200B;**timestamp** フィールドが、次の計算フィールドにマッピングされていることを確認します。

```none
lastOrderStatusUpdate
```

![&#x200B; タイムスタンプマッピングのフィールド式のプレビューを計算](assets/initial-mappings-expression-preview.png "次の式を書き込み、「プレビュー」をクリックします。 この値は大文字と小文字が区別され、正確に次のように記述する必要があります。")

![計算フィールド式「inStore」を注文にマッピングしています。_devbc.acqSource](assets/initial-mappings-map-instore-expression-to-acqsource.png)

1. 計算フィールド式&#x200B;**&quot;inStore&quot;**&#x200B;を&#x200B;**の順序にマッピングします。\_devbc.acqSource**

![店舗内の計算フィールド式を書き込み、「プレビュー」をクリック &#x200B;](assets/initial-mappings-write-instore-expression-preview.png "次の式を書き込み、「プレビュー」をクリックします。 この値は大文字と小文字が区別され、正確に次のように記述する必要があります。")

## 重複マッピングの処理

マッピング画面で問題が発生した場合は、**orderStatus**&#x200B;が&#x200B;**order.\_devbc.acqSource,**&#x200B;にマッピングされているなどの重複したマッピングがあります。「 – 」アイコンをクリックしてマッピングを削除します。

&#x200B;> [!NOTE]
>
>複数の入力フィールドを同じ出力フィールドにマッピングすることはできないので、マッピングが曖昧になります。 しかし、1つの入力フィールドをXDM スキーマの複数の出力フィールドにマッピングすることは可能です。

![order.devbc.acqSourceにマッピングされたorderStatusのマッピング警告の重複](assets/initial-mappings-duplicate-mapping-warning.png "order.devbc.acqSourceにマッピングされたorderStatusのマッピングの重複")



![計算フィールドを作成した後のorder._devbc.acqSourceのマッピング警告の重複](assets/initial-mappings-duplicate-mapping-for-acqsource.png "計算フィールドを作成し、既にマッピングしたので、order._devbc.acqSourceのマッピングの重複。")
