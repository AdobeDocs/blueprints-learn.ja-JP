---
title: Adobe Campaign v8 ブループリントを使用したJourney Optimizer
description: Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 96%

---

# Journey Optimizer と Adobe Campaign v8 ブループリント

Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します。

<br>

## アーキテクチャ

<img src="assets/ajo-campaign-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>Journey Optimizer と Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を熟慮する必要があります。このルートを進める場合は、Pre-Sales Enterprise Architect と協力し、実装をサポートするために必要な事項を理解する必要があります。

<br>

## 前提条件

### Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーション eventID」フィールドグループを追加します
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします
* Journey Optimizer と Campaign が同じ IMS 組織内でプロビジョニングされています

### Campaign v8

* リアルタイムメッセージングサービス（Message Center）の実行インスタンスは、アドビが管理する Cloud Services がホストする必要があります
* すべてのメッセージの作成は、Campaign インスタンス自体内で行われます。

<br>

## ガードレール

[Journey Optimizer ガードレール製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja)

### その他のJourney Optimizerガードレール

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
   * 認証のサポート：トークン | パスワード | OAuth2
* Adobe Experience Platform や Journey Optimizer の個々のコンポーネントをパッケージ化して、様々なサンドボックス間で移動させることはできません。新しい環境に再実装する必要があります

<br>

### Campaign（v8）

* Message Center の実行インスタンスは、アドビが管理する Cloud Services がホストする必要があります
* メッセージングスループット
   * AC（v8）1 時間あたり最大 1M（パッケージに基づく）
* AC (v8) は、メッセージでの意思決定管理をサポートしていません
* Campaign へのアウトバウンド API コールのスロットリングはありません
* Campaign v8.4 では、Experience Platform で Adobe Campaign Managed Services ソースコネクタを利用して、Campaign の配信およびトラッキングイベントを Experience Platform に同期することができます。詳しくは、ソースコネクタのドキュメントを参照してください。[リンク](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja)

<br>

## 実装の手順

### Adobe Experience Platform

#### スキーマ/データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)。
1. Adobe Campaign broadLog、trackingLog および配信不能アドレステーブル（オプション）用の Experience Event クラスベースのスキーマを作成します。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル/ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. ジャーニー使用状況用のセグメントを作成します。

#### ソース/宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)

### Journey Optimizer

1. Experience Platform データソースを設定し、カスタマージャーニーの開始に使用する profileStreaming データの一部としてキャッシュするフィールドを決定します。このデータは、まず Journey Optimizer 内で設定され、オーケストレーション ID を取得する必要があります。このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます
1. 外部データソースを設定
1. Campaign インスタンス用のカスタムアクションを設定

### Campaign v8

* メッセージテンプレートは、適切なパーソナライズ機能コンテキストを使用して設定する必要があります
* Campaign Standard - トランザクションメッセージログを Experience Platform に書き戻すには、書き出しワークフローを設定する必要があります。最大でも 4 時間ごとに実行することをお勧めします。
* Campaign v8.4 では、Experience Platform で Adobe Campaign Managed Services ソースコネクタを利用して、Campaign の配信およびトラッキングイベントを Experience Platform に同期することができます。詳しくは、ソースコネクタのドキュメントを参照してください。[リンク](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja)

### モバイルプッシュ設定（オプション）

1. Experience Platform Mobile SDK を実装して、プッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます
1. Adobe タグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform Edge Network
   * ID Edge ネットワーク用
   * モバイルコア
1. モバイルアプリデプロイメント用と web デプロイメント用の専用のデータストリームがあることを確認
1. 詳しくは、[Adobe Journey Optimizer Mobile ガイド](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)を参照

   >[!IMPORTANT]
   >Journey Optimizer 経由でリアルタイムの通信を送信し、Campaign 経由でバッチプッシュ通知を送信する場合、Journey Optimizer と Campaign の両方でモバイルトークンを収集する必要が生じる場合があります。Campaign v8 では、プッシュトークンをキャプチャするために Campaign SDK を排他的に使用する必要があります。

<br>

## 関連ドキュメント

* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja)
