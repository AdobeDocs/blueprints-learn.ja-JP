---
title: 新しいデータフローの作成
description: 既存のデータセットに対してバッチソースデータフローを作成し、以前のデータフローからマッピングをインポートして、セットアップを高速化します。
doc-type: article
solution: Experience Platform
exl-id: 6f26f742-27e8-445a-8005-21d4e59dc3d0
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%
---

# 新しいデータフローの作成

## ソースに移動

1. Adobe Experience Platform UIで、次の場所に移動します。\
   **ソース** -> **カタログ** -> **ローカルシステム**
1. 次に、**ローカルファイルアップロード** カードの「**データを追加**」ボタンをクリックします

![&#x200B; ソースカタログ内のローカルファイルアップロードカードの「データを追加」ボタン &#x200B;](assets/create-a-new-dataflow-local-file-upload-add-data.png " データランディングゾーンにアクセス ")



## データフローの設定

1. データフローの詳細画面で、**既存のデータセット**&#x200B;を選択します。
1. 以前に作成したデータセットを使用します。名前は&#x200B;**顧客アカウント - \&lt; イニシャル >**&#x200B;です
1. **プロファイルデータセット**&#x200B;の切り替えがオンになっていることを確認します。
（これをオンにしない場合、プロファイルストアはこのデータセットに入力される新しいデータを監視できず、このデータをプロファイルに取り込むことができません）
1. **部分取り込みを有効にする** トグルがオンになっていることを確認してください
（このオプションをオンにしない場合、レコードの1つにエラーがある場合、取り込み全体が失敗する可能性があります）
1. データフロー名を&#x200B;**Customer Account Batch v2 - \&lt;Your Initials>**&#x200B;に設定します
1. すべてのアラートを有効にする&#x200B;**ソースデータフローの開始/成功/失敗**
1. 問題がなければ、画面の右上隅にある「**次へ**」ボタンをクリックして、次の手順に進みます。

![2番目のデータフローの既存のデータセットで設定されたデータフローの詳細画面](assets/create-a-new-dataflow-existing-dataset-flow-details.png " データフローの詳細")



## サンプルファイルをアップロード

1. UIに&#x200B;**Lab\_Customer\_Account.csv** ファイルをドラッグ&amp;ドロップまたはアップロードします。  完了すると、画面は以下のようになります。

![2番目のデータフロー用にアップロードされた顧客アカウント CSV ファイルのプレビュー](assets/create-a-new-dataflow-uploaded-csv-preview.png "Adobe Experience Platform内のAzure Storage Explorer ファイルへのアクセス ")



## マッピングの読み込み

すべてのマッピングを再度設定する代わりに、マッピング画面で、以前に作成したマッピングを読み込むことができます。

1. 「**マッピングをインポート**」ボタンをクリックします
1. 以前に作成したマッピングを持つデータフローを選択します



![&#x200B; マッピング画面にマッピングボタンを読み込む](assets/create-a-new-dataflow-import-mapping-button.png " マッピングボタンを読み込む")



![&#x200B; マッピングをインポートするデータフローを選択するためのダイアログ &#x200B;](assets/create-a-new-dataflow-select-dataflow-to-import-mapping-from.png " マッピングをインポートするデータフローを選択")

>[!NOTE]
>
>マッピングのインポートは、他のデータフローからマッピングを再利用し、実行する必要があるマッピング作業を削減する便利な方法です
