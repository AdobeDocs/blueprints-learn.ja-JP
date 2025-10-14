---
title: Journey Optimizer と Adobe Campaign v8 ブループリント
description: Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Journey Optimizer, Campaign, Campaign v8, Campaign v8 Client Console
version: Campaign v8, Campaign v8 Client Console
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 6ec61ae7e1cfe3bad7beff127dc2e80873424d53
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 52%

---

# Journey Optimizer と Adobe Campaign v8 ブループリント

Adobe [!DNL Journey Optimizer] をAdobe [!DNL Campaign] と共にネイティブに使用し、[!DNL Campaign] のリアルタイムメッセージサーバーを利用してメッセージを送信する方法を示します。

## アーキテクチャ

<img src="images/ajo-campaign-v8-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>Journey Optimizer と Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を熟慮する必要があります。このルートを追求する場合は、プリセールスのエンタープライズアーキテクトと協力して、実装をサポートするために必要な事項を確実に理解するようにしてください

<br>

## 前提条件

各アプリケーションについて、次の前提条件を確認してください。

### Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーするには、「オーケストレーション eventID」フィールドグループを追加します
* 個々のプロファイルクラスベースのスキーマの場合は、「プロファイルテストの詳細」フィールドグループを追加して、Journey Optimizerで使用するテストプロファイルを読み込むことができます
* Journey Optimizer と Campaign が同じ IMS 組織内でプロビジョニングされています

### Campaign v8

* Adobe Managed Cloud Services は、リアルタイムメッセージサービス（Message Center など）の実行インスタンスをホストしている必要があります
* すべてのメッセージの作成は、Campaign インスタンス自体内で行われます。

## ガードレール

* [Journey Optimizer ガードレール製品の制限 &#x200B;](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)

* [&#x200B; ガードレールとエンドツーエンドの待ち時間ガイダンス &#x200B;](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=ja)

## 実装手順

以下に説明する各アプリケーションの実装に従います。

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=ja)。
1. （任意）Adobe Campaign broadLog、trackingLog および配信不能アドレステーブル用に、エクスペリエンスイベントクラスベースのスキーマを作成します。
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

1. ストリーミング API とソースコネクタを使用した [&#x200B; データの取り込み  [!DNL Experience Platform]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=ja)。

### Journey Optimizer

1. [!DNL Experience Platform] データソースを設定し、キャッシュするフィールドを決定します
1. カスタマージャーニーを開始するために使用されるストリーミングデータは、最初に Journey Optimizer 内で設定して、オーケストレーション ID を取得する必要があります。このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます。
1. 外部データソースを設定します。
1. Campaign インスタンスのカスタムアクションを設定します。

### Campaign v8

* メッセージテンプレートは、適切なパーソナライゼーションコンテキストで設定する必要があります。
* 標準 [!DNL Campaign] 場合：トランザクションメッセージログをExperience Platformにエクスポートするようにエクスポートワークフローを設定する必要があります。 最大 4 時間ごとに実行することをお勧めします。
* [!DNL Campaign] v8.4 では、Experience PlatformのAdobe [!DNL Campaign] Managed Services Source コネクタを利用して、Campaign からの配信イベントとトラッキングイベントをExperience Platformに同期することができます。 詳しくは、[Source コネクタ &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja) ドキュメントを参照してください。

### モバイルプッシュ設定（オプション）

1. [!DNL Experience Platform] Mobile SDKを実装してプッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます。
1. Adobe タグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe [!DNL Journey Optimizer] |Adobe[!DNL Campaign Classic] |Adobe[!DNL Campaign Standard]
   * Adobe [!DNL Experience Platform] [!DNL Edge Network]
   * [!DNL Edge Network] の ID
   * モバイルコア
1. Web デプロイメントではなく、モバイルアプリのデプロイメントに専用のデータストリームがあることを確認します。
1. 詳しくは、[Adobe Journey Optimizer モバイルガイド &#x200B;](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer/push-notification/) を参照してください。

   >[!IMPORTANT]
   >Journey Optimizer 経由でリアルタイムの通信を送信し、Campaign 経由でバッチプッシュ通知を送信する場合、Journey Optimizer と Campaign の両方でモバイルトークンを収集する必要が生じる場合があります。Campaign v8 では、プッシュトークンをキャプチャするために Campaign SDK を排他的に使用する必要があります。

## 関連ドキュメント

* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja)
