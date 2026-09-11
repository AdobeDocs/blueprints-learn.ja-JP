---
hold: true
title: イベントの監視
description: Adobe Experience Platform Assuranceを使用してデバッグセッションを作成し、Postmanを介して検証済みイベントを送信し、エッジイベント処理ログを調べます。
doc-type: article
solution: Experience Platform
exl-id: 94b200c0-6714-4996-a266-119cc8f7f4e2
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---


# イベントの監視

## Assuranceに移動します

[Adobe Experience Platform Assurance](https://experienceleague.adobe.com/ja/docs/experience-platform/assurance/home)は、Adobe Experience Platform Edgeにデータを収集する方法の調査、検証、シミュレーション、検証を支援するAdobe Experience Cloudの製品です。

1. Adobe Experience Platform/Assurance/Create Sessionに移動します

![Adobe Experience Platform Assuranceに移動してセッションを作成](assets/monitor-your-event-navigate-to-assurance-create-session.png)



&#x200B;2. 「**開始**」ボタンをクリックします

![開始ボタンをクリックして、Assurance セッションの設定を開始します](assets/monitor-your-event-click-start-button.png)



## セッションの設定

1. 名前 – > \[Sandbox] Edge Session
1. URL —> https\://www\.adobe.com
   - このURLは、お客様の実際のサイトに置き換えられます
1. 「次へ」ボタンをクリックします

![&#x200B; セッション名とURLを入力したら、「次へ」をクリックします](assets/monitor-your-event-click-next-button.png)

&#x200B;4. 後で参照できる場所にリンクをコピー

&#x200B;5. 「**完了**」ボタンをクリックします

![Assurance セッション リンクをコピーして、「完了」をクリックします](assets/monitor-your-event-copy-link.png)



&#x200B;6. **設定**&#x200B;に移動します

![Assurance セッションの「設定」タブに移動します](assets/monitor-your-event-navigate-to-settings.png "設定をクリックします")



&#x200B;7. **+** ボタンをクリックして&#x200B;**イベントトランザクション**&#x200B;および&#x200B;**Edge Delivery**&#x200B;を有効にし、**完了**&#x200B;します

![&#x200B; イベントトランザクションとEdge Deliveryを有効にし、「完了」をクリックします](assets/monitor-your-event-enable-event-transactions-and-edge-delivery.png)


## Postmanを開く

Postman/Web イベントの作成/Edge（認証なし）/ヘッダーに移動します

1. 上記のAssuranceからコピーしたリンクを含む&#x200B;**x-adobe-aep-validation-token**&#x200B;をHeadersに追加します。 Assuranceからコピーしたリンクで、=の後のID **の値だけを**&#x200B;取得します。 e.g. [https://www.adobe.com/?adb\_validation\_sessionid=](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0) [`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0)
1. 完全なURLではなく、[`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0)値だけを使用します

![x-adobe-aep-validation-token ヘッダーをPostmanのAssurance セッション IDに追加](assets/monitor-your-event-populate-the-x-adobe-aep-validation-token.png)



&#x200B;3. Postmanで、**Web イベントの作成Edge （認証なし）** リクエストを保存して実行します



## Assurance ログの表示

Assuranceに戻ると、たくさんのイベントが表示されます。 検索にデータストリーム IDを配置して、関連するイベントタイプだけを絞り込むことができます

![&#x200B; データストリーム IDを検索してAssurance イベントをフィルタリング &#x200B;](assets/monitor-your-event-filter-using-search.png)



イベントを選択し、必要に応じて右側のパネルでメッセージを開きます。

![&#x200B; イベントを選択し、右側のパネルでメッセージを展開する](assets/monitor-your-event-expand-messages.png)

確認するイベントタイプ：

- hitReceived （Edgeが受信したペイロードを表示）
- evaluatingRule （SSFを設定した場合、評価されるルールが表示されます）
- firedDestinations （この宛先が送信された宛先）
- segmentsDiscovered （任意のエッジセグメントに適格でした）
- com.adobe.experience\_platform.edge\_segmentation/response （どのセグメントで応答したか）

![各イベントタイプを選択して、Assuranceがどのように解釈するかを確認します](assets/monitor-your-event-select-each-event.png)

Assuranceが各ステップをどのように解釈しているかを説明します。
