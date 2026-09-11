---
title: SMS チャネルの設定
description: Twilio ベースのSMS チャネルとその実行ディメンションを、オーケストレーションされたキャンペーンで使用するように設定する方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: 63c994f2-4b6b-42e9-aa82-cb6697390a08
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# SMS チャネルの設定

## 目標

次の一連の手順では、SMS チャネルを設定します。 これは、施策を構築する際に、後で個々のラインホルダーにメッセージを送信するために必要です。



## チャネルへの移動

1. Adobe Journey Optimizerで、**管理** -> **チャネル** メニューに移動します。
1. **SMS設定** → **API資格情報**&#x200B;を選択します。
1. 「**API資格情報を作成**」をクリックします。

![管理チャネルメニューのSMS設定とAPI資格情報に移動します。「SMS設定に移動」 ](assets/configure-sms-channel-navigate-to-sms-settings.png "SMS設定に移動")



## SMS API資格情報の定義

まず、AJOがアウトバウンド SMS リクエストの送信に使用するAPI コネクタを作成します。

1. 「SMS ベンダー」で「**Twilio**」を選択します。
1. 独自の[Twilio体験版アカウント ](https://www.twilio.com/try-twilio)を使用して、次のAPI資格情報の詳細を入力します。
   - **名前：** `DEP SMS`
   - **アカウント SID:**&#x200B;がTwilio Console ダッシュボードに見つかりました
   - **認証トークン：**&#x200B;がTwilio Console ダッシュボードに見つかりました（**表示**&#x200B;をクリックすると表示されます）
1. **送信**&#x200B;をクリックして、API資格情報を登録します

>[!NOTE]
>
>この手順を開始する前に、確認済みの電話番号を持つ無料のTwilio体験版アカウントが必要です。 [twilio.com/try-twilio](https://www.twilio.com/try-twilio)にサインアップし、Twilio Console ダッシュボードでアカウント SIDと認証トークンを見つけます。

Twilio ベンダー](assets/configure-sms-channel-enter-api-credentials.png)の![SMS API資格情報フィールド



## SMS チャネル設定の作成

次に、このAPI資格情報を、ジャーニーとキャンペーンが使用できるチャネル設定にマッピングします。

1. **チャネル** → **一般設定** → **チャネル設定**&#x200B;に移動します。

   ![一般設定](assets/configure-sms-channel-navigate-channel-configurations.png)でチャネル設定に移動します



2. 「**チャネル設定を作成**」をクリックします。

   ![ チャネル設定の作成ボタン ](assets/configure-sms-channel-click-create-configuration.png)



3. SMS チャネル設定設定を次の値で入力します。
   - **名前：** `Relational-SMS-Multi-Entity`
   - **チャネル：** `Mobile Message`
   - **マーケティングアクション：** `SMS Targeting`

>[!NOTE]
>
>ユーザーに権限がないことを示すエラーが発生した場合は、無視して続行します。

## SMS設定

「チャネル」を「モバイルメッセージ」として選択すると、「SMS設定」という新しいセクションが表示されます。 次の詳細を入力します。

- **モバイルメッセージの種類：** `Marketing`
- **モバイルメッセージ設定：** `DEP SMS`
- **送信者番号：** `01234567890`
- **サブドメイン：** `leave blank`
- **オプトアウト番号：** `leave blank`

送信者番号とモバイルメッセージタイプを含む![SMS設定](assets/configure-sms-channel-sms-settings-fields.png)



## 実行の詳細

1. 「実行の詳細」で、「**オーケストレーションされたキャンペーン**」タブをクリックします

   ![実行の詳細](assets/configure-sms-channel-execution-details-tab.png)の下の「キャンペーンを調整」タブ



2. 「**有効**」チェックボックスがオンになっていることを確認します

   ![ オーケストレーションされたキャンペーンに対して有効なチェックボックスがオンになりました](assets/configure-sms-channel-enabled-checkbox.png)



3. 次に、**実行ディメンション**&#x200B;のサブセクションの下で、次のように設定されていることを確認します。
   - **次のメッセージを配信：** `Target + Secondary Dimension`
   - **Profile Target Dimension:** `dep-rel: Customer Account - customer_id`
   - **Dimension:** `Customer Line`

   ![ ターゲットディメンションとセカンダリディメンションを使用した実行ディメンション設定](assets/configure-sms-channel-execution-dimension-setup.png)

   ![Dimensionは、実行分析コード設定「セカンダリDimension」 ](assets/configure-sms-channel-secondary-dimension-detail.png "セカンダリDimension")で顧客行に設定されています

   >[!NOTE]
   >
   >これは、メッセージを送信する際に、Profile Target Dimensionに一致するメッセージをレコードごとに1つ配信する必要があることをOrchestrated Campaignsに伝えています。



4. 「実行アドレス」見出しで、**Dimension**&#x200B;のラジオボタンを選択し、**SMS実行フィールド**&#x200B;の「編集」ボタンをクリックします

   ![実行アドレスが編集フィールドを持つDimensionに設定されています](assets/configure-sms-channel-execution-address-selection.png)



5. ポップアップで、スキーマ **dep-rel: Customer Line**&#x200B;をクリックし、**Mobile Phone**&#x200B;を選択します。

   営業担当者の![ スキーマポップアップ：顧客行スキーマ ](assets/configure-sms-channel-customer-line-schema-popup.png)

   dep-relから![携帯電話フィールドが選択されました：Customer Line スキーマ &quot;携帯電話フィールド&quot;](assets/configure-sms-channel-mobile-phone-field-selected.png "携帯電話フィールド ")



6. 最後の「実行の詳細」セクションが次のように一致することを確認します

![必要な設定に一致する最終実行の詳細設定](assets/configure-sms-channel-final-execution-details.png)



## 送信してレビュー

1. **送信** ボタンをクリックして設定を完了すると、成功メッセージが表示されます

   チャネル設定を送信した後の![成功メッセージ ](assets/configure-sms-channel-submit-success-message.png)



2. チャネル設定インベントリ ページで、次に進む前にステータスが&#x200B;**アクティブ**&#x200B;として表示されていることを確認します

   ![ チャネル設定ステータスがアクティブとして表示されます](assets/configure-sms-channel-active-status.png)

   >[!CAUTION]
   >
   >ステータスが&#x200B;**Active**&#x200B;になるまで待ちます。そうしないと、将来のラボステップが失敗します



3. ステータスが「アクティブ」になると、完了です。

>[!TIP]
>
>🚀 ブーヤ！ SMS チャネルがライブになり、アクションの準備が整いました。



## まとめ

これで、SMS チャネルを正常に設定する方法を確認しました。  これはAPI ベースのSMSであるため、プロバイダーによっては、認証に別の方法を使用する場合があります。

ご興味のある方は、[こちら](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)をご覧ください。
