---
title: Journey Optimizer と Adobe Campaign ブループリント
description: Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
source-git-commit: a04bd6fe26c9b67a5bfbe753d734882f30f6c047
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 90%

---

# Journey Optimizer と Adobe Campaign

Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します。

<br>

## アーキテクチャ

<img src="assets/ajo-campaign-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>Journey Optimizer と Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を熟慮する必要があります。このルートを進める場合は、Pre-Sales Enterprise Architect と協力し、実装をサポートするために必要な事項を理解する必要があります。

<br>

## 前提条件

### Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります。
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、を追加します エクスペリエンスイベントクラスベースのスキーマでは、ルールベースのイベントではないイベントをトリガーさせたい場合は「オーケストレーション eventID」フィールドグループを追加します。
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします
* Journey Optimizer と Campaign が同じ IMS 組織内でプロビジョニングされています

### Campaign v7/v8 または Campaign Standard

* リアルタイムメッセージングサービス (Message Center) の実行インスタンスは、アドビが管理する Cloud Services がホストする必要があります
* すべてのメッセージの作成は、Campaign インスタンス自体内でおこなわれます

<br>

## ガードレール

[Journey Optimizer ガードレール製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja)

### その他の Journey Optimizer ガードレール

* キャッピングは、宛先システムが障害点で飽和しないようにするために、今日では API を通じて利用できます。これは、キャップを超過したメッセージが完全にドロップされ、まったく送信されないことを意味します。スロットリングは、サポートされていません。
   * 最大接続数：宛先が処理できる http/s 接続の最大数
   * 最大呼び出し数：periodInMs パラメーターで行われる呼び出しの最大数
   * periodInMs：ミリ秒単位の時間
* セグメントメンバーシップで開始されるジャーニーは、2 つのモードで操作できます。
   * バッチセグメント（24 時間ごとに更新）
   * ストリーミングセグメント（5 分未満での認定）
* バッチセグメント - 認定ユーザーの毎日のボリュームを確実に把握し、宛先システムがジャーニーごと、およびすべてのジャーニーのバーストスループットを処理するために必要です
* ストリーミングセグメント - ジャーニーごと、およびすべてのジャーニーの毎日のストリーミング認定ボリュームと共に、プロファイル認定の最初のバーストを処理するために必要です
* 意思決定管理はサポートされていません
* ビジネスイベントはサポートされていません
* サードパーティシステムへのアウトバウンド統合
   * インフラはマルチテナントであるため、単一の静的 IP をサポートしていません（すべてのデータセンター IP を許可リストに含める必要があります）
   * カスタムアクションは POST メソッドと PUT メソッドのみ対応
   * 認証のサポート：トークン｜パスワード｜OAuth2
* Adobe Experience Platform や Journey Optimizer の個々のコンポーネントをパッケージ化して、様々なサンドボックス間で移動させることはできません。新しい環境に再実装する必要があります

<br>

### Campaign（v7/v8）

* Message Center の実行インスタンスは、アドビが管理する Cloud Services がホストする必要がある
* v7 ビルドが 21.1 より上か v8 のどちらかである必要があります
* メッセージングスループット
   * AC（v7）1 時間あたり 50k
   * AC（v8）1 時間あたり最大 1M（パッケージに基づく）
* AC（v7）は、イベントが開始したジャーニーのみ、サポートします。
   * 開始されたセグメントまたはセグメントメンバーシップが開始したジャーニーがありません
   * Audience の読み込みとビジネスイベントベースのジャーニーは、実行インスタンスに送信できる量が多いため、サポートされていません
* AC（v7）も AC（v8）も、メッセージの 意思決定管理 をサポートしていません
* Campaign へのアウトバウンド API コールのスロットリングはありません
* Campaign v8.4 では、Experience PlatformでAdobe Campaign Managed Services Source Connector を利用して、Campaign の配信およびトラッキングイベントをExperience Platformに同期できます。 詳しくは、ソースコネクタのドキュメントを参照してください。 [リンク](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html)

<br>

### Campaign Standard

* スループットで 14 tps（1 時間あたり 50,000）をサポート
* イベントが開始したジャーニーのみ、サポートします。
   * 開始されたセグメントまたはセグメントメンバーシップが開始したジャーニーがありません
   * Audience の読み込みとビジネスイベントベースのジャーニーは、実行インスタンスに送信できる量が多いため、サポートされていません
* Campaign Standard に送信されたトランザクションメッセージから「開く」アクティビティと「クリックア」クティビティは、Journey Optimizer ジャーニーキャンバス内で「再アクションイベント」としてネイティブに公開されます。
* トランザクションメッセージログは、Experience Platform には、逆方向でネイティブ同期されません。コンサルティングの取り組みが必要です。最大 4 時間ごとにログを書き出すことを推奨

<br>

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)。
1. Adobe Campaign broadLog、trackingLog および配信不能アドレステーブル（オプション）用の Experience Event クラスベースのスキーマを作成します。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL Real-Time Customer Profile] の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. ジャーニー使用状況用のセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)

### Journey Optimizer

1. Experience Platform データソースを設定し、カスタマージャーニーの開始に使用する profileStreaming データの一部としてキャッシュするフィールドを決定します。このデータは、まず Journey Optimizer 内で設定され、オーケストレーションIDを取得する必要があります。このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます
1. 外部データソースを設定
1. Campaign インスタンス用のカスタムアクションを設定

### Campaign v7/v8 または Campaign Standard

* メッセージテンプレートは、適切なパーソナライズ機能コンテキストを使用して設定する必要があります
* Campaign Standard の場合：エクスポートワークフローは、トランザクションメッセージログをExperience Platformにエクスポートするように設定する必要があります。 最大で 4 時間ごとに実行することをお勧めします。
* Campaign v8.4 では、Experience PlatformでAdobe Campaign Managed Services Source Connector を利用して、Campaign の配信およびトラッキングイベントをExperience Platformに同期できます。 詳しくは、ソースコネクタのドキュメントを参照してください。 [リンク](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html)

### モバイルプッシュ設定（オプション）

1. Experience Platform Mobile SDK を実装して、プッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます
1. Adobe タグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform Edge Network
   * IDEdge ネットワーク用
   * モバイルコア
1. モバイルアプリデプロイメント用と Web デプロイメント用の専用のデータストリームがあることを確認
1. 詳しくは、 [Adobe Journey Optimizer Mobile ガイド](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer) を参照

   >[!IMPORTANT]
   >Journey Optimizer 経由でリアルタイムの通信を送信し、Campaign 経由でバッチプッシュ通知を送信する場合、Journey Optimizer と Campaign の両方でモバイルトークンを収集する必要が生じる場合があります。Campaign v8 では、プッシュトークンをキャプチャするために Campaign SDK を排他的に使用する必要があります。

<br>

## 関連ドキュメント

* [Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja)
* [Campaign v7 ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign Standard ドキュメント](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
