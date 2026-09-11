---
title: メールアクティビティの追加
description: オーケストレーションされたキャンペーンで異なるメールチャネル設定を使用して、別々のフォーク分岐で2つのメールアクティビティを追加および設定する方法について説明します。
doc-type: article
solution: Experience Platform
exl-id: e911a251-9f9f-484c-a2de-101b0fc2c417
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# メールアクティビティの追加

## 目標

次の一連の手順では、キャンペーンを構築して、2つのメールアクティビティを2つのフォークアクティビティブランチに追加します。 先ほど作成したメールチャネルを使用するように、2つのメールアクティビティを設定します。 最後に、これらの各メールアクティビティに基本的なメール設定（件名と本文）を追加します。

>[!CAUTION]
>
>続行する前に、両方のメールチャネル設定がステータスでアクティブであることを確認する必要があります。
>
>![ アクティブなステータスを表示する両方のメールチャネル設定](assets/add-email-activities-email-channel-configs-active.png " メールチャネル設定")



## 最上位ブランチのメールアクティビティを追加

1. 上位フローの&#x200B;**+**&#x200B;をクリックし、**チャネルアクティビティ**&#x200B;から&#x200B;**電子メール**&#x200B;を選択します

   ![電子メールアクティビティを追加](assets/add-email-activities-select-email-activity.png)

   **電子メール**&#x200B;の詳細ペインが開きます

   ![ メールの詳細ペイン ](assets/add-email-activities-email-details-pane.png)

2. **Email** アクティビティのプロファイル属性&#x200B;**を使用してラベルの名前を** Emailに変更し、**メールを編集**&#x200B;をクリックします。 メール本文の作成は、テスト目的でのみ行われます

   ![電子メールアクティビティラベルの名前を変更して、「電子メールを編集」をクリック ](assets/add-email-activities-rename-and-edit-email.png)

3. 「**アクション**」タブを選択し、ドロップダウンから「**プロファイル – メール**」チャネル設定を選択します

   ![ アクション タブでプロファイルと電子メール チャネルの設定を選択](assets/add-email-activities-select-profile-email-channel.png)

4. 次に、**コンテンツを編集**&#x200B;をクリックして、テストコンテンツを追加します

   ![ 「コンテンツを編集」をクリックしてテストコンテンツを追加](assets/add-email-activities-edit-content.png)

5. **件名** （「基本プランメンバー向けアップグレードオファー」）を入力し、**メール本文を編集** ボタンをクリックします

   ![件名を追加してメール本文を編集](assets/add-email-activities-subject-line-edit-body.png)

6. 多くのオプションがあります。このテストでは、**独自のコードを作成** HTML オプションを選択します

   ![独自のHTML オプションのコードを選択](assets/add-email-activities-code-your-own-html.png)

7. **電子メール Designer**&#x200B;に、テスト行「Upgrade Offer Available!」を挿入します。 表示されている`</body></html>` タグの直前に、**保存**&#x200B;をクリックします

   ![電子メール Designerにテスト行を挿入し、「保存」をクリックします](assets/add-email-activities-email-designer-save.png)

8. 右下隅に確認メッセージが表示されるのを待ちます

   ![確認メッセージが表示されます](assets/add-email-activities-confirmation-message.png)

9. **電子メール Designer**&#x200B;の横にある&#x200B;**左向き矢印**&#x200B;をクリックして終了します

   ![左向き矢印をクリックしてメールDesignerを終了](assets/add-email-activities-exit-email-designer.png)

10. 確認ダイアログがポップアップ表示され、**保存して閉じる** ボタンをクリックします

![保存と閉じるボタンを含む確認ダイアログ ](assets/add-email-activities-save-and-close-dialog.png)

11. メール本文に追加されたテキストを含む、メールのプロパティとアクションを確認します。 **左向き矢印**&#x200B;をクリックして、キャンペーンキャンバスに戻ります

![Campaign キャンバスに戻る](assets/add-email-activities-back-to-campaign-canvas.png)

## 下部ブランチのメールアクティビティを追加

キャンペーンキャンバスに戻り、下部フローの&#x200B;**+**&#x200B;をクリックし、**チャネルアクティビティ**&#x200B;から&#x200B;**電子メール**&#x200B;を選択します。 以下を除き、上記と同じ手順（手順2～11）に従います。

- **電子メール** アクティビティのTarget Dimension **を使用して、ラベルを**&#x200B;電子メールに変更します
- メール設定で、**Relational-Email** メールチャネル設定を選択します

![ リレーショナルメールチャネルで設定された2番目のメールアクティビティ ](assets/add-email-activities-bottom-branch-relational-email.png "2番目のメールアクティビティを追加")

## まとめ

これで、メールチャネルでメールアクティビティを設定する方法を確認しました。 各アクティビティは、非常に基本的なメールの件名と本文で設定されました。 次にキャンペーン全体をテストします。
