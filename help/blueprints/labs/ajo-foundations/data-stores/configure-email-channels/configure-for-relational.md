---
hold: true
title: リレーショナル用に設定
description: Orchestrated Campaignsのみのリレーショナルスキーマのemail属性を使用して、メールチャネルを設定する方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: 6f299942-79a6-42c2-8a5b-dd4bccd6aad4
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 10%

---


# リレーショナル用に設定

## 目標

次の一連の手順では、リレーショナルスキーマ `dep-rel: Customer Account`の`email`属性を使用して、オーケストレーションされたキャンペーンでのみ使用するためのメールチャネル設定を作成します

## チャネル設定の作成

1. メニュー&#x200B;**チャネルの管理と一般設定**&#x200B;の下にある&#x200B;**チャネル設定**→→移動します
2. 「**設定を作成**」ボタンをクリックします

![&#x200B; チャネル設定の作成](assets/configure-for-profile-create-configuration-button.png)

&#x200B;3. 作成ウィザードで、次の値を設定します。
   - **名前：** `Relational-Email`
   - **チャネル：** `Email`
   - **マーケティングアクション：** `Email Targeting`

![&#x200B; チャネル設定の詳細](assets/configure-for-relational-channel-configuration-name-values.png)

>[!NOTE]
>
>チャネルとして「電子メール」を選択すると、新しいセクション「メール設定」が表示されます。





## メールの種類を設定

**メールの種類**&#x200B;を&#x200B;**マーケティング**&#x200B;に設定

![&#x200B; メール設定](assets/configure-for-profile-set-email-type-marketing.png)

## サブドメインの設定

**サブドメイン** ドロップダウンから、**email.dep-labs.com**&#x200B;を選択します

![email.dep-labs.comを選択したサブドメインドロップダウン &#x200B;](assets/configure-for-profile-select-email-subdomain.png " サブドメインの設定")

## IP プールの詳細の設定

**IP プール** ドロップダウンから、**マーケティング**&#x200B;を選択します

![&#x200B; マーケティングが選択されたIP プールのドロップダウン &#x200B;](assets/configure-for-profile-select-marketing-ip-pool.png "IP プールの詳細の設定")

## リストの登録解除の設定

1. リストの購読解除に対して&#x200B;**有効**&#x200B;であることを確認してください
1. リストの購読解除の環境設定領域で、すべてのチェックボックスが&#x200B;**オンになっていることを確認します**
1. リンク管理で、**Adobe managed**&#x200B;が選択されていることを確認します
1. 同意レベルの場合、これが&#x200B;**チャネル**&#x200B;に設定されていることを確認してください

![&#x200B; リストの登録解除の設定](assets/configure-for-profile-configure-list-unsubscribe-settings.png)

## ヘッダーパラメーターの設定

1. 次のフィールドを次のように設定します。
   - **送信者名：** `DEP Labs`
   - **電子メールのプレフィックスから：** `dep`
   - **名前に返信：** `DEP Labs Support`
   - **メールへの返信：** `reply@email.dep-labs.com`
   - **エラー電子メールのプレフィックス：** `error`

![&#x200B; ヘッダーパラメーター](assets/configure-for-profile-email-header-parameters.png)

## BCC メールの設定

空白のままにする

>[!NOTE]
>
>BCC インボックスに送信することで、送信済みメールのコピーを保持できます。 送信されたすべてのメールがこの BCC アドレスにブラインドコピーされるように、目的のメールアドレスを入力します。 BCC アドレスのドメインは、アドビにデリゲートされたサブドメインとは異なる必要があります。 この機能はオプションです。 *メールにBCCを使用する方法*

## メール再試行パラメーターの設定

デフォルト設定の&#x200B;**時間**&#x200B;を&#x200B;**84**&#x200B;に設定したままにします

## URL トラッキングパラメーターの設定

デフォルト設定のままにする

## 実行の詳細

1. 「オーケストレーションされたキャンペーン」タブで、「**有効にする」チェックボックスを** オンにします。

![&#x200B; オーケストレーションされたキャンペーンの設定](assets/configure-for-profile-enable-orchestrated-campaign-tab.png)

&#x200B;2. 実行ディメンションで、次の設定を行います。
   - **次の1つにつき1つのメッセージを配信します：** `Target Dimension `
   - **Profile Target Dimension:** `dep-rel: Customer Account - customer_id`

![実行ディメンション &#x200B;](assets/configure-for-relational-execution-dimension-target-settings.png)

&#x200B;3. 「実行アドレス」で、次の設定を行います。
   - **Source:** `Target Dimension`
   - **配信アドレス：** `click on the Edit button`

![Target Dimension](assets/configure-for-relational-execution-address-source-target-dimension.png)

&#x200B;4. ポップアップで、**dep-rel: Customer Account** フォルダーをクリックします

![配信アドレスの設定](assets/configure-for-relational-customer-account-folder.png)

&#x200B;5. **メール**&#x200B;を選択し、**選択** ボタンをクリックします

![電子メールを配信先住所](assets/configure-for-relational-select-email-as-delivery-address.png)

&#x200B;6. 完了すると、最終的な実行の詳細は以下のスクリーンショットのようになります

![実行ディメンションが設定されました](assets/configure-for-relational-execution-details-final-result.png)

>[!NOTE]
>
>オーケストレーションされたキャンペーンの場合は、メールで顧客アカウントをターゲティングするので、Target Dimensionごとに1つのメッセージを送信するだけで済みます。  使用する実行アドレスは、Target Dimension自体から取得されます（例：**dep-rel: Customer Account** テーブルに保存されている&#x200B;**email** アドレス）。


## レビューして保存

1. すべての詳細を再度確認して、一致することを確認します。
1. 上にスクロールして、**送信**&#x200B;をクリックします。
1. 完了すると、2つのメールチャネル設定が表示されます。両方とも「処理中」状態である可能性があります。

>[!WARNING]
>
>メールチャネル設定の処理には、最大2時間かかることが確認されています。

## まとめ

これで、オーケストレーションされたキャンペーンにリレーショナルスキーマ属性を使用するメールチャネル設定の作成方法を確認しました。
