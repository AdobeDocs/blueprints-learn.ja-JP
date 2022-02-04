---
title: Campaign v7 ブループリント
description: Adobe Campaign v7 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築されたキャンペーンツールです。 堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。 そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。  また、マーケティングチームが、パスワードのリセット、注文の確認、電子メールの受信などに関して、あらゆる IT システムの包括的なペイロードに基づいて事前に定義されたメッセージを送信できるリアルタイムメッセージングサーバーと組み合わせています。
solution: Campaign Classic v7
hidefromtoc: true
exl-id: d8cae05f-cf29-45f6-8ee0-1d670a31bdcc
source-git-commit: 13f750c0ff820ab01ed4fc615aba864bc2dc7b75
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Campaign v7 ブループリント

Adobe Campaign v7 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築されたキャンペーンツールです。 堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。 そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。  また、マーケティングチームが、パスワードのリセット、注文の確認、電子メールの受信などに関して、あらゆる IT システムの包括的なペイロードに基づいて事前に定義されたメッセージを送信できるリアルタイムメッセージングサーバーと組み合わせています。

<br>

## ユースケース

* バッチベースのメッセージングプログラム
* オンボーディングおよびリマーケティングキャンペーン
* ダイレクトメール広告、パンフレット、雑誌キャンペーン
* 少量のシンプルなトランザクションメッセージ（パスワードリセット、E メールの受信、注文確認など）

<br>

## アーキテクチャ

<img src="assets/campaign-v7-architecture.svg" alt="Campaign v7 ブループリントのリファレンスアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" />

<br>

## ブループリントのシナリオ

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [Journey OptimizerとAdobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizerを使用して、リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスの調整をおこない、ネイティブのAdobe Campaignトランザクションメッセージングシステムを活用してメッセージを送信する方法を示します | Adobe Campaignのネイティブリアルタイムメッセージング機能を利用してラストマイル通信を実行しながら、リアルタイム顧客プロファイルとJourney Optimizerの機能を活用して、瞬時のエクスペリエンスで調整<br><br>注意点：<br><ul><li>リアルタイムメッセージサーバーを介して 1 時間に最大 50,000 件のメッセージを送信可能<li>Journey Optimizerからのスロットルは実行されないので、プリセールスのエンタープライズアーキテクトが技術的な検証を行う</li><li>offer decisioningは、Campaign v7 リアルタイムメッセージングサーバーへのペイロードでサポートされていません</li></ul> |
| [Real-Time CDPとAdobe Campaign](rtcdp-and-campaign.md) | Adobe Experience PlatformのReal-Time CDPとその一元化されたセグメント化ツールをAdobe Campaignと共に使用して、パーソナライズされた会話を提供する方法を紹介します | <ul><li>製品化された宛先を介して、Experience PlatformからAdobe Campaign v8 にネイティブにオーディエンスを共有</li><li>顧客の会話から配信およびインタラクションデータをExperience Platformに取り込み、リアルタイム顧客プロファイルを強化し、メッセージングキャンペーンに関するクロスチャネルレポートを提供するネイティブサポート</li></ul> |

<br>

## 前提条件

### アプリケーションサーバおよびリアルタイムメッセージングサーバ

* Adobe Campaign Client Console は、Campaign v8 ソフトウェアとやり取りして使用するために必要です。 これは Windows ベースのクライアントで、標準のインターネットプロトコル（SOAP、HTTP など）を使用します。 ソフトウェアの配布、インストール、実行に必要な権限が組織で有効になっていることを確認します。

* IP アドレス許可リストへの登録
   * クライアントコンソールへのアクセス時にすべてのユーザーが利用する IP 範囲を特定します
   * リアルタイム・メッセージング・サーバとの通信を許可するエンタープライズ・システムの ID。また、許可リスト可能な IP または範囲が静的に割り当てられていることを確認します。
   * これは、CampaignCampaign コントロールパネルで設定および制御できます
* sFTP キー管理
   * SSH 公開鍵を Campaign で提供された SFTP で使用できるようにする。 これは、CampaignCampaign コントロールパネルで設定および制御できます。

### 電子メール

* メッセージ送信に使用するサブドメインの準備が整っている
* サブドメインは、Adobeに完全にデリゲートすることも（推奨）、CNAME を使用してAdobe固有の DNS サーバー（カスタム）を指すこともできます
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要です

### モバイルプッシュ

* モバイルデベロッパーを使用して、モバイルアプリをデプロイ、設定およびビルドできます
* Adobeは、メッセージペイロードをサーバーに送信するために必要な情報を FCM(Android) および APNS(iOS) から収集する SDK のみを提供しています。 モバイルアプリをコード化、デプロイ、管理、デバッグする必要があるのは、お客様の責任です

### Webapps （オプション）

* Campaign でホストされている購読解除およびランディングページ用に追加のサブドメインをデリゲートできます。
* SSL 証明書を強く推奨します

<br>

## ガードレール

### アプリケーションサーバーのサイズ設定

* ストレージは最大 1 億件のプロファイルに拡張可能
* Adobe Admin Console（推奨）を介した、またはアプリケーション自体でのローカルなユーザーアクセスの設定と制御
* Campaign へのデータの読み込みは、バッチファイルを使用しておこなう必要があります
   * API データの読み込みのサポートは、主にデータベース内のプロファイルや単純なオブジェクトの管理（作成と更新）に使用します。 大量のデータの読み込みや、バッチ操作などの操作には使用しません。
   * API を使用したカスタムアプリケーション目的でのデータ読み取りはサポートされていません
* API 呼び出しは、1 秒あたり 15 件または 1 日あたり 150,000 件に制限されています。

### バッチメッセージングサーバーのサイズ設定

* 1 時間あたり最大 2.500 万件のメッセージに対応可能

### リアルタイムメッセージングサーバーのサイズ設定

* 1 時間に最大 50,000 件のメッセージを送信可能
* デフォルトでは、1 台のリアルタイムメッセージングサーバーのみがプロビジョニングされます。 これは、24 時間で期限切れになるセッショントークンを介して、サーバーとの通信が確実におこなわれるようにするためです
* オプションで、最大 8 台のリアルタイムメッセージングサーバーをデプロイできますが、認証ではユーザー/パスのみがサポートされます
* 推奨されるアプローチは、常に 1 つのリアルタイムメッセージングサーバーを利用して、可能な限りセッショントークンベースの認証を活用することです

### SMS 設定

* Campaign には、と SMS プロバイダーを統合する機能が用意されています。 プロバイダーは、顧客によって調達され、SMS ベースのメッセージを送信するためのキャンペーンと統合されます
* サポートは、SMPP プロトコルを使用します。
* 次の 3 種類の SMS があり、Adobeがサポートします。
   * SMS MT （モバイル終了）:Adobe Campaignが SMPP プロバイダーを通じて携帯電話に向けて発信する SMS。
   * SMS MO（モバイル発信）:携帯電話から SMPP プロバイダー経由でAdobe Campaignに送信される SMS。
   * SMS SR（ステータスレポート）、DR または DLR（配信受信）:SMS が正常に受信されたことを示す返信確認メッセージが、SMPP プロバイダーを通じてAdobe Campaignに送信されました。 Adobe Campaignは、メッセージが配信できなかったことを示す SR を受け取る場合もあり、多くの場合、エラーの説明が記載されています。

### モバイルプッシュ設定

* プッシュ通知用にモバイルデバイスとの統合に関してサポートされる 2 つの方法を示します。
   * Experience Platformモバイル SDK （推奨）
   * Campaign モバイル SDK
* Experience Platformモバイル SDK のルート：
   * AdobeタグとCampaign Classic拡張機能を活用して、Experience PlatformMobile SDK との統合を設定します。
   * Adobeタグとデータ収集に関する実務知識が必要
   * SDK のデプロイには Android とiOSの両方でプッシュ通知を使用したモバイル開発エクスペリエンスが必要で、FCM(Android) や APNS(iOS) と統合してプッシュトークンを取得し、プッシュ通知を受信してプッシュインタラクションを処理するにはアプリを設定
* Campaign モバイル SDK
   * Adobeカスタマーケアに連絡して、
   * 詳しくは、 [Campaign SDK ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) SDK のインストールと設定の方法について説明します。

   >[!IMPORTANT]
   >Campaign SDK をデプロイし、他のExperience Cloudアプリケーションと連携する場合は、データ収集にExperience Platformの Mobile SDK を使用する必要があります。 これは別の SDK なので、Campaign SDK と共にインストールする必要があります

<br>

## 実装手順

詳しくは、 [はじめに](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=en) Adobe Campaign v7 の実装


## 関連ドキュメント

* [Campaign v7 ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign v7 製品説明](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
