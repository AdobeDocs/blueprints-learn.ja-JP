---
hold: true
title: データストリームの作成
description: Adobe Experience Platform、Offer Decisioning、およびJourney Optimizer サービスを使用してデータストリームを作成および設定し、Edge イベント処理を有効にする方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: 37873340-476a-4303-886d-de4835bba8df
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# データストリームの作成

## 学習目標

Edge イベント処理を有効にするために、必要なサービスを使用してデータストリームを作成および設定します。

データストリームは、それを利用するサービスを定義します。

- Edgeにデータを送信する場合、使用するデータストリームを指定します
- これらのデータストリームに送信されたデータは、設定されたサービスに従ってアクションを実行できます
  - Adobe Experience Platform

## 新しいデータストリームの作成

1. **データ収集**&#x200B;の下の左側のパネルで、**データストリーム**&#x200B;をクリックします
1. 次に、**新しいデータストリーム**&#x200B;をクリックして作成します

![新しいデータストリームボタンがハイライト表示されたデータストリームリスト &#x200B;](assets/create-datastream-new-datastream-button.png)

## データストリームの設定

次の情報を使用してデータストリームを設定します。

1. 名前 – > **データストリーム SB + \&lt; サンドボックス名> （データストリーム SB01）**
1. マッピングスキーマ -> **dep: Web**
1. この情報を取得する場合は、**位置情報とネットワーク検索**&#x200B;のすべてのオプションを&#x200B;**で**&#x200B;切り替えます。
1. 完了したら、**保存** ボタンをクリックします

>[!WARNING]
>
>「保存してマッピングを追加」をクリックしないでください。  誤って入力した場合は、キャンセルするだけです

![名前およびマッピングスキーマフィールドを含むデータストリーム設定フォーム &#x200B;](assets/create-datastream-configure-datastream-form.png " データストリームの設定")



データストリームを保存すると、次の画面が表示されます。

![新しいデータストリームを保存した後の確認画面](assets/create-datastream-created-confirmation.png " データストリームが最終画面を作成しました")

## Adobe Experience Platform サービスを追加

これにより、データをハブに送信し、このデータストリームで受信したデータのデータセットに格納できます。

1. 画面の中央にある青い&#x200B;**サービスを追加** ボタンをクリックします

![&#x200B; データストリーム設定画面の「サービスを追加」ボタン &#x200B;](assets/create-datastream-add-service-button.png)

&#x200B;2. 次の項目を設定します。
   - **サービス** -> `Adobe Experience Platform`
   - **イベントデータセット** -> `dep: Web`
   - **プロファイルデータセット** -> `dep: Customer Account`
   - **チェックボックスを選択** -> `Offer Decisioning`
   - **チェックボックスを選択** -> `Adobe Journey Optimizer`
&#x200B;3. 完了したら、**保存**&#x200B;をクリックします

![&#x200B; イベントおよびプロファイルデータセットフィールドを含むAdobe Experience Platform サービス設定ダイアログ &#x200B;](assets/create-datastream-configure-aep-service.png)

これで、データストリームにサービスが追加されました

![Adobe Experience Platform サービスがデータストリームに追加されました](assets/create-datastream-aep-service-added.png "Adobe Experience Platform サービスがデータストリームに追加されました")

**Copy**&#x200B;および&#x200B;**save** the **Datastream ID**&#x200B;をローカルコンピューターに保存します（後でPostmanで使用します）

後で使用するためにコピーして保存する![&#x200B; データストリーム ID フィールド &#x200B;](assets/create-datastream-copy-datastream-id.png)

## まとめ

Adobe Experience Platform サービスが設定された機能するデータストリームが必要です。
