---
hold: true
title: APIによる自動化
description: スキーマ、フィールドグループ、IDおよびリレーションシップ記述子、データセットを1回のパスで自動的に作成するPostman コレクションを実行します。
doc-type: article
solution: Experience Platform
exl-id: a490f93f-19da-4de3-81c8-4569c49c5354
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# APIによる自動化

## 概要

APIを使用してデプロイメントを自動化する方法を確認するには、次のオブジェクトを作成するAPIのフォルダーを実行します。

- 顧客アカウントとプラン \[Lookup] スキーマ
- 上記のスキーマを構成するフィールドグループ
- プロファイルに必要なID記述子
- 顧客アカウントとプラン間の関係を作成するために必要な関係と参照記述子\[参照]
- 作成された各スキーマに一致する2つのデータセット



## フォルダーを実行

1. Postmanで、**XDM Schema Lab** フォルダー内の&#x200B;**Automation with API** フォルダーに移動します

![PostmanのXDM Schema Lab フォルダー内のAPI フォルダーを使用した自動化](assets/automate-with-apis-postman-automation-folder.png)



1. **Automation with API** フォルダーをクリックし、ワークスペースで「**実行**」ボタンをクリックします

>[!NOTE]
>
>「実行」ボタンは、Postman ワークスペースの右上にあります

![Automation with API フォルダーのPostman ワークスペースの右上にある「実行」ボタン &#x200B;](assets/automate-with-apis-click-folder-run-button.png " フォルダー「実行」をクリック ")



1. フォルダー内のすべてのAPI呼び出しを示す新しいウィンドウが表示されます。 **遅延**&#x200B;を&#x200B;**500ms**&#x200B;に設定し、**実行** ボタンをクリックします。

![実行](assets/automate-with-apis-execute-automation-dialog.png "自動化を実行")をクリックする前に、遅延が500 ミリ秒に設定された自動化を実行ダイアログ



1. API呼び出しが順番に実行され始め、完了すると32の合格したテストが表示されます。

![32件のテストに合格し、自動化を正常に実行しました](assets/automate-with-apis-successful-automation-32-passed-tests.png "自動化を成功しました")



1. Experience Platform UIに移動すると、**postman:**&#x200B;というプレフィックスを持つプロファイル用に2つのスキーマと2つのデータセットが作成され、有効になっている必要があります

![2つのスキーマが作成され、Postmanでプロファイルに対して有効になりました：接頭辞](assets/automate-with-apis-schemas-created-in-ui.png "自動化スキーマ ")



![Postmanで作成された2つのデータセット：自動スキーマに一致する接頭辞](assets/automate-with-apis-datasets-created-in-ui.png "自動化データセット ")

&#x200B;> [!TIP]
>
>おめでとうございます。  ID名前空間、フィールドグループ、スキーマ、ID/関係記述子のデプロイメントを自動化し、プロファイルのスキーマを有効にし、スキーマを使用してデータセットを生成するだけです
