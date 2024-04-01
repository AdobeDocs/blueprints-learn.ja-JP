---
title: Journey Optimizer と Adobe Campaign v8 ブループリント
description: Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Journey Optimizer, Campaign, Campaign v8 Client Console
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 64%

---

# Journey Optimizer と Adobe Campaign v8 ブループリント

Adobe [!DNL Journey Optimizer] Adobe [!DNL Campaign] リアルタイムメッセージングサーバーを使用して、メッセージをネイティブに送信するには、 [!DNL Campaign].

## アーキテクチャ

<img src="assets/ajo-campaign-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>Journey Optimizer と Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を熟慮する必要があります。このルートを進める場合は、Pre-Sales Enterprise Architect と協力し、実装をサポートするために必要な事項を理解する必要があります。

## 前提条件

各アプリケーションに関する次の前提条件を確認します。

### Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーション eventID」フィールドグループを追加します
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします
* Journey Optimizer と Campaign が同じ IMS 組織内でプロビジョニングされています

### Campaign v8

* リアルタイムメッセージングサービス（Message Center）の実行インスタンスは、アドビが管理する Cloud Services がホストする必要があります
* すべてのメッセージの作成は、Campaign インスタンス自体内で行われます。

## ガードレール

* [Journey Optimizer Guardrails の製品制限](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja)

* [Guardrail とエンドツーエンドの待ち時間のガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 実装手順

以下で説明する各アプリケーションの実装に従います。

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)。
1. （オプション） Adobe Campaign broadLog、trackingLog および配信不能アドレステーブル用に、Experience Event クラスベースのスキーマを作成します。
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

1. [データの取り込み先 [!DNL Experience Platform]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja) ストリーミング API とソースコネクタの使用

### Journey Optimizer

1. を設定します。 [!DNL Experience Platform] データソースを作成し、カスタマージャーニーの開始に使用する profileStreaming データの一部としてキャッシュする必要があるフィールドを決定します。まず、オーケストレーション ID を取得するために、Journey Optimizer内で設定する必要があります。 このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます。
1. 外部データソースを設定します。
1. Campaign インスタンスのカスタムアクションを設定します。

### Campaign v8

* メッセージテンプレートは、適切なパーソナライゼーションコンテキストを使用して設定する必要があります。
* の場合 [!DNL Campaign] 標準：書き出しワークフローは、トランザクションメッセージログをExperience Platformに書き出すように設定する必要があります。 最大で 4 時間おきに実行することをお勧めします。
* の場合 [!DNL Campaign] v8.4ADOBE [!DNL Campaign] Managed Services Source Connector をExperience Platformして、Campaign の配信およびトラッキングイベントをExperience Platformに同期します。 詳しくは、 [ソースコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja) ドキュメントを参照してください。

### モバイルプッシュ設定（オプション）

1. 実装方法 [!DNL Experience Platform] プッシュトークンおよびログイン情報を収集し、既知の顧客プロファイルに結び付ける Mobile SDK。
1. Adobe タグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe [!DNL Journey Optimizer] | Adobe [!DNL Campaign Classic] | Adobe [!DNL Campaign Standard]
   * Adobe [!DNL Experience Platform] [!DNL Edge Network]
   * の ID [!DNL Edge Network]
   * モバイルコア
1. モバイルアプリデプロイメントと Web デプロイメント用の専用のデータストリームがあることを確認します。
1. 詳しくは、 [Adobe Journey Optimizer Mobile ガイド](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer).

   >[!IMPORTANT]
   >Journey Optimizer 経由でリアルタイムの通信を送信し、Campaign 経由でバッチプッシュ通知を送信する場合、Journey Optimizer と Campaign の両方でモバイルトークンを収集する必要が生じる場合があります。Campaign v8 では、プッシュトークンをキャプチャするために Campaign SDK を排他的に使用する必要があります。

## 関連ドキュメント

* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ja)
