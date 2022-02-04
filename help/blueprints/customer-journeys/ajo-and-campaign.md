---
title: Journey OptimizerとAdobe Campaignブループリント
description: Adobe Journey OptimizerをAdobe Campaignで使用して、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Experience Platform, Journey Optimizer, Campaign v8, Campaign Classic v7, Campaign Standard
source-git-commit: 1c46cbdfc395de4fc9139966cf869ba1feeceaaa
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 25%

---

# Journey OptimizerとAdobe Campaign

Adobe Journey OptimizerをAdobe Campaignと共に使用して、Campaign のリアルタイムメッセージングサーバーを利用してメッセージをネイティブに送信する方法を示します。

<br>

## アーキテクチャ

<img src="assets/ajo-campaign-architecture.svg" alt="参照アーキテクチャJourney Optimizerブループリント" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>Journey Optimizerと Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を考慮する必要があります。 このルートを進める場合は、プリセールスエンタープライズアーキテクトと協力し、実装をサポートするために必要な事項を理解していただく必要があります。

<br>

## 前提条件

### Adobe Experience Platform

* スキーマとデータセットは、Journey Optimizerデータソースを設定する前に、システムで設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーションイベント ID 」フィールドグループを追加します
* 個々のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizerで使用するテストプロファイルを読み込めるようにします
* Journey Optimizerと Campaign が同じ IMS 組織でプロビジョニングされている

### Campaign v7/v8 またはCampaign Standard

* リアルタイムメッセージングサービス (Message Center) の実行インスタンスは、Adobe管理Cloud Servicesがホストする必要があります
* すべてのメッセージのオーサリングは、Campaign インスタンス自体内でおこなわれます

<br>

## ガードレール

[Journey Optimizer Guardrails 製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja)

### その他のJourney Optimizer Guardrail

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
* ビジネスイベントはサポートされていません
* サードパーティシステムへのアウトバウンド統合
   * インフラストラクチャはマルチテナントなので、単一の静的 IP はサポートされません ( すべてのデータセンター IP を許可リストする必要があります )
   * カスタムアクションでは、POSTおよびPUTメソッドのみがサポートされます
   * 認証のサポート：トークン |パスワード | OAuth2
* Adobe Experience PlatformまたはJourney Optimizerの個々のコンポーネントを様々なサンドボックス間でパッケージ化および移動する機能はありません。 新しい環境に再実装する必要がある

<br>

### キャンペーン (v7/v8)

* Message Center の実行インスタンスは、Adobe管理Cloud Servicesでホストする必要がある
* v7 ビルドが 21.1 より上か v8 のどちらかにある必要があります
* メッセージングスループット
   * AC(v7) 50k/時
   * AC (v8) 1 時間あたり最大 1M（パッケージに基づく）
* AC(v7) は、イベントが開始したジャーニーの
   * 開始されたセグメントまたはセグメントメンバーシップのジャーニーがありません
   * オーディエンスおよびビジネスイベントベースの読み取りのジャーニーは、実行インスタンスに送信できるボリュームが原因でサポートされていません
* AC(v7) も AC(v8) も、メッセージのOffer decisioningをサポートしていません
* Campaign に対して送信 API 呼び出しのスロットルが行われていない
* トランザクションメッセージログは、AEP とネイティブに同期されていません。 コンサルティングの取り組みが必要です。 最大 4 時間ごとにログを書き出すことを推奨

<br>

### Campaign Standard

* スループットで 14 時間（1 時間あたり 50,000）をサポート
* イベントが開始されたジャーニーのみをサポート
   * 開始されたセグメントまたはセグメントメンバーシップのジャーニーがありません
   * オーディエンスおよびビジネスイベントベースの読み取りのジャーニーは、実行インスタンスに送信できるボリュームが原因でサポートされていません
* Campaign Standardに送信されたトランザクションメッセージから開いたアクティビティとクリックアクティビティは、Journey Optimizerジャーニーキャンバス内に「再アクションイベント」としてネイティブに公開されます。
* トランザクションメッセージログがネイティブ同期されず、Experience Platformに戻る。 コンサルティングの取り組みが必要です。 最大 4 時間ごとにログを書き出すことを推奨

<br>

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)。
1. Adobe Campaign broadLog、trackingLog および配信不能アドレステーブル用の Experience Event クラスベースのスキーマを作成します（オプション）。
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
1. Campaign インスタンスのカスタムアクションの設定

### Campaign v7/v8 またはCampaign Standard

* メッセージテンプレートは、適切なパーソナライゼーションコンテキストを使用して設定する必要があります
* トランザクションメッセージログをExperience Platformに書き出すには、書き出しワークフローを設定する必要があります。 最大 4 時間ごとに実行することをお勧めします

### モバイルプッシュ設定（オプション）

1. Experience PlatformMobile SDK を実装して、プッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます。
1. Adobeタグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform Edge Network
   * ID （Edge ネットワーク用）
   * モバイルコア
1. モバイルアプリデプロイメント用と Web デプロイメント用の専用のデータストリームがあることを確認します。
1. 詳しくは、 [Adobe Journey Optimizer Mobile ガイド](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

   >[!IMPORTANT]
   >Journey Optimizer経由でリアルタイムの通信を送信し、Campaign 経由でバッチプッシュ通知を送信する場合は、Journey Optimizerと Campaign の両方でモバイルトークンを収集する必要が生じる場合があります。 Campaign v8 では、プッシュトークンをキャプチャするために Campaign SDK を排他的に使用する必要があります。

<br>

## 関連ドキュメント

* [Experience Platform文書](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Campaign v7 ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign Standard ドキュメント](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)