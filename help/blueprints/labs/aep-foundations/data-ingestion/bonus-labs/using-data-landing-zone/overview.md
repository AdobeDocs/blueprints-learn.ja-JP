---
title: データランディングゾーンの活用
description: SAS URLを使用してAzure Storage Explorerをインストールし、Adobe Experience Platform Data Landing Zoneに接続するように設定します。
doc-type: overview-page
solution: Experience Platform
exl-id: d61bef25-7039-450d-a8e7-01bb12e8df7c
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%
---

# データランディングゾーンの活用

## 前提条件

Azure Storage Explorerをまだダウンロードしていない場合は、このラボの要件であるため、今すぐダウンロードしてください。  ダウンロードは以下のリンクからダウンロードできます。

[Azure Storage Explorerのダウンロード](https://azure.microsoft.com/en-us/blog/microsoft-azure-data-lake-storage-adls-in-storage-explorer-public-preview/)

1. アプリケーションのインストール
1. アプリケーションを初めて開いたときに、エンドユーザー使用許諾契約に同意します

Azure Storage Explorerの![&#x200B; エンドユーザーライセンス契約書画面](assets/overview-end-user-license-agreement-screen.png " エンドユーザーライセンス契約書画面")


## Experience PlatformでのAzure Storage Explorerの設定

1. Azure Storage Explorerを開き、**リソースを選択アイコン**&#x200B;をクリックし、**ADLS Gen2 Containerまたはdirectory**&#x200B;を選択します

   ![Azure Storage ExplorerのリソースとしてADLS Gen2 コンテナまたはディレクトリを選択しています](assets/overview-choose-the-resource-as-shown-above.png)



1. **共有アクセス署名URL （SAS）**&#x200B;を選択し、**次へ**&#x200B;をクリックします

   ![接続モードとしてSAS URL オプションを選択する](assets/overview-choose-the-sas-url-option-as-the-mode-of-connection.png "接続モードとしてSAS URL オプションを選択する")



1. 表示名を&#x200B;**データランディングゾーン**&#x200B;と入力します

   >[!NOTE]
   >
   >この手順を続行するには、SAS URLを指定する必要があります。  これは、次のステップで表示されるExperience Platformから取得できます。

   ![接続データランディングゾーンの命名](assets/overview-name-the-connection.png "接続の命名")



1. Adobe Experience Platformに移動し、次の操作を行ってデータランディングゾーンに移動します。

   - **ソース/カタログ**&#x200B;に移動します
   - ソースの下の&#x200B;**クラウドストレージ**&#x200B;を選択します
   - 次に、**データランディングゾーン** カードを探します
   - データランディングゾーンカードをクリックし、右側のパネルで「**資格情報を表示**」をクリックします

   ![Adobe Experience Platformの「資格情報を表示」オプションを使用したデータランディングゾーンのソースカード &#x200B;](assets/overview-data-landing-zone-view-credentials.png "Adobe Experience PlatformのデータランディングゾーンのSource カードへのアクセス ")



1. 表示されるモーダルから&#x200B;**SASUri**&#x200B;をコピーします。

   Azure Storage Explorerに戻り、前の手順で空白のままにした&#x200B;**SASUri値**&#x200B;を&#x200B;**Blob コンテナまたはディレクトリ SAS URL**&#x200B;に貼り付けます

   ![Experience PlatformからAzure Storage ExplorerへのSASUri値のコピー](assets/overview-copy-sas-uri-into-azure-storage-explorer.png "Adobe Experience PlatformからSAS URL資格情報をコピーし、Azure Storage Explorerにコピー")



1. **次へ**&#x200B;をクリックして続行します

   ![接続情報のSAS URL セクションにSAS URL資格情報をコピー](assets/overview-copy-sas-url-into-connection-info.png "接続情報のSAS URL セクションにSAS URL資格情報をコピー")



1. 概要画面で「**Connect**」をクリックします

![接続ボタン付きの概要画面](assets/overview-connect-screen.png "画面の接続")



次のような画面が表示されるはずです

![正常に接続されたData Landing Zone アカウントを示すAzure Storage Explorer](assets/overview-successfully-connected-account.png)

>[!SUCCESS]
>
>おめでとうございます。  Azure Storage Explorerが正常に設定されました
