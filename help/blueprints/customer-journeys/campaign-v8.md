---
title: Campaign v8 ブループリント
description: Adobe Campaign v8 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築された次世代キャンペーンツールです。堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。また、拡張性の高いリアルタイムメッセージングサーバーと組み合わせることで、マーケティングチームは、パスワードのリセット、注文確認、電子領収書など、あらゆる IT システムから包括的なペイロードに基づいて事前に定義したメッセージを送信することが可能になります。
solution: Campaign,Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 37fa3bc00175a4636766564f0b8fb847fa8a951e
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 99%

---

# Campaign v8 ブループリント

Adobe Campaign v8 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築された次世代キャンペーンツールです。堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。また、拡張性の高いリアルタイムメッセージングサーバーと組み合わせることで、マーケティングチームは、パスワードのリセット、注文確認、電子領収書など、あらゆる IT システムから包括的なペイロードに基づいて事前に定義したメッセージを送信することが可能になります。

<br>

## ユースケース

* 非常に複雑なバッチベースのメッセージングプログラム
* オンボーディングおよびリマーケティングキャンペーン
* ダイレクトメール広告、パンフレット、雑誌キャンペーン
* シンプルなトランザクションメッセージ（パスワードリセット、電子メールの受信、注文確認など）

<br>

## アーキテクチャ

<img src="assets/campaign-v8-architecture.svg" alt="Campaign v8 ブループリントの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 統合パターン

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [Journey Optimizer と Adobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizer を使用して、リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスの調整をおこない、ネイティブの Adobe Campaign トランザクションメッセージングシステムを活用してメッセージを送信する方法を示します | リアルタイム顧客プロファイルと Journey Optimizer の機能を活用し、瞬時のエクスペリエンスで調整しながら、Adobe Campaign のネイティブリアルタイムメッセージング機能を利用して、ラストマイルのコミュニケーションを実現します。<br><br>注意点：<br><ul><li>リアルタイムメッセージサーバーを介して 1 時間に最大 100 万件のメッセージを送信可能<li>Journey Optimizer からのスロットリングは行われませんので、プリセールスのエンタープライズアーキテクトによる技術的な検証を必ず行います</li><li>決定管理は、Campaign v8 へのペイロードではサポートされていません</li></ul> |

<br>

## 前提条件


### アプリケーションサーバおよびリアルタイムメッセージングサーバ

* Adobe Campaign Client Console は、Campaign v8 ソフトウェアとやり取りして使用するために必要です。これは Windows ベースのクライアントで、標準のインターネットプロトコル（SOAP、HTTP など）を使用します。ソフトウェアの配布、インストール、実行に必要な権限が組織で有効になっていることを確認します。

* IP アドレス許可リストへの登録
   * クライアントコンソールへのアクセス時にすべてのユーザーが利用する IP 範囲を指定します
   * リアルタイムメッセージングサーバとの通信を許可するエンタープライズシステムの ID。また、許可リスト登録可能な IP または範囲が静的に割り当てられていることを確認します。
   * これは、Campaign コントロールパネルで設定および制御可能
* sFTP キー管理
   * SSH 公開鍵を Campaign で提供された sFTP で使用できるようにします。これは、Campaign コントロールパネルで設定および制御できます。

### 電子メール

* メッセージ送信に使用するサブドメインの準備を整える
* サブドメインは、アドビに完全にデリゲートすることも（推奨）、CNAME を使用してアドビ固有の DNS サーバー（カスタム）を指すこともできます
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要

### モバイルプッシュ

* モバイルデベロッパーを使用して、モバイルアプリをデプロイ、設定およびビルドが可能
* アドビは、メッセージペイロードをサーバーに送信するために必要な情報を FCM (Android) および APNS (iOS) から収集する SDK のみを提供しています。モバイルアプリをコード化、デプロイ、管理、デバッグするのは、お客様の責任です

### Webapps（オプション）

* Campaign でホストされている購読解除およびランディングページ用に追加のサブドメインのデリゲートが可能
* SSL 証明書を強く推奨します

<br>

## ガードレール

### アプリケーションサーバーのサイズ設定

* ストレージは最大 2 億のプロファイルに拡張可能で、最大 1B のプロファイルに拡張可能
* Adobe Admin Console を介したユーザーアクセスの設定と制御
* Campaign へのデータの読み込みは、バッチファイルを使用しておこなう必要があります
   * API データの読み込みのサポートは、主にデータベース内のプロファイルや単純なオブジェクトの管理（作成と更新）に使用します。大量のデータの読み込みや、バッチ操作などの操作に向けたものではありません。
   * API を使用したカスタムアプリケーション目的でのデータ読み取りはサポートされていません
   * API を介して読み込まれたデータは、アプリケーションデータベースでステージングされ、1 時間ごとにクラウドデータベースにレプリケートされます
* API 呼び出しは、1 秒あたり 15 件または 1 日あたり 150,000 件に制限されます

### バッチメッセージングサーバーのサイズ設定

* 1 時間あたり最大 2,000 万件のメッセージに対応可能

### リアルタイムメッセージングサーバーのサイズ設定

* 1 時間に最大 100 万件のメッセージを送信可能
* デフォルトでは、2 つのリアルタイムメッセージングサーバーがプロビジョニングされます。最大 8 台のリアルタイムメッセージングサーバを拡張可能

### SMS 設定

* Campaign には、SMS プロバイダーと統合される機能が用意されています。プロバイダーは、顧客によって調達され、SMS ベースのメッセージを送信するためのキャンペーンと統合されます
* サポートは、SMPP プロトコル経由で
* 次の 3 種類の SMS があり、アドビがサポートします。
   * SMS MT （モバイル終了）：Adobe Campaign が SMPP プロバイダーを通じて携帯電話に向けて発信する SMS。
   * SMS MO（モバイル発信）：携帯電話から SMPP プロバイダー経由で Adobe Campaign に送信される SMS。
   * SMS SR（ステータスレポート）、DR または DLR（配信受信）：SMS が正常に受信されたことを示す返信確認メッセージが、SMPP プロバイダーを通じて Adobe Campaign に送信されました。Adobe Campaign は、メッセージが配信できなかったことを示す SR を受け取る場合もあり、多くの場合、エラーの説明が記載されています。

### モバイルプッシュ設定

* Campaign SDK のみが、Campaign v8 ではサポートされています。アドビカスタマーケアに連絡
* SDK のインストールと設定の方法については、[Campaign SDK ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=ja) を参照してください。

   >[!IMPORTANT]
   >その他の Experience Cloud アプリケーションでは、データ収集に Experience Platform Mobile SDK を使用する必要があります。これは別の SDK なので、Campaign SDK と共にインストールする必要があります

<br>

## 実装手順

[Adobe Campaign v8 の実装](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=ja) の入門ガイドを参照してください。


## 関連ドキュメント

* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja)
* [Campaign v8 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
