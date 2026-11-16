---
title: 行をフィルタリング
description: 分割アクティビティを使用してオプトアウトした顧客行を除外し、ディメンションの変更を使用して、ワークフローのターゲットディメンションとSMS チャネル設定を整合させる方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: fb556a27-5c73-4457-ae98-dba43d445c7f
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 689f227965176096ccd1785699de65046af4f3d3
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%
---

# 行をフィルタリング

## 目標

次の一連の手順では、行レベルでオプトアウトしているため、SMS メッセージで実際にターゲットにできない行をすべて除外します。  これが行レベルのターゲットであるため、プロファイルの同意に依存することはできません。



## 分割アクティビティの設定

1. フォークアクティビティの下部のトランジションにある&#x200B;**+** アイコンをクリックし、ポップアップで「**分割**」アクティビティを選択します。

   ![下部のフォーク ブランチに分割アクティビティを追加](assets/filter-the-lines-add-split-activity.png)



2. 右側のパネルでラベルを更新し、次の内容を示します：`Filter out opt'd out lines`

   ![ オプトアウト行を除外するように設定されたアクティビティ ラベルを分割](assets/filter-the-lines-set-split-label.png)



3. 右側のパネルで、「**サブセット**」セクションを展開し、「**フィルターを作成**」ボタンをクリックします

   ![ サブセットセクションでフィルターボタンを作成](assets/filter-the-lines-create-filter-button.png)



4. SMS メッセージからオプトアウトされるすべての顧客行を削除する条件を追加し、**確認**&#x200B;をクリックします。

   ![SMSから顧客行を削除する条件](assets/filter-the-lines-sms-optin-condition.png)

   >[!NOTE]
   >
   >条件の作成方法を理解する必要がありますが、最終的な結果は上記のスクリーンショットと一致します。  分かったぞ！



5. 右上の「保存」ボタンをクリックして、作品を保存します。  あなたのキャンバスは今このように見えます\...

![分割アクティビティを保存した後のワークフローキャンバス ](assets/filter-the-lines-canvas-after-split-save.png)



## SMS アクティビティの追加

1. ワークフローキャンバスで、追加した分割条件の後にある&#x200B;**+** アイコンをクリックし、**モバイルメッセージ「Activity**」を選択します

   ![分割条件の後にモバイルメッセージアクティビティを追加](assets/filter-the-lines-add-sms-activity.png)

   ![SMS アクティビティがワークフローキャンバスに追加されました](assets/filter-the-lines-sms-activity-on-canvas.png)



2. 右側のパネルで「モバイルメッセージを編集」ボタンをクリックして、SMS メッセージの設定を開始します

   ![右側のパネルの「モバイルメッセージを編集」ボタン ](assets/filter-the-lines-edit-sms-button.png)



3. 上部のナビゲーションで「アクション」メニュー項目をクリックし、「モバイルメッセージ設定」ドロップダウンから、以前に作成したチャネルを選択します。

![SMS設定で、選択したチャネルが正常に表示されました](assets/filter-the-lines-sms-configuration-selected.png)




## まとめ

オプトアウトのためにSMS メッセージでターゲットにすることが許可されていない行をすべてフィルタリングし、ターゲットにすることが許可されたユーザーのSMS アクティビティを追加しました。
