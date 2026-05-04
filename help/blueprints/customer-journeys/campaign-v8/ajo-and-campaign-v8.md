---
title: Journey Optimizer と Adobe Campaign v8 ブループリント
description: Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Journey Optimizer, Campaign, Campaign v8, Campaign v8 Client Console
version: Campaign v8, Campaign v8 Client Console
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
TQID: https://experienceleague.adobe.com/EWmi1DKRUqfWUqK0u-pfXkdUlzDc6-HjC0i1QqOocpk
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: d556b755-390a-43f0-be32-a08cf6236126
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
subfeature_v2:
  - id: af7571a6-3ddb-4c1c-abdf-4d4dde592140
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 795
ht-degree: 56%

---

# Journey Optimizer と Adobe Campaign v8 ブループリント

[!DNL Campaign]のリアルタイム メッセージング サーバーを利用して、Adobe [!DNL Journey Optimizer]とAdobe [!DNL Campaign]をネイティブに使用してメッセージを送信する方法を示します。

## アーキテクチャ

<img src="images/ajo-campaign-v8-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>Journey Optimizer と Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を熟慮する必要があります。 このルートを進める場合は、プリセールスエンタープライズアーキテクトと協力して、実装をサポートするために必要な内容を確実に把握してください

<br>

## 前提条件

各アプリケーションについて、次の前提条件を確認します。

### Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります
* Experience Event クラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合は、「Orchestration eventID フィールドグループ」を追加します
* 個人プロファイルクラスベースのスキーマの場合は、「プロファイルテストの詳細」フィールドグループを追加して、Journey Optimizerで使用するテストプロファイルを読み込むことができます
* Journey Optimizer と Campaign が同じ IMS 組織内でプロビジョニングされています

### Campaign v8

* Adobe Managed Cloud Servicesは、リアルタイムメッセージングサービス（Message Center）の実行インスタンスをホストしている必要があります
* すべてのメッセージの作成は、Campaign インスタンス自体内で行われます。

## ガードレール

* [Journey Optimizer Guardrails製品の制限事項](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)

* [ガードレールとエンドツーエンドの遅延ガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=ja)

## 実装手順

以下に説明する各アプリケーションの実装に従います。

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=ja)。
1. （オプション）Adobe Campaign broadLog、trackingLog、配信不能アドレステーブルのExperience Event クラスベースのスキーマを作成します。
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

1. ストリーミング APIとソースコネクタを使用して[&#x200B; データを [!DNL Experience Platform]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=ja)に取り込みます。

### Journey Optimizer

1. [!DNL Experience Platform] データソースを設定し、キャッシュするフィールドを決定します
1. カスタマージャーニーを開始するために使用されるストリーミングデータは、最初に Journey Optimizer 内で設定して、オーケストレーション ID を取得する必要があります。 このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます。
1. 外部データソースを設定します。
1. Campaign インスタンスのカスタムアクションを設定します。

### Campaign v8

* メッセージングテンプレートは、適切なパーソナライゼーションコンテキストで設定する必要があります。
* [!DNL Campaign]標準の場合：トランザクションメッセージングログをExperience Platformに書き出すように、書き出しワークフローを設定する必要があります。 推奨は、最大4時間ごとに実行することです。
* [!DNL Campaign] v8.4では、Experience PlatformのAdobe [!DNL Campaign] Managed Services Source Connectorを活用して、CampaignからExperience Platformに配信およびトラッキングイベントを同期できます。 詳しくは、[Source コネクタ &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja) ドキュメントを参照してください。

### モバイルプッシュ設定（オプション）

1. [!DNL Experience Platform] Mobile SDKを実装してプッシュトークンとログイン情報を収集し、既知の顧客プロファイルに関連付けます。
1. Adobe タグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe [!DNL Journey Optimizer] | Adobe [!DNL Campaign Classic] | Adobe [!DNL Campaign Standard]
   * Adobe [!DNL Experience Platform] [!DNL Edge Network]
   * [!DNL Edge Network]のID
   * モバイルコア
1. モバイルアプリのデプロイメントとweb デプロイメント用の専用データストリームがあることを確認します。
1. 詳しくは、[Adobe Journey Optimizer モバイルガイド &#x200B;](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer/push-notification/)を参照してください。

   >[!IMPORTANT]
   >Journey Optimizer 経由でリアルタイムの通信を送信し、Campaign 経由でバッチプッシュ通知を送信する場合、Journey Optimizer と Campaign の両方でモバイルトークンを収集する必要が生じる場合があります。 Campaign v8 では、プッシュトークンをキャプチャするために Campaign SDK を排他的に使用する必要があります。

## 関連ドキュメント

* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizerの製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja)
