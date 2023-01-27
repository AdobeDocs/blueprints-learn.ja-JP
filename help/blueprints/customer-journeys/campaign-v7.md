---
title: Campaign v7 ブループリント
description: Adobe Campaign v7 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築されたキャンペーンツールです。堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。また、リアルタイムメッセージングサーバーと組み合わせることで、マーケティングチームは、パスワードのリセット、注文確認、電子領収書など、あらゆる IT システムから包括的なペイロードに基づいて事前に定義したメッセージを送信することが可能になります。
solution: Campaign,Campaign Classic v7
exl-id: 71c808f5-59e6-4f49-a6ba-581ed508bc04
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 94%

---

# Campaign v7 ブループリント

Adobe Campaign v7 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築されたキャンペーンツールです。堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。また、リアルタイムメッセージングサーバーと組み合わせることで、マーケティングチームは、パスワードのリセット、注文確認、電子領収書など、あらゆる IT システムから包括的なペイロードに基づいて事前に定義したメッセージを送信することが可能になります。

<br>

## 使用例

* バッチベースのメッセージングプログラム
* オンボーディングおよびリマーケティングキャンペーン
* ダイレクトメール広告、パンフレット、雑誌キャンペーン
* 少量のシンプルなトランザクションメッセージ（パスワードリセット、電子メールの受信、注文確認など）

<br>

## アーキテクチャ

<img src="assets/campaign-v7-architecture.svg" alt="Campaign v7 ブループリントの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 統合パターン

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [Real-Time CDP と Adobe Campaign](rtcdp-and-campaign.md) | Adobe Experience Platform の Real-Time CDP とその一元化されたセグメント化ツールを Adobe Campaign と併用して、パーソナライズされた会話を提供する方法を紹介します | <ul><li>クラウドストレージのファイル交換と Adobe Campaign の取り込みワークフローを使用した、Real-Time CDP から Adobe Campaign へのプロファイルとオーディエンスの共有 </li><li>顧客との会話から得られた配信データとインタラクションデータを Adobe Campaign から リアルタイムReal-Time CDP に戻し、リアルタイム顧客プロファイルとメッセージングキャンペーンのクロスチャネルレポートの両方を簡単に共有できる</li></ul> |
| [Journey Optimizer と Adobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizer を使用し、リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスの調整を行い、ネイティブの Adobe Campaign トランザクションメッセージングシステムを活用してメッセージを送信する方法を示します | リアルタイム顧客プロファイルと Journey Optimizer の機能を活用し、瞬時のエクスペリエンスで調整しながら、Adobe Campaign のネイティブリアルタイムメッセージング機能を利用して、ラストマイルのコミュニケーションを実現します。<br><br>注意点：<br><ul><li>リアルタイムメッセージサーバーを介して 1 時間に最大 50,000 件のメッセージを送信可能<li>Journey Optimizer からのスロットリングは行われませんので、プリセールスのエンタープライズアーキテクトによる技術的な検証を必ず行います</li><li>Campaign v7 リアルタイムメッセージングサーバーへのペイロードでは、意思決定管理 はサポートされていません。</li></ul> |

<br>

## 前提条件

### アプリケーションサーバーとリアルタイムメッセージングサーバー

* Adobe Campaign Client Console は、Campaign v8 ソフトウェアとやり取りして使用するために必要です。これは Windows ベースのクライアントで、標準のインターネットプロトコル（SOAP、HTTP など）を使用します。ソフトウェアの配布、インストール、実行に必要な権限が組織で有効になっていることを確認します。

* IP アドレス許可リストへの登録
   * クライアントコンソールへのアクセス時にすべてのユーザーが利用する IP 範囲を指定します
   * リアルタイム・メッセージング・サーバとの通信を許可するエンタープライズ・システムの ID。また、許可リスト可能な IP または範囲が静的に割り当てられていることを確認します。
   * これは、Campaign コントロールパネルで設定および制御可能
* sFTP キー管理
   * SSH パブリックキーを Campaign で提供された sFTP で使用できるようにします。これは、Campaign コントロールパネルで設定および制御できます。

### 電子メール

* メッセージ送信に使用するサブドメインの準備を整える
* サブドメインは、アドビに完全にデリゲートすることも（推奨）、CNAME を使用してアドビ固有の DNS サーバー（カスタム）を指すこともできます
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要

### モバイルプッシュ

* モバイルデベロッパーを使用して、モバイルアプリをデプロイ、設定およびビルドが可能
* アドビは、メッセージペイロードをサーバーに送信するために必要な情報を FCM（Android）および APNS（iOS）から収集する SDK のみを提供しています。モバイルアプリをコード化、デプロイ、管理、デバッグするのは、お客様の責任です

### Webapps（オプション）

* Campaign でホストされている購読解除およびランディングページ用に追加のサブドメインのデリゲートが可能
* SSL 証明書を強く推奨します

<br>

## ガードレール

### アプリケーションサーバーのサイズ設定

* ストレージは最大 1 億件のプロファイルに拡張可能
* Adobe Admin Console（推奨）を介した、またはアプリケーション自体でのローカルなユーザーアクセスの設定と制御
* Campaign へのデータの読み込みは、バッチファイルを使用して行う必要があります
   * API データの読み込みのサポートは、主にデータベース内のプロファイルや単純なオブジェクトの管理（作成と更新）に使用します。大量のデータの読み込みや、バッチ操作などの操作に向けたものではありません。
   * API を使用したカスタムアプリケーション目的でのデータ読み取りはサポートされていません
* API 呼び出しは、1 秒あたり 15 件または 1 日あたり 150,000 件に制限されます

### バッチメッセージングサーバーのサイズ設定

* 1 時間あたり最大 2,500 万件のメッセージに対応可能

### リアルタイムメッセージングサーバーのサイズ設定

* 1 時間に最大 50,000 件のメッセージを送信可能
* デフォルトでは、2 つのリアルタイムメッセージングサーバーがプロビジョニングされます。最大 8 台のリアルタイムメッセージングサーバーを拡張可能

### SMS 設定

* Campaign には、SMS プロバイダーと統合される機能が用意されています。プロバイダーは、顧客によって調達され、SMS ベースのメッセージを送信するためのキャンペーンと統合されます
* サポートは、SMPP プロトコル経由で
* 次の 3 種類の SMS があり、アドビがサポートします。
   * SMS MT （モバイル終了）：Adobe Campaign が SMPP プロバイダーを通じて携帯電話に向けて発信する SMS。
   * SMS MO（モバイル発信）：携帯電話から SMPP プロバイダー経由で Adobe Campaign に送信される SMS。
   * SMS SR（ステータスレポート）、DR または DLR（配信受信）：SMS が正常に受信されたことを示す返信確認メッセージが、SMPP プロバイダーを通じて Adobe Campaign に送信されました。Adobe Campaign は、メッセージが配信できなかったことを示す SR を受け取る場合もあり、多くの場合、エラーの説明が記載されています。

### モバイルプッシュ設定

* プッシュ通知用にモバイルデバイスとの統合に関してサポートされる 2 つの方法を示します。
   * Experience Platform Mobile SDK（推奨）
   * Campaign モバイル SDK
* Experience Platform Mobile SDK ルート：
   * アドビタグと Campaign Classic 拡張機能を活用して、Experience Platform Mobile SDK との統合を設定します。
   * アドビタグとデータ収集に関する実務知識が必要です
   * SDK のデプロイ、FCM（Android）および APNS（iOS）との統合によるプッシュトークンの取得、プッシュ通知を受け取るためのアプリの設定、プッシュインタラクションの処理など、Android および iOS でのプッシュ通知に関するモバイル開発経験が必要です。
* Campaign モバイル SDK
   * アドビカスタマーケアに連絡
   * SDK のインストールと設定の方法については、[Campaign SDK ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=ja)を参照してください。

   >[!IMPORTANT]
   >Campaign SDK をデプロイし、他の Experience Cloud アプリケーションと連携する場合は、データ収集に Experience Platform Mobile SDK を使用する必要があります。これは別の SDK なので、Campaign SDK と共にインストールする必要があります

<br>

## 実装の手順

Adobe Campaign v7 の実装に関しては、[はじめる前に](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=ja)を参照してください。


## 関連ドキュメント

* [Campaign v7 ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign v7 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
