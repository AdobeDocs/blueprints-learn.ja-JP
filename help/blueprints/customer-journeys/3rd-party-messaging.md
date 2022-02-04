---
title: Journey Optimizer — サードパーティのメッセージングブループリント
description: Adobe Journey Optimizerをサードパーティのメッセージングシステムと共に使用して、パーソナライズされた通信を調整および送信する方法を示します。
solution: Experience Platform, Journey Optimizer
hidefromtoc: true
exl-id: 57e4d90a-61c9-444d-9bc5-40c7e58b4d21
source-git-commit: 13f750c0ff820ab01ed4fc615aba864bc2dc7b75
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# サードパーティのメッセージ

Adobe Journey Optimizerをサードパーティのメッセージングシステムと共に使用して、パーソナライズされた通信を調整および送信する方法を示します。

<br>

## アーキテクチャ

<img src="assets/3rd-party-messaging-architecture.svg" alt="参照アーキテクチャJourney Optimizerブループリント" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 前提条件

Adobe Experience Platform

* スキーマとデータセットは、Journey Optimizerデータソースを設定する前に、システムで設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーションイベント ID 」フィールドグループを追加します
* 個々のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizerで使用するテストプロファイルを読み込めるようにします

サードパーティのメッセージングアプリケーション

* トランザクションペイロードを送信するには REST API 呼び出しをサポートする必要がある

<br>

## ガードレール

[Journey Optimizer Guardrails 製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja)

その他のJourney Optimizer Guardrail:

* 現時点では、宛先システムで障害が発生した時点まで飽和しないように、API を介してキャッピングが使用できます。 つまり、上限を超えたメッセージは完全に破棄され、送信されなくなります。 スロットルはサポートされていません。
   * 最大接続数 — 宛先で処理できる http/s 接続の最大数
   * 最大呼び出し数 — periodInMs パラメーターで実行する呼び出しの最大数
   * periodInMs — 時間（ミリ秒）
* セグメントメンバーシップで開始されるジャーニーは、2 つのモードで操作できます。
   * バッチセグメント（24 時間ごとに更新）
   * ストリーミングセグメント（5 分未満の認定）
* バッチセグメント - 認定ユーザーの毎日のボリュームを確実に把握し、宛先システムがジャーニーごと、およびすべてのジャーニーのバーストスループットを処理するために必要です
* ストリーミングセグメント - ジャーニーごと、およびすべてのジャーニーの毎日のストリーミング認定ボリュームと共に、プロファイル認定の最初のバーストを処理するために必要です
* offer decisioningはサポートされていません
* サードパーティシステムへのアウトバウンド統合
   * インフラストラクチャはマルチテナントなので、単一の静的 IP はサポートされません ( すべてのデータセンター IP を許可リストする必要があります )
   * カスタムアクションでは、POSTおよびPUTメソッドのみがサポートされます
   * 認証のサポート：トークン |パスワード | OAuth2
* Adobe Experience PlatformまたはJourney Optimizerの個々のコンポーネントを様々なサンドボックス間でパッケージ化および移動する機能はありません。 新しい環境に再実装する必要がある

<br>

サードパーティのメッセージングシステム

* トランザクション API 呼び出しでシステムがサポートできる読み込みを理解する必要がある
   * 1 秒あたりに許可される呼び出し数
   * 接続数
* API 呼び出しをおこなうために必要な認証を理解する必要がある
   * 認証タイプ：  トークン |パスワード | OAuth2 はJourney Optimizer経由でサポートされます
   * 認証キャッシュの期間：  トークンの有効期間はどれくらいですか？ 
* バッチ取り込みのみがサポートされている場合は、Amazon Kinesisまたは Azure Event Grid 1st などのクラウドストレージエンジンにストリーミングする必要があります。
   * データは、これらのクラウドストレージエンジンのバッチ処理を行い、サードパーティに送り込むことができます
   * 必要なミドルウェアは、お客様またはサードパーティが提供する責任を負います

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

1. Experience Platformデータソースを設定し、カスタマージャーニーの開始に使用する profileStreaming データの一部としてキャッシュするフィールドを決定します。オーケストレーション ID を取得するには、まずJourney Optimizer内で設定する必要があります。 次に、このオーケストレーション ID が、取り込みで使用するために開発者に提供されます
1. 外部データソースの設定
1. サードパーティアプリケーションのカスタムアクションの設定

### モバイルプッシュ設定（オプションでサードパーティがトークンを収集する場合があります）

1. Experience PlatformMobile SDK を実装して、プッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます。
1. Adobeタグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * ID （Edge ネットワーク用）
   * モバイルコア
1. モバイルアプリデプロイメント用と Web デプロイメント用の専用のデータストリームがあることを確認します。
1. 詳しくは、 [Adobe Journey Optimizer Mobile ガイド](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

<br>

## 関連ドキュメント

* [Experience Platform文書](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
