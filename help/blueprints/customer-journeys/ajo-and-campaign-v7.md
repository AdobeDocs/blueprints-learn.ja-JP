---
title: Journey Optimizer と Adobe Campaign v7 ブループリント
description: Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Journey Optimizer, Campaign, Campaign Classic v7, Campaign Standard
exl-id: 6d9bc65c-cca0-453f-8106-d2895d005ada
source-git-commit: 7547cdc57e50d63f4a7949c00a77b82c86da831e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 97%

---

# Journey Optimizer と Adobe Campaign v7 ブループリント

Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します。

<br>

## アーキテクチャ

<img src="assets/ajo-campaign-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>Journey Optimizer と Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を熟慮する必要があります。このルートを進める場合は、Pre-Sales Enterprise Architect と協力し、実装をサポートするために必要な事項を理解する必要があります。

<br>

## 前提条件

### Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーション eventID」フィールドグループを追加します
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします
* Journey Optimizer と Campaign が同じ IMS 組織内でプロビジョニングされています

### Campaign v7

* リアルタイムメッセージングサービス（Message Center）の実行インスタンスは、アドビが管理する Cloud Services がホストする必要があります
* すべてのメッセージの作成は、Campaign インスタンス自体内で行われます。

<br>

## ガードレール

[Journey Optimizer ガードレール製品リンク](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)

[ ガードレールとエンドツーエンドの待ち時間のガイダンス ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=ja)

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?lang=ja&recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)。
1. Adobe Campaign broadLog、trackingLog および配信不能アドレステーブル（オプション）用の Experience Event クラスベースのスキーマを作成します。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. ジャーニー使用状況用のセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?lang=ja&recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)

### Journey Optimizer

1. Experience Platform データソースを設定し、カスタマージャーニーの開始に使用する profileStreaming データの一部としてキャッシュするフィールドを決定します。このデータは、まず Journey Optimizer 内で設定され、オーケストレーション ID を取得する必要があります。このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます
1. 外部データソースを設定
1. Campaign インスタンス用のカスタムアクションを設定

### Campaign v7

* メッセージテンプレートは、適切なパーソナライズ機能コンテキストを使用して設定する必要があります
* Campaign v7 - トランザクションメッセージログを Experience Platform に書き戻すには、書き出しワークフローを設定する必要があります。最大でも 4 時間ごとに実行することをお勧めします。

### モバイルプッシュ設定（オプション）

1. Experience Platform Mobile SDK を実装して、プッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます
1. Adobe タグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe Journey Optimizer | Adobe Campaign Classic | Adobe Campaign Standard
   * Adobe Experience Platform [!DNL Edge Network]
   * [!DNL Edge Network] の ID
   * モバイルコア
1. モバイルアプリデプロイメント用と web デプロイメント用の専用のデータストリームがあることを確認
1. 詳しくは、[Adobe Journey Optimizer Mobile ガイド](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer/push-notification/)を参照

   >[!IMPORTANT]
   >Journey Optimizer 経由でリアルタイムの通信を送信し、Campaign 経由でバッチプッシュ通知を送信する場合、Journey Optimizer と Campaign の両方でモバイルトークンを収集する必要が生じる場合があります。Campaign v8 では、プッシュトークンをキャプチャするために Campaign SDK を排他的に使用する必要があります。

<br>

## 関連ドキュメント

* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v7 ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
