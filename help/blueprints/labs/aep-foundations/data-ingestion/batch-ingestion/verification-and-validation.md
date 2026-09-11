---
hold: true
title: 検証と検証
description: UIで取り込んだデータセットをプレビューし、SQL クエリを実行して、バッチ取り込まれたレコードとネストされたスキーマフィールドを検証します。
doc-type: article
solution: Experience Platform
exl-id: 7e7cd43d-cc24-4a40-a175-2c651436ab79
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 検証と検証

## データセットのプレビュー

1. **データセット**&#x200B;をクリック
1. **作成したデータセット名を**&#x200B;検索して&#x200B;**クリック**&#x200B;します。

![ データセット ペインでデータセット名を検索してクリック ](assets/verification-and-validation-access-dataset-in-datasets-pane.png " データセット ペインでデータセットにアクセス ")



1. 右上隅の「**データセットをプレビュー**」をクリックします

![ データセット画面の右上隅にある「データセットをプレビュー」ボタンの場所](assets/verification-and-validation-preview-dataset-button-location.png " データセットをプレビューは右上隅にあります")



1. **スキーマ階層を示す左側のペインをクリックして、取り込んだレコードと同じレコードを**&#x200B;および&#x200B;**検証**&#x200B;します。

![取り込まれたレコードを示すスキーマ階層ペインを含むデータセットのプレビュー](assets/verification-and-validation-verify-and-validate-the-dataset.png)

>[!NOTE]
>
>**データセットのプレビュー**&#x200B;には、このデータセットで成功した最新のバッチが表示されます。 以前のバッチは表示されません。 また、配列やマップなどの複雑なデータは現在表示できず、空の列として表示されます。 慌てないでください！ より包括的なビューを取得するには、SQLを使用して、以下で説明するようにデータセットを探索する必要があります。



## クエリデータセット

1. プレビューを&#x200B;**閉じる**
1. データセット画面で、**テーブル名**&#x200B;のコピーアイコンをクリックします。 下の例の画面では、テーブル名は`customer_account_sm`です

![ データセット画面のテーブル名の横にあるコピーアイコン ](assets/verification-and-validation-copy-table-name.png " テーブル名をコピー")



1. **クエリ** セクションに移動します

1. 「**クエリを作成**」をクリック

![ クエリセクションの「クエリを作成」ボタン ](assets/verification-and-validation-access-the-query-editor.png)



1. 次のSQL クエリを&#x200B;**Editor**&#x200B;にコピー&amp;ペーストします。 `<table_name>`を手順6で取得した値に置き換えることを忘れないでください。

```sql
SELECT * FROM <table_name>
```



1. 「**再生**」ボタンを押します。

![SQL クエリと再生ボタンを備えたクエリエディターインターフェイス ](assets/verification-and-validation-query-editor-interface.png " クエリエディターインターフェイス ")



1. **結果をプレビュー**

1. また、次のSQL クエリを実行して、データとともにXDM スキーマを取得します。

```sql
SELECT to_json(shippingAddress) FROM <table_name>
```

`postalCode` **ノード**&#x200B;のデータにアクセスするには、次のように入力します。

```sql
SELECT shippingAddress.postalCode FROM <table_name>
```

>[!TIP]
>
>おめでとうございます。  Real-Time Customer Profilesのサンプルセットの取り込みと作成が完了しました
