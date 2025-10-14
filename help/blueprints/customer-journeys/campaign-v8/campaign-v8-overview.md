---
title: Campaign v8 ブループリント、Campaign および Platform
description: Campaign v8 のブループリントについて説明します。
solution: Campaign,Campaign v8
version: Campaign v8
exl-id: 89b3a761-9cb3-4e01-8da0-043e634fa61f
source-git-commit: 0a3ebcbc6029df46bd988cb8f15ecf838f80c3c9
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 31%

---

# Campaign v8 ブループリント

Adobe Campaign v8 は、メールやダイレクトメールなどの従来のマーケティングチャネル用に設計された、次世代のキャンペーン管理プラットフォームです。 複雑なセグメント化とオーディエンスのターゲティングをサポートする堅牢な ETL およびデータ管理機能に加え、マルチタッチのバッチ駆動型マーケティングプログラムを作成するための強力なオーケストレーションエンジンを備えています。

また、拡張性の高いリアルタイムメッセージングサーバも含まれており、外部システムから完全なペイロードを受け取り、すぐに配信できるようにすることで、パスワードのリセット、注文の確認、電子領収書などのトランザクション通信を可能にします。

## ユースケース

>[!BEGINTABS]

>[!TAB  キャンペーンのバッチ実行 ]

- メール、SMS、ダイレクトメールにわたる大規模でスケジュールに沿ったマーケティングキャンペーンを設計して配信します。
- 複雑なセグメント化とターゲティングを備えた、プロモーションのバースト、ニュースレター、季節ごとのオファーに最適です。

>[!TAB  マルチタッチオーケストレーション ]

- 定義済みのマーケティングジャーニーを通じて顧客をガイドする、複数の手順を備えたマルチチャネルプログラムを作成します。
- オーディエンスの再入力、条件付きロジックおよび時間ベースのトランジションをサポートします。

>[!TAB  データ管理および ETL]

- 様々なソースから顧客データを取り込み、変換および管理して、正確なターゲティングをサポートします。
- カスタムスキーマ、計算フィールドおよびオーディエンス定義の作成を有効にします。

>[!TAB  トランザクションメッセージ ]

- 外部システムによってトリガーされた、事前定義されたリアルタイムのメッセージ（パスワードのリセット、注文の確認、電子領収書など）を送信します。
- IT システムからフルペイロードを受け入れて即時に配信できる、スケーラブルなメッセージングサーバーを使用します。

>[!ENDTABS]

<br>

## アーキテクチャ図

[Campaign v8 デプロイメントモデル &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/config/architecture/architecture.html?lang=ja#ac-deployment){target="_blank"} の詳細情報。

### Campaign Enterprise （FFDA）デプロイメント

<img src="images/campaign-v8-ffda.svg" alt="Campaign v8 （FFDA）デプロイメントブループリントのリファレンスアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

### Campaign v8 FDA デプロイメント

<img src="images/campaign-v8-fda.svg" alt="Campaign v8 （FDA）ブループリントのリファレンスアーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 統合パターン

| シナリオ | 説明 | 技術上の考慮事項 |
| :-- | :--- | :--- |
| [[!DNL Real-time Customer Data Platform] Adobeを使用  [!DNL Campaign]](rtcdp-and-campaign-v8.md) | Adobe Experience Platformとそのリアルタイム顧客プロファイルおよび一元化されたセグメンテーションツールをAdobe [!DNL Campaign] と共に利用して、パーソナライズされた会話を提供する方法を紹介します | <ul><li>クラウドストレージのファイル交換ワークフローおよびAdobe [!DNL Real-Time CDP] ータ取り込みワークフローを使用した、[!DNL Campaign] からAdobe [!DNL Campaign] へのプロファイルとオーディエンスの共有 </li><li>Adobe [!DNL Real-Time CDP] から [!DNL Campaign] ージに送り返される、お客様の会話からの配信およびインタラクションデータを簡単に共有して、リアルタイム顧客プロファイルを強化し、メッセージキャンペーンに関するクロスチャネルレポートを提供します</li></ul> |
| [[!DNL Journey Optimizer] Adobeを使用  [!DNL Campaign]](ajo-and-campaign-v8.md) | Adobe Journey Optimizerを使用して、リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスを調整する方法や、Adobe [!DNL Campaign] のネイティブなトランザクションメッセージシステムを活用してメッセージを送信する方法を示します | <ul><li>リアルタイムメッセージサーバーを介して 1 時間に最大 100 万件のメッセージを送信可能<li>[!DNL Journey Optimizer] からスロットリングが実行されないので、事前にセールスエンタープライズアーキテクトが技術的な検証を行います。</li><li>意思決定管理は、Campaign v8 へのペイロードではサポートされていません</li></ul> |

<br>

## 前提条件

このブループリントには次の前提条件があります。

### アプリケーションサーバーおよびリアルタイムメッセージングサーバー

- Adobe [!DNL Campaign] クライアントコンソールは、[!DNL Campaign] v8 ソフトウェアとやり取りして使用するために必要です。 これは Windows ベースのクライアントで、標準のインターネットプロトコル（SOAP、HTTP など）を使用します。ソフトウェアの配布、インストール、実行に必要な権限が組織で有効になっていることを確認します。

- IP アドレスの許可リストへの登録：
   - クライアントコンソールへのアクセス時にすべてのユーザーが利用する IP 範囲を識別します。
   - リアルタイムメッセージングサーバーとの通信を許可されるエンタープライズシステムの ID で、許可リストに登録できる IP または範囲が静的に割り当てられていることを確認します。
   - これは、Campaign コントロールパネルで設定および制御できます。
- sFTP キー管理：
   - SSH パブリックキーを Campaign で提供された sFTP で使用できるようにします。これは、Campaign コントロールパネルで設定および制御できます。

### 電子メール

- メッセージ送信に使用するサブドメインを準備します。
- サブドメインは、Adobeに完全にデリゲートするか（推奨）、CNAME を使用してAdobe固有の DNS サーバーを指すことができます（カスタム）。
- Google TXT レコードは、優れた配信品質を確保するためにサブドメインごとに必要です。

### モバイルプッシュ

- モバイルアプリのデプロイ、設定、ビルドを行えるモバイル開発者を用意します。
- アドビは、メッセージペイロードをサーバーに送信するために必要な情報を FCM（Android）および APNS（iOS）から収集する SDK のみを提供しています。モバイルアプリをどのようにコーディング、デプロイ、管理、デバッグする必要があるかは、お客様の責任です。

### Webapps（オプション）

- Campaign がホストする登録解除ページとランディングページに追加のサブドメインをデリゲートできます。
- SSL 証明書が強く推奨されます。

<br>

## ガードレール

### アプリケーションサーバーのサイズ設定

- ストレージは最大 2000 万プロファイルまで拡張でき、最大 1 B のプロファイルまで拡張できる可能性があります。
- Adobe [!DNL Admin Console] を介してユーザーアクセスを設定および制御します。
- [!DNL Campaign] へのデータ読み込みは、バッチファイルを使用して行うことが想定されています。
   - API データの読み込みのサポートは、主にデータベース内のプロファイルや単純なオブジェクトの管理（作成と更新）に使用します。大量のデータの読み込みや、バッチ操作などの操作に向けたものではありません。
   - API を使用したカスタムアプリケーション目的でのデータ読み取りはサポートされていません
   - API を介して読み込まれたデータは、アプリケーションデータベースでステージングされ、1 時間ごとにクラウドデータベースにレプリケートされます
- API 呼び出しの制限が適用されます。 詳しくは、[Adobe Campaignの製品説明 &#x200B;](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"} を参照してください。

### バッチメッセージングサーバーのサイズ設定

- 1 時間あたり最大 2,000 万件のメッセージに対応可能

### リアルタイムメッセージングサーバーのサイズ設定

- 1 時間に最大 100 万件のメッセージを送信可能
- デフォルトでは、2 つのリアルタイムメッセージングサーバーがプロビジョニングされます。最大 8 台のリアルタイムメッセージングサーバーを拡張可能

### SMS 設定

- Campaign には、SMS プロバイダーと統合される機能が用意されています。プロバイダーは、顧客によって調達され、SMS ベースのメッセージを送信するためのキャンペーンと統合されます。
- SMPP プロトコルによるサポート。
- 次の 3 種類の SMS があり、アドビがサポートします。
   - SMS MT （Mobile Terminated）: Adobe [!DNL Campaign] から SMPP プロバイダーを通じて携帯電話に送信される SMS です。
   - SMS MO （Mobile Originated）: モバイルから SMPP プロバイダーを通じてAdobe [!DNL Campaign] に送信される SMS です。
   - SMS SR （ステータスレポート）または DR または DLR （配信確認）: SMS が正常に受信されたことを示す、SMPP プロバイダーを通じてAdobe [!DNL Campaign] にモバイルから送信された再来訪の確認メッセージ。 Adobe [!DNL Campaign] は、メッセージを配信できなかったことを示す SR を（多くの場合エラーの説明と共に）受け取る場合もあります。

<br>

## 実装手順

[Adobe Campaign v8 の実装](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=ja)の入門ガイドを参照してください。

## 関連ドキュメント

- [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja)
- [Campaign v8 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
- [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
- [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)