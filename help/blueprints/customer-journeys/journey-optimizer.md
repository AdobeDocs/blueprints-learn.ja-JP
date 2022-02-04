---
title: Journey Optimizer - トリガーされるメッセージおよび Adobe Experience Platform ブループリント
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Experience Platform, Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 2ead62f94e761cd9453be284a9fde3c5803879eb
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 41%

---

# Journey Optimizer

Adobe Journey Optimizer は、マーケティングチームが顧客行動にリアルタイムで反応し、顧客が場所を問わずにアクセスできることを目的に構築されたシステムです。データ管理機能が Adobe Experience Platform に移行したことで、マーケティングチームは、世界最高クラスのカスタマージャーニーと、パーソナライズされたやり取りを生み出すことに全力で取り組むことができます。このブループリントは、アプリケーションの技術的機能の概要を説明し、Adobe Journey Optimizer を構成する様々なアーキテクチャコンポーネントについて深く掘り下げます。

<br>

## ユースケース

* トリガーされるメッセージ
* ようこそと登録の確認
* 買い物かごおよび申請フォームの破棄
* 場所でトリガーされるメッセージ
* 競技場での体験
* 旅行と接客の事前到着および滞在の経験

<br>

## アーキテクチャ

<img src="assets/ajo-architecture.svg" alt="参照アーキテクチャJourney Optimizerブループリント" style="width:100%; border:1px solid #4a4a4a" />

<br>

## ブループリントのシナリオ

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [サードパーティのメッセージ](3rd-party-messaging.md) | Adobe Journey Optimizerをサードパーティのメッセージングシステムと共に使用して、パーソナライズされた通信を調整および送信する方法を示します | ブランドや会社とのやり取りに応じて、パーソナライズされたコミュニケーションを顧客に即座に提供する<br><br>注意点：<br><ul><li>サードパーティシステムは、認証のためにベアラートークンをサポートする必要があります。</li><li>マルチテナントアーキテクチャが原因で静的 IP がサポートされない</li><li>1 秒あたりの API 呼び出しに関しては、サードパーティシステムのアーキテクチャの制約に注意してください。  お客様がJourney Optimizerからのボリュームをサポートするために、サードパーティベンダーから追加のボリュームを購入する必要が生じる場合があります</li><li>メッセージまたはペイロードのOffer decisioningをサポートしていません</li></ul> |

<br>

## 統合パターン

| 統合 | 説明 | 機能 |
| :-- | :--- | :--- |
| [Journey OptimizerとAdobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizerを使用して、リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスの調整をおこない、ネイティブのAdobe Campaignトランザクションメッセージングシステムを活用してメッセージを送信する方法を示します | Adobe Campaignのネイティブリアルタイムメッセージング機能を利用してラストマイル通信を実行しながら、リアルタイム顧客プロファイルとJourney Optimizerの機能を活用して、瞬時のエクスペリエンスで調整<br><br>注意点：<br><ul><li>Campaign アプリケーションは、v7 ビルドが 21.1 より上か v8 のどちらかである必要があります</li><li>メッセージングスループット</li><ul><li>Campaign v7 - 1 時間あたり最大 50,000</li><li>Campaign v8 - 1 時間あたり最大 1M</li><li>Campaign Standard- 1 時間あたり最大 50,000 個</li></ul><li>スロットルは実行されないので、使用例ではエンタープライズアーキテクトによる技術的な検証が必要です</li><li>Campaign から送信されたメッセージのOffer decisioningを利用するサポートはありません</li></ul> |

<br>

## 前提条件

Adobe Experience Platform

* スキーマとデータセットは、Journey Optimizerデータソースを設定する前に、システムで設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーションイベント ID 」フィールドグループを追加します
* 個々のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizerで使用するテストプロファイルを読み込めるようにします

電子メール

* メッセージ送信に使用するサブドメインの準備が整っている必要があります
* サブドメインは、Adobeに完全にデリゲートすることも（推奨）、CNAME を使用してAdobe固有の DNS サーバー（カスタム）を指すこともできます
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要です

モバイルプッシュ

* 顧客は、モバイルデベロッパーを使用してアプリを作成できる必要があります
* Adobe Experience Platform Mobile SDK

<br>

## ガードレール

[Journey Optimizer Guardrails 製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja)

上記のリンクには記載されていないことに注意してください。

* バッチセグメント - 認定ユーザーの毎日のボリュームを確実に把握し、宛先システムがジャーニーごと、およびすべてのジャーニーのバーストスループットを処理するために必要です
* ストリーミングセグメント - ジャーニーごと、およびすべてのジャーニーの毎日のストリーミング認定ボリュームと共に、プロファイル認定の最初のバーストを処理するために必要です
* メッセージでのOffer decisioningのみをネイティブでサポート（カスタムアクションなし）
* サポートされるメッセージタイプ：
   * 電子メール
   * プッシュ（FCM／APNS）
   * カスタムアクション（Rest API を介する）
* サードパーティシステムへのアウトバウンド統合
   * インフラストラクチャはマルチテナントなので、単一の静的 IP はサポートされません ( すべてのデータセンター IP を許可リストする必要があります )
   * カスタムアクションでは、POSTおよびPUTメソッドのみがサポートされます
   * ユーザー/パスまたは認証トークンを使用した認証
* Adobe Experience PlatformまたはJourney Optimizerの個々のコンポーネントを様々なサンドボックス間でパッケージ化および移動する機能はありません。 新しい環境に再実装する必要がある

### データ取り込みガードレール

<img src="assets/aep-data-ingestion-details-latency.svg" alt="参照アーキテクチャJourney Optimizerブループリント" style="width:80%; border:1px solid #4a4a4a" />

<br>

### 有効化ガードレール

<img src="assets/ajo-activation-details-latency.svg" alt="参照アーキテクチャJourney Optimizerブループリント" style="width:80%; border:1px solid #4a4a4a" />

<br>

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)（オプション）。
1. セグメントを作成してジャーニーを使用する。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)

### Journey Optimizer

1. Experience Platformデータソースを設定し、プロファイルの一部としてキャッシュするフィールドを決定します。カスタマージャーニーの開始に使用するストリーミングデータは、オーケストレーション ID を取得するために最初にJourney Optimizer内で設定する必要があります。 次に、このオーケストレーション ID が、取り込みで使用するために開発者に提供されます
1. 外部データソースを設定します。
1. カスタムアクションを設定します。

### モバイルプッシュ設定

1. Experience PlatformMobile SDK を実装して、プッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます。
1. Adobeタグを活用し、次の拡張子を持つモバイルプロパティを作成します。
1. Adobe Journey Optimizer
1. Adobe Experience Platform Edge Network
1. ID （Edge ネットワーク用）
1. モバイルコア
1. モバイルアプリデプロイメント用と Web デプロイメント用の専用のデータストリームがあることを確認します。
1. 詳しくは、 [Adobe Journey Optimizer Mobile ガイド](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)


## 関連ドキュメント

* [Experience Platform文書](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
