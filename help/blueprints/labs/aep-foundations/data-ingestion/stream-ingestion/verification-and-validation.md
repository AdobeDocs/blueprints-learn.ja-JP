---
title: 検証と検証
description: UIでストリーミングデータセットをプレビューし、SQL クエリを実行して、取り込んだレコードとネストされたスキーマフィールドを検証します。
doc-type: article
solution: Experience Platform
exl-id: fbdb0b6b-08b6-49b8-b6ab-d59d5941c678
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%
---

# 検証と検証

## データセットのプレビュー

1. **データセット**&#x200B;をクリック
1. **作成したデータセット名を**&#x200B;検索して&#x200B;**クリック**&#x200B;します。

   ![&#x200B; データセット ペインで作成されたデータセットにアクセス &#x200B;](assets/verification-and-validation-access-the-dataset-in-the-datasets-pane.png " データセット ペインでデータセットにアクセス ")



1. 右上隅の「**データセットをプレビュー**」をクリックします

   ![&#x200B; データセット画面の右上隅にある「データセットをプレビュー」ボタン &#x200B;](assets/verification-and-validation-preview-dataset-button.png " データセットをプレビューは右上隅にあります")



1. **スキーマ階層を示す左側のペインをクリックして、取り込んだレコードと同じレコードを**&#x200B;および&#x200B;**検証**&#x200B;します。

![&#x200B; スキーマ階層ペインを使用した取り込みレコードの検証と検証](assets/verification-and-validation-verify-and-validate-the-dataset.png " データセットの検証と検証")

>[!NOTE]
>
>**データセットのプレビュー**&#x200B;には、データセットの最初の数行のみが表示されます。 配列オブジェクトは表示できません。



## クエリデータセット

1. プレビューを&#x200B;**閉じる**
1. データセット画面で、**テーブル名**&#x200B;のコピーアイコンをクリックします。 下の例の画面では、テーブル名は`customer_account_sm`です

   ![&#x200B; クエリで使用するためにデータセット画面からテーブル名をコピーする](assets/verification-and-validation-copy-the-table-name.png " テーブル名をコピーする")



1. **クエリ** セクションに移動します

1. 「**クエリを作成**」をクリック

   ![&#x200B; クエリセクションからクエリエディターにアクセス &#x200B;](assets/verification-and-validation-access-the-query-editor.png " クエリエディターにアクセス ")



1. **拡張クエリエディター**&#x200B;を有効にする切替スイッチ

   拡張クエリエディター切り替えが有効になっている![&#x200B; クエリエディターインターフェイス &#x200B;](assets/verification-and-validation-enhanced-query-editor-toggle.png " クエリエディターインターフェイス ")



1. 次のSQL クエリをコピーして、**Editor**&#x200B;に貼り付けます。 `<table_name>`を手順2で取得した値に置き換えることを忘れないでください。

   ```sql
   SELECT * FROM <table_name>
   ```



1. 「**再生**」ボタンを押します。

1. **結果をプレビュー**&#x200B;します。

1. また、次のSQL クエリを実行して、データとともにXDM スキーマを取得します。

   ```sql
   SELECT to_json(shippingAddress) FROM <table_name>
   ```



1. `postalCode` **ノード**&#x200B;のデータにアクセスするには、次のように入力します。

```sql
SELECT shippingAddress.postalCode FROM <table_name>
```

>[!SUCCESS]
>
>おめでとうございます。  Real-Time Customer Profilesのサンプルセットの取り込みと作成が完了しました
