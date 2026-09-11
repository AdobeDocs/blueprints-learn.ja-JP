---
hold: true
title: プロパティを作成
description: 受信エクスペリエンスイベントをWebhook エンドポイントに転送するデータ要素とルールを使用して、イベント転送プロパティを作成します。
doc-type: article
solution: Experience Platform
exl-id: eabd5f75-7706-4c96-982e-2512509bdc55
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 0%

---


# プロパティを作成

通常、エクスペリエンスイベントをサードパーティに転送します（必須ではありません）。 これは通常、特定の状況で第三者に通知するためにイベントのコピーがリアルタイムで必要な場合に使用されます（例：購入についてGoogle、Meta、TikTokに通知する）。

>[!NOTE]
>
>リマインダー：プロパティには、何をどこに送るかを決定するために必要なすべての拡張機能、データ要素、およびルールが含まれています

1. 左側のパネルで「イベント転送」をクリックします
2. 「New Property」をクリックして

![新しいプロパティボタンが強調表示されたイベント転送セクション ](assets/create-property-new-property-button.png "新しいイベント転送プロパティを作成")

3. 次の数式を使用してプロパティ名を更新します：`Event Forward Property SB + [sandbox number]`。 最終名称は次のようになります。**イベント転送プロパティ SB01**

4. 完了したら、**保存**&#x200B;をクリックします

![保存ボタンがハイライト表示されたイベント転送プロパティ名フィールドが入力されました](assets/create-property-name-property-form.png)

## 拡張機能をインストール

1. 作成したイベント転送プロパティをクリックします

![新しく作成されたプロパティがハイライト表示されたイベント転送プロパティのリスト ](assets/create-property-open-new-property.png " イベントプロパティを開く")



2. 以下のような画面が表示されます。  **拡張機能**&#x200B;をクリックします。

「拡張機能」タブが強調表示された![ イベント転送プロパティの概要画面](assets/create-property-click-extensions-tab.png)



3. 次の手順を実行して、拡張機能Adobe Cloud Connectorをインストールします。

4. 上部ナビゲーションの&#x200B;**カタログ**&#x200B;をクリックします
5. **Adobe Cloud Connector** カードをクリックします
6. 右側のパネルで「**Install**」ボタンをクリックします

![Adobe Cloud Connector カードとインストールボタンがハイライト表示された拡張機能カタログ ](assets/create-property-install-cloud-connector-extension.png)



インストールをクリックすると、次に示すように、プロパティの「インストール済み」拡張機能の下に拡張機能が表示されます

![Adobe Cloud Connector拡張機能が正常にインストールされたことを示すインストール済み拡張機能リスト ](assets/create-property-extension-installed-confirmation.png "完全にインストールされた拡張機能")

## データ要素を作成

>[!NOTE]
>
>データ要素は、受信イベントを参照し、必要に応じて複数の個々のコンポーネントに解析できます

1. 左側のパネルで、**データ要素**&#x200B;をクリックします



![ データ要素のリンクがハイライト表示された左パネルのナビゲーション ](assets/create-property-navigate-to-data-elements.png " データ要素に移動")



2. 「**新しいデータ要素を作成**」ボタンをクリックします

![新しいデータ要素を作成ボタンが強調表示されたデータ要素ページ ](assets/create-property-create-new-data-element-button.png "新しいデータ要素を作成")



3. 次の情報を使用して、新しいデータ要素を設定します。

| 要素タイプ | 設定する値 |
| ----------------- | ------------------ |
| 名前 | データオブジェクト |
| 拡張機能 | コア |
| データ要素タイプ | カスタムコード |

![ データ要素の設定（名前、拡張機能、データ要素タイプのフィールドが設定されている） ](assets/create-property-data-element-config-step-1.png " データ要素の設定")



4. ボタン **エディターを開く**&#x200B;をクリックして、次のカスタムコードを追加します。

![ カスタムコード用に「エディターを開く」ボタンがハイライト表示されたデータ要素の設定](assets/create-property-open-custom-code-editor.png " エディターを開く")



5. このようにカスタムコードをエディターに追加し、保存します

```none
var xdm = arc?.event || '';
return xdm;
```

![受信XDM イベントオブジェクトを返すスクリプトを表示するカスタムコードエディター](assets/create-property-custom-code-added.png " カスタムコード ")

>[!NOTE]
>
>これにより、ペイロードに翻訳を行うことなく、xdm オブジェクト全体を取得します。  必要であれば、XDM オブジェクト内の個々の要素（ページ名、購入額など）を、フィールドごとに1つのデータ要素に解析できます。  これを行う理由は、構造が別の構造に変換された場合です





6. 「**保存**」ボタンをクリックして、データ要素を保存します。

![保存ボタンがハイライト表示されたデータ要素エディター](assets/create-property-save-data-element-button.png)



完了すると、データ要素が追加されたことを確認する次の画面が表示されます。

![新しく保存されたデータ要素がプロパティに追加されたことを示すデータ要素リスト ](assets/create-property-data-element-saved-confirmation.png)


## ルールの作成

>[!NOTE]
>
>ルールには次のものが含まれます。
>
>1. 今後の措置に関する条件
>2. ペイロードを変換し、送信先を定義するアクション



1. 左側のパネルで「**ルール**」をクリックします

![ ルール リンクがハイライト表示された左側のレール ナビゲーション ](assets/create-property-navigate-to-rules.png)



2. 次に、**新しいルールの作成**&#x200B;をクリックします

![新しいルールを作成ボタンが強調表示されたルールページ ](assets/create-property-new-rule-button.png)



3. 次の数式を使用してルール名を更新します：`"EF Rule SB" + [your sandbox number]` （EF ルール SB01）。 次に示すように、ブラウザーウィンドウの右上にサンドボックス番号が表示されます。

![ ブラウザーウィンドウの右上隅に、ルール名](assets/create-property-sandbox-number-location.png)で使用されているサンドボックス番号が表示されています

4. 完了したら、**保存**&#x200B;をクリックします

>[!NOTE]
>
>ルール名が`"EF Rule SB" + [sandbox number]`の数式パターンに従っていることを確認してください

![EF ルール サンドボックスの名前付けパターンで入力されたルール名フィールド ](assets/create-property-add-rule-name.png " ルールに名前を追加")



5. 「+」記号をクリックしてルールにアクションを追加し、新しいアクションを追加します

![新しいアクションを追加するためにプラスアイコンがハイライト表示されたルールエディター](assets/create-property-add-action-button.png " アクションを追加")

## Webhook URLを取得（実際に使用）

>[!NOTE]
>
>このラボでは、ここでWebhookを使用して、データが送信先に到着したかどうかを確認できます。 現実世界のシナリオでは、代わりにその宛先にログインし、そのツールを使用して何が届いたかを確認します。



1. ブラウザーの新しいタブで次のリンクを開きます – > [https://webhook.site](https://webhook.site/)
2. 表示された一意のURLをコピーし、安全な場所に保存します

コピー用に一意のURLがハイライト表示された![Webhook.site ページ ](assets/create-property-webhooksite-copy-url.png)



3. 次の情報を使用してアクションを設定します。

| 設定 | 値 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 拡張機能 | Adobe Cloud Connector |
| アクションタイプ | 呼び出しの取得 |
| メソッド | 投稿 |
| URL | ストリーミング宛先の設定に使用したのと同じWebhook URLを使用します。 ブラウザーで新しいタブを開き、「宛先」/「参照」に移動すると、見つけることができます |
| 本文 | Raw |
| Body Data | \{ &quot;data&quot;: \{ &quot;event&quot;: &quot;\{\{Data Object\}}&quot; } } |

>[!NOTE]
>
>ここで参照されている\{{Data Object\}\}は、前に作成したデータ要素です。 ここで、下流システムの要件は、イベントオブジェクトをデータオブジェクトにラップすることでした。 ここにフォーマットを入力してください。
>
>\{\{Data Object\}\}を複数のフィールド（ページ名、購入など）に分割した場合、各フィールドを目的の場所に配置するJSON構造を変換して、宛先の一致をより詳細に制御できます。





完了したら、画面を下の画面と同じように検証し、**変更を保持**&#x200B;をクリックします

![Adobe Cloud Connectorで設定されたルールアクションの取得呼び出し設定とWebhook URLの設定](assets/create-property-configure-action-settings.png " アクションの設定")



4. 完了すると、アクションがルールに追加されます。 **保存**&#x200B;をクリックして続行します。

![保存ボタンが強調表示された設定されたアクションを表示するルールエディター](assets/create-property-save-rule-button.png " ルールを保存")

>[!WARNING]
>
>エクスペリエンスイベントを送信する場合、プロファイルではなく、その属性（Edge オーディエンスであっても）も含めて、イベントを送信します。
>
>これは、スピードアップの目的で行われます。



## 変更を公開

1. 左側のパネルで「**公開フロー**」をクリックします

![公開フローのリンクがハイライト表示された左パネルのナビゲーション ](assets/create-property-navigate-to-publishing-flow.png "公開フローに移動")



2. 「**ライブラリを追加**」ボタンをクリック

ライブラリを追加ボタンがハイライト表示された![公開フローページ ](assets/create-property-add-library-button.png " ライブラリを追加")



3. 次の情報を使用してライブラリを設定します。

- 名前 – > **EF ライブラリ**
- 環境 – > **開発**
- **変更されたすべてのリソースを追加**&#x200B;をクリックします


完了すると、画面は以下のスクリーンショットと同じように表示されます。  すべてが正常に見える場合は、「**開発に保存してビルド**」ボタンをクリックします

![名前、開発環境、および「開発に保存してビルド」ボタンを使用したライブラリ設定](assets/create-property-configure-library-save-and-build.png)



4. すると、開発ビルドが緑色になり、使用する準備ができたことが示されます

![開発ビルドのステータスが緑色になり、使用できる状態になったことを示す公開フロー](assets/create-property-development-build-ready.png)
