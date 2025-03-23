---
title: Campaign v8 ブループリント、Campaign および Platform
description: Campaign v8 のブループリントについて説明します。
solution: Campaign,Campaign v8
version: Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 1d10727899aaae6b8cd339ce10d2a520c73bdaa2
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 41%

---

# Campaign v8 ブループリント

Adobe Campaign v8 は、電子メールやダイレクトメールなどの従来のマーケティングチャネル用に構築された次世代キャンペーンツールです。堅牢な ETL およびデータ管理機能を提供し、最適なキャンペーンの作成とキュレーションを支援します。そのオーケストレーションエンジンは、バッチベースのジャーニーに重点を置いた、豊富なマルチタッチマーケティングプログラムを提供します。

また、拡張性の高いリアルタイムメッセージングサーバーと組み合わせることで、マーケティングチームは、パスワードのリセット、注文確認、電子領収書など、あらゆる IT システムから包括的なペイロードに基づいて事前に定義したメッセージを送信することが可能になります。

## ユースケース

* 非常に複雑なバッチベースメッセージプログラム。
* オンボーディングおよびリマーケティングキャンペーン。
* ダイレクトメール広告、パンフレット、雑誌キャンペーン
* シンプルなトランザクションメッセージ（パスワードリセット、メールの受信、注文の確認など）。
* 分析とプロファイル構築のためのAdobe Experience Platformへの Campaign データの統合。
* Real-time Customer Data Platform オーディエンスの Campaign への共有。

## アーキテクチャ図

[Campaign v8 デプロイメントモデル ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html#ac-deployment){target="_blank"} の詳細情報。

### Campaign Enterprise （FFDA）デプロイメント

<img src="assets/P4-architecture.png" alt="Campaign v8 ブループリント（P4）のリファレンスアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

### Campaign v8 FDA デプロイメント

<img src="assets/P1-P3-architecture.png" alt="Campaign v8 ブループリント（P1～P3）のリファレンスアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 統合パターン

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [[!DNL Real-time Customer Data Platform] Adobeを使用  [!DNL Campaign]](rtcdp-and-campaign-v8.md) | Adobe Experience Platformとそのリアルタイム顧客プロファイルおよび一元化されたセグメンテーションツールをAdobe [!DNL Campaign] と共に利用して、パーソナライズされた会話を提供する方法を紹介します | <ul><li>クラウドストレージのファイル交換ワークフローおよびAdobe [!DNL Campaign] ータ取り込みワークフローを使用した、[!DNL Real-Time CDP] からAdobe [!DNL Campaign] へのプロファイルとオーディエンスの共有 </li><li>Adobe [!DNL Campaign] から [!DNL Real-Time CDP] ージに送り返される、お客様の会話からの配信およびインタラクションデータを簡単に共有して、リアルタイム顧客プロファイルを強化し、メッセージキャンペーンに関するクロスチャネルレポートを提供します</li></ul> |
| [[!DNL Journey Optimizer] Adobeを使用  [!DNL Campaign]](ajo-and-campaign.md) | Adobe Journey Optimizerを使用して、リアルタイム顧客プロファイルを利用して 1 対 1 のエクスペリエンスを調整し、ネイティブのAdobe [!DNL Campaign] トランザクションメッセージシステムを活用してメッセージを送信する方法を示します | リアルタイム顧客プロファイルと [!DNL Journey Optimizer] の機能を活用して、即座にエクスペリエンスを調整すると同時に、Adobe [!DNL Campaign] のネイティブなリアルタイムメッセージ機能を活用してラストマイルでのコミュニケーションを実現します <br><br> 考慮事項：<br><ul><li>リアルタイムメッセージサーバーを介して 1 時間に最大 100 万件のメッセージを送信可能<li>[!DNL Journey Optimizer] からスロットリングが実行されないので、事前にセールスエンタープライズアーキテクトが技術的な検証を行います。</li><li>意思決定管理は、Campaign v8 へのペイロードではサポートされていません</li></ul> |

## 前提条件

このブループリントには次の前提条件があります。

### アプリケーションサーバーおよびリアルタイムメッセージングサーバー

* Adobe [!DNL Campaign] クライアントコンソールは、[!DNL Campaign] v8 ソフトウェアとやり取りして使用するために必要です。 これは Windows ベースのクライアントで、標準のインターネットプロトコル（SOAP、HTTP など）を使用します。ソフトウェアの配布、インストール、実行に必要な権限が組織で有効になっていることを確認します。

* IP アドレスの許可リストへの登録：
   * クライアントコンソールへのアクセス時にすべてのユーザーが利用する IP 範囲を識別します。
   * リアルタイムメッセージングサーバーとの通信を許可されるエンタープライズシステムの ID で、許可リストに登録できる IP または範囲が静的に割り当てられていることを確認します。
   * これは、Campaign コントロールパネルで設定および制御できます。
* sFTP キー管理：
   * SSH パブリックキーを Campaign で提供された sFTP で使用できるようにします。これは、Campaign コントロールパネルで設定および制御できます。

### 電子メール

* メッセージ送信に使用するサブドメインを準備します。
* サブドメインは、Adobeに完全にデリゲートするか（推奨）、CNAME を使用してAdobe固有の DNS サーバーを指すことができます（カスタム）。
* Google TXT レコードは、優れた配信品質を確保するためにサブドメインごとに必要です。

### モバイルプッシュ

* モバイルアプリのデプロイ、設定、ビルドを行えるモバイル開発者を用意します。
* アドビは、メッセージペイロードをサーバーに送信するために必要な情報を FCM（Android）および APNS（iOS）から収集する SDK のみを提供しています。モバイルアプリをどのようにコーディング、デプロイ、管理、デバッグする必要があるかは、お客様の責任です。

### Webapps（オプション）

* Campaign がホストする登録解除ページとランディングページに追加のサブドメインをデリゲートできます。
* SSL 証明書が強く推奨されます。

## ガードレール

ガードレールについては、以下で説明します。

### アプリケーションサーバーのサイズ設定

* ストレージは最大 2000 万プロファイルまで拡張でき、最大 1 B のプロファイルまで拡張できる可能性があります。
* Adobe [!DNL Admin Console] を介してユーザーアクセスを設定および制御します。
* [!DNL Campaign] へのデータ読み込みは、バッチファイルを使用して行うことが想定されています。
   * API データの読み込みのサポートは、主にデータベース内のプロファイルや単純なオブジェクトの管理（作成と更新）に使用します。大量のデータの読み込みや、バッチ操作などの操作に向けたものではありません。
   * API を使用したカスタムアプリケーション目的でのデータ読み取りはサポートされていません
   * API を介して読み込まれたデータは、アプリケーションデータベースでステージングされ、1 時間ごとにクラウドデータベースにレプリケートされます
* API 呼び出しの制限が適用されます。 詳しくは、[Adobe Campaignの製品説明 ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"} を参照してください。

### バッチメッセージングサーバーのサイズ設定

* 1 時間あたり最大 2,000 万件のメッセージに対応可能

### リアルタイムメッセージングサーバーのサイズ設定

* 1 時間に最大 100 万件のメッセージを送信可能
* デフォルトでは、2 つのリアルタイムメッセージングサーバーがプロビジョニングされます。最大 8 台のリアルタイムメッセージングサーバーを拡張可能

### SMS 設定

* Campaign には、SMS プロバイダーと統合される機能が用意されています。プロバイダーは、顧客によって調達され、SMS ベースのメッセージを送信するためのキャンペーンと統合されます。
* SMPP プロトコルによるサポート。
* 次の 3 種類の SMS があり、アドビがサポートします。
   * SMS MT （Mobile Terminated）: Adobe [!DNL Campaign] から SMPP プロバイダーを通じて携帯電話に送信される SMS です。
   * SMS MO （Mobile Originated）: モバイルから SMPP プロバイダーを通じてAdobe [!DNL Campaign] に送信される SMS です。
   * SMS SR （ステータスレポート）または DR または DLR （配信確認）: SMS が正常に受信されたことを示す、SMPP プロバイダーを通じてAdobe [!DNL Campaign] にモバイルから送信された再来訪の確認メッセージ。 Adobe [!DNL Campaign] は、メッセージを配信できなかったことを示す SR を（多くの場合エラーの説明と共に）受け取る場合もあります。

## 実装手順

[Adobe Campaign v8 の実装](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=ja)の入門ガイドを参照してください。

## 関連ドキュメント

* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html)
* [Campaign v8 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/launch.html)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html)
