---
hold: true
title: プロファイルクラスを取得
description: グローバルスキーマレジストリ APIを呼び出して、カスタムスキーマで使用するXDM Individual Profile クラスの$idを取得して保存します。
doc-type: article
solution: Experience Platform
exl-id: d87c21a2-dad4-4666-b917-cdf8e16058d4
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# プロファイルクラスを取得

## 手順3 - プロファイルクラスの取得

1. `XDM API Lab -> Create Schema` フォルダーの`Step 3 - Get Profile Class` リクエストをクリックします
1. `Send` ボタンをクリックして実行

![手順3 - プロファイルクラス API リクエストを取得](assets/get-profile-class-step-3-api-request.jpeg "手順3 - プロファイルクラス API リクエストを取得")

>[!NOTE]
>
>GET リクエストで、`global` パス : .../schemaregistry/**global**/classesに注意してください。 `global`を使用すると、Adobe標準XDM オブジェクトのみを返すことをスキーマレジストリに伝えることを忘れないでください


## クラス $idを見つけて保存します

API リクエストを実行した後、次の手順を実行して、XDM Individual Profile クラスの`$id`を見つけて保存します。

1. 応答で`XDM Individual Profile` クラスを検索します
1. `XDM Individual Profile` クラスの`$id`をコピーし、後で参照できる場所に保存します。

![API応答にあるXDM個人プロファイルクラス &#x200B;](assets/get-profile-class-xdm-individual-profile-class.png "XDM個人プロファイルクラス ")

>[!WARNING]
>
>`$id`をどこかに保存するまで続行しないでください。  顧客アカウントスキーマを作成するには、後で必要になります
