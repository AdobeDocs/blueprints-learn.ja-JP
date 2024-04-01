---
title: Campaign v8 ブループリント、Campaign および Platform
description: Campaign v8 のブループリントについて説明します。
solution: Campaign,Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 16b233c7ea9077566ebf12238f0a87beec1c61ce
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 41%

---

# Campaign v8 ブループリント

Adobe Campaign v8 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築された次世代キャンペーンツールです。堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。

また、拡張性の高いリアルタイムメッセージングサーバーと組み合わせることで、マーケティングチームは、パスワードのリセット、注文確認、電子領収書など、あらゆる IT システムから包括的なペイロードに基づいて事前に定義したメッセージを送信することが可能になります。

## ユースケース

* 非常に複雑なバッチベースのメッセージングプログラム。
* オンボーディングおよびリマーケティングキャンペーン。
* ダイレクトメール広告、パンフレット、雑誌キャンペーン
* シンプルなトランザクションメッセージ（パスワードリセット、電子メールの受信、注文確認など）。
* 分析およびプロファイル作成のためのAdobe Experience Platformへの Campaign データの統合。
* Real-time Customer Data Platform オーディエンスの Campaign への共有。

## アーキテクチャ図

詳細情報： [Campaign v8 デプロイメントモデル](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html#ac-deployment){target="_blank"}.

### Campaign エンタープライズ (FFDA) デプロイメント

<img src="assets/P4-architecture.png" alt="Campaign v8 ブループリント (P4) のリファレンスアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

### Campaign v8 FDA デプロイメント

<img src="assets/P1-P3-architecture.png" alt="Campaign v8 ブループリントのリファレンスアーキテクチャ (P1-P3)" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 統合パターン

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [[!DNL Real-time Customer Data Platform] Adobe [!DNL Campaign]](rtcdp-and-campaign-v8.md) | Adobe Experience Platformとそのリアルタイム顧客プロファイルおよび一元化されたセグメント化ツールをAdobeと共に使用する方法を紹介します [!DNL Campaign] パーソナライズされた会話を配信する | <ul><li>からのプロファイルおよびオーディエンスの共有 [!DNL Real-Time CDP] Adobe [!DNL Campaign] クラウドストレージのファイル交換とAdobeを使用 [!DNL Campaign] 取り込みワークフロー </li><li>顧客との会話からに戻る配信およびインタラクションデータを簡単に共有 [!DNL Real-Time CDP] Adobeから [!DNL Campaign] リアルタイム顧客プロファイルを強化し、メッセージングキャンペーンに関するクロスチャネルレポートを提供する</li></ul> |
| [[!DNL Journey Optimizer] Adobe [!DNL Campaign]](ajo-and-campaign.md) | Adobe Journey Optimizerを使用して、リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスを調整し、ネイティブAdobeを活用する方法を示します [!DNL Campaign] メッセージを送信するトランザクションメッセージングシステム | リアルタイムの顧客プロファイルとの力を活用する [!DNL Journey Optimizer] Adobeのネイティブリアルタイムメッセージング機能を利用して、瞬時のエクスペリエンスで調整する [!DNL Campaign] 最後の 1 マイルの通信を行う<br><br>注意点：<br><ul><li>リアルタイムメッセージサーバーを介して 1 時間に最大 100 万件のメッセージを送信可能<li>からのスロットルは実行されません [!DNL Journey Optimizer] プリセールスエンタープライズアーキテクトによる技術的な検証を確実に行う</li><li>意思決定管理は、Campaign v8 へのペイロードではサポートされていません</li></ul> |

## 前提条件

このブループリントには、次の前提条件が存在します。

### アプリケーションサーバーおよびリアルタイムメッセージングサーバー

* Adobe [!DNL Campaign] クライアントコンソールは、 [!DNL Campaign] v8 ソフトウェア。 これは Windows ベースのクライアントで、標準のインターネットプロトコル（SOAP、HTTP など）を使用します。ソフトウェアの配布、インストール、実行に必要な権限が組織で有効になっていることを確認します。

* IP アドレスの許可リストへの登録：
   * クライアントコンソールへのアクセス時にすべてのユーザーが利用する IP 範囲を特定します。
   * リアルタイム・メッセージング・サーバとの通信が許可されているエンタープライズ・システムの ID。また、許可リストに登録できる IP または範囲が静的に割り当てられていることを確認します。
   * これは、Campaign コントロールパネルで設定および制御できます。
* sFTP キー管理：
   * SSH パブリックキーを Campaign で提供された sFTP で使用できるようにします。これは、Campaign コントロールパネルで設定および制御できます。

### 電子メール

* メッセージの送信に使用できるサブドメインを用意します。
* サブドメインは、Adobeに完全にデリゲートすることも（推奨）、CNAME を使用してAdobe固有の DNS サーバー（カスタム）を指すこともできます。
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要です。

### モバイルプッシュ

* モバイルデベロッパーを使用して、モバイルアプリをデプロイ、設定および構築できます。
* アドビは、メッセージペイロードをサーバーに送信するために必要な情報を FCM（Android）および APNS（iOS）から収集する SDK のみを提供しています。モバイルアプリをコード化、デプロイ、管理、デバッグする方法は、お客様の責任です。

### Webapps（オプション）

* Campaign でホストされている購読解除およびランディングページ用に追加のサブドメインをデリゲートできます。
* SSL 証明書を強くお勧めします。

## ガードレール

ガードレールについては、以下で説明します。

### アプリケーションサーバーのサイズ設定

* ストレージは、最大 2 億のプロファイルに拡張でき、最大 1B のプロファイルに拡張できます。
* Adobeを介したユーザーアクセスの設定と制御 [!DNL Admin Console].
* へのデータ読み込み [!DNL Campaign] は、次のバッチファイルを使用して実行されると想定されます。
   * API データの読み込みのサポートは、主にデータベース内のプロファイルや単純なオブジェクトの管理（作成と更新）に使用します。大量のデータの読み込みや、バッチ操作などの操作に向けたものではありません。
   * API を使用したカスタムアプリケーション目的でのデータ読み取りはサポートされていません
   * API を介して読み込まれたデータは、アプリケーションデータベースでステージングされ、1 時間ごとにクラウドデータベースにレプリケートされます
* API 呼び出しに制限が適用されます。 詳しくは、 [Adobe Campaign Product Description](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"}.

### バッチメッセージングサーバーのサイズ設定

* 1 時間あたり最大 2,000 万件のメッセージに対応可能

### リアルタイムメッセージングサーバーのサイズ設定

* 1 時間に最大 100 万件のメッセージを送信可能
* デフォルトでは、2 つのリアルタイムメッセージングサーバーがプロビジョニングされます。最大 8 台のリアルタイムメッセージングサーバーを拡張可能

### SMS 設定

* Campaign には、SMS プロバイダーと統合される機能が用意されています。プロバイダーは、顧客によって調達され、SMS ベースのメッセージを送信するためのキャンペーンと統合されます。
* サポートは、SMPP プロトコルを介しておこなわれます。
* 次の 3 種類の SMS があり、アドビがサポートします。
   * SMS MT（モバイル終了）:Adobeから発信される SMS [!DNL Campaign] SMPP プロバイダーを通じて携帯電話に向かって
   * SMS MO（モバイル発信）：携帯電話からAdobeに送信される SMS [!DNL Campaign] SMPP プロバイダー経由で使用する。
   * SMS SR（ステータスレポート）、DR または DLR（配信受信）：携帯電話からAdobeに送信される返信受信 [!DNL Campaign] SMS が正常に受信されたことを示す SMPP プロバイダーを通じて。 Adobe [!DNL Campaign] また、は、メッセージが配信できなかったことを示す SR を受け取る場合もあります。多くの場合、エラーの説明が記載されています。

## 実装手順

[Adobe Campaign v8 の実装](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=ja)の入門ガイドを参照してください。

## 関連ドキュメント

* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html)
* [Campaign v8 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/launch.html)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html)
