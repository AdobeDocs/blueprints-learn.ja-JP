---
title: Journey Optimizer - サードパーティメッセージングのブループリント
description: Adobe Journey Optimizerをサードパーティのメッセージングシステムと共に使用して、パーソナライズされたコミュニケーションを送信する方法を示します。
solution: Journey Optimizer
source-git-commit: 8284380fb9202991f3da7d755225da2e38a50cac
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 62%

---

# サードパーティメッセージングのブループリント

Adobe Journey Optimizerをサードパーティのメッセージングシステムと共に使用して、パーソナライズされたコミュニケーションを送信する方法を示します。

<br>

## アーキテクチャ

<img src="/help/blueprints/customer-journeys/journey-optimizer/images/3rd-party-messaging-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 前提条件

**Adobe Experience Platform**

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります
* Experience Event クラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合は、「Orchestration eventID フィールドグループ」を追加します
* 個人プロファイルクラスベースのスキーマの場合は、「プロファイルテストの詳細」フィールドグループを追加して、Journey Optimizerで使用するテストプロファイルを読み込むことができます

**サードパーティのメッセージング アプリケーション**

* トランザクションペイロードを送信するには REST API 呼び出しをサポートする必要があります

<br>

## ガードレール

[Journey Optimizer Guardrails製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[ガードレールとエンドツーエンドのレイテンシーガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html)

<br>

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. お客様から提供されたデータに基づいて、Experience Platformで[ スキーマ ](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=ja)を設定します。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/ja/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. ジャーニー使用状況用のセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=ja)

### Journey Optimizer

1. Experience Platform データソースを設定し、ジャーニーの一部としてキャッシュするフィールドを決定します
1. カスタマージャーニーの開始に使用されるストリーミングデータは、オーケストレーション IDを取得するには、まず設定する必要があります。 このオーケストレーション IDは、取り込み中に使用するために開発者に提供されます
1. 外部データソースを設定
1. サードパーティアプリケーションのカスタムアクションを設定

### モバイルプッシュ設定（オプションでサードパーティがトークンを収集する場合があります）

1. Experience Platform Mobile SDK を実装して、プッシュトークンとログイン情報を収集し、既知の顧客プロファイルに結び付けます
1. Adobe タグを活用し、次の拡張子を持つモバイルプロパティを作成します。
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * [!DNL Edge Network]のID
   * モバイルコア
1. モバイルアプリデプロイメント用と web デプロイメント用の専用のデータストリームがあることを確認
1. 詳しくは、[Adobe Journey Optimizer Mobile ガイド](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer/)を参照

<br>

## 関連ドキュメント

* [Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Experience Platform Tags ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Platform Mobile SDKのドキュメント](https://experienceleague.adobe.com/docs/mobile.html)
* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
* [Journey Optimizerの製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
