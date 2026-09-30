---
title: セットアップ
description: AJO Foundations ラボを開始する前に、サンドボックスのデプロイメントとPostmanの設定手順を完了してください。
doc-type: article
solution: Experience Platform
exl-id: 7c1a9e3d-5b8f-4a2e-9c6d-3f7b0e4a8c2d
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 1d6ba1444c119437eb8a86d5c4a1050d56d16023
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%
---

# セットアップ

AJO Foundations ラボを開始する前に、以下の設定手順を完了してください。 どのステップが必要かは、このブートキャンプの進め方によって異なります。

## サンドボックス設定

>[!NOTE]
>
>ライブトレーニングコースやイベントに参加されている場合は、サンドボックスが既にデプロイされています。このセクションをスキップして、以下のPostman設定に直接移動してください。

ラボアセットがデプロイされた作業用サンドボックスがまだ存在しない場合は、次の手順を実行します。

- [Developer Consoleの設定](sandbox-setup/developer-console-setup.md)
- [デプロイメントの手順](sandbox-setup/deployment-instructions.md)

## Postmanの設定

サンドボックスのプロビジョニング方法に関係なく、このコースのラボにはPostmanが必要です。 続行する前に、次の項目を完了してください。

- [Postman インストール](postman-setup/postman-installation.md)
- [環境ファイルを読み込む](postman-setup/import-environment-file.md)
- [API コレクションのインポート](postman-setup/import-api-collection.md)

## オンデマンド対応

ラボを開始する前に、上記のPostman設定を完了してください。 自習型学習者には、メールに依存するラボ用のデリゲートされたサブドメインと、Flagship phone launch lab用のSMS資格情報も必要です。

## チャネルの前提条件

このブートキャンプの後半にある2つのラボは、自習型学習者のみが配置する必要がある外部アカウントに依存しています。ライブトレーニングコースやイベントの場合、これらのアカウントは既にプロビジョニングされています。

### デリゲートされたサブドメイン

[ メールチャネルの設定](data-stores/configure-email-channels/overview.md) ラボ – およびそれに依存するすべて（[実際のメッセージ配信](orchestrated-campaigns/message-delivery-in-action/overview.md)、[購入後の興奮](journeys/post-purchase-excitement/overview.md)、[AJO Brands](content-authoring-with-ai/overview.md)）では、メールを送信するためにAdobeにデリゲートされたサブドメインが必要です。 ドメインがまだ存在しない場合は、任意のドメインレジストラー（Namecheapなど）に登録します。 次に、そのサブドメイン（例：`email.yourdomain.com`）をAdobeにデリゲートするには、Adobeの[ サブドメインデリゲートの手順](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/delegate-subdomains/delegate-subdomain)に従います。

>[!NOTE]
>
>サブドメインのデリゲーションは、伝播に時間がかかる場合があります。 メールチャネルの設定ラボに到達する前に、このデリゲーションを十分に開始してください。

### SMS 資格情報

[Flagship phone launch](orchestrated-campaigns/flagship-phone-launch/overview.md) ラボは、Twilioを通じてSMS チャネルを設定します。 メッセージは送信されませんが、設定を完了するには作業用の資格情報が必要です。 最も簡単なオプションは、無料の[Twilio体験版アカウント ](https://www.twilio.com/try-twilio)です。アカウント SIDと認証トークンを登録して見つける方法については、Twilioの[入門ガイド ](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account)を参照してください。
