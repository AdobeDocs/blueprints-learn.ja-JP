---
title: トリガーされたメッセージングとAdobe Experience PlatformのBlueprint
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされたメッセージとエクスペリエンスを実行します。
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 81%

---

# トリガーされたメッセージングとAdobe Experience PlatformのBlueprint

ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされたメッセージとエクスペリエンスを実行します。

## ユースケース

* トリガーされるメッセージ
* 登録確認
* 買い物かごおよび申請フォームの破棄
* 場所でトリガーされるメッセージ

## 構造

<img src="assets/triggered.svg" alt="トリガーされたメッセージングとAdobe Experience PlatformのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## 統合パターン

* Adobe Experience Platform → Journey Orchestration

## 前提条件

* Adobe Experience Platform
* Journey Orchestration

## ガードレール

### Journey Orchestration

* 制限について詳しくは、[リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja#starting-with-journeys)を参照してください
* キャッピングは、宛先システムが障害点で飽和しないようにするために、API セットアップを通じて利用できます。キャッピングとは、キャップを超過したメッセージが完全にドロップされ、まったく送信されないことを意味します。スロットリングは、まだサポートされていません。
   * 最大接続数：宛先が処理できる http/s 接続の最大数
   * 最大呼び出し数：periodInMs パラメーターで行われる呼び出しの最大数
   * periodInMs：ミリ秒単位の時間
* セグメントメンバーシップで開始されるジャーニーは、2 つのモードで操作できます。
   * バッチセグメント（24 時間ごとに更新）
   * ストリーミングセグメント（5 分未満での認定）
* バッチセグメント：認定ユーザーの毎日のボリュームを確実に把握し、宛先システムがジャーニーごと、およびすべてのジャーニーのバーストスループットを処理できるようにします
* ストリーミングセグメント：ジャーニーごと、およびすべてのジャーニーの毎日のストリーミング認定ボリュームと共に、プロファイル認定の最初のバーストを処理できるようにします
* 最終的な宛先は、REST API および JSON ペイロードをサポートする必要があります
* 現在、Offer Decisioning はサポートしていません
* [Experience Platform のプロファイルおよびデータ取り込みのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)を参照してください

### Adobe Campaign Standard

* スループットで 14 tps（1 時間あたり 50k）のみサポート可能
* セグメントメンバーシップで開始されるジャーニーはサポートされていません
* トランザクションメッセージ開く／クリックに対する反応イベントは、Journey Orchestration 内でサポートされます。
* トランザクションメッセージログは、現在、ネイティブでは Experience Platform に同期されず、手動設定が必要です。最大でも 4 時間ごとにログを書き出すことをお勧めします。


## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づいて、Experience Platform で個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します。
1. 次のAdobe Campaignスキーマを作成します。broadLog、trackingLog、配信不能アドレス、プロファイル環境設定（オプション）。
1. ガバナンス用に、データセットにデータ使用ラベルを追加します。
1. ポリシーを作成して、宛先のガバナンスを実施します。

#### プロファイル／ID

1. 任意の顧客専用の名前空間を作成します。
1. スキーマに ID を追加します。
1. プロファイル用のスキーマおよびデータセットを有効にします。
1. 異なる表示の[!UICONTROL リアルタイム顧客プロファイル]（オプション）にマージルールを設定します。
1. Adobe Campaignに使用するセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、Experience Platform にデータを取り込みます。
1. Adobe Campaignで使用する[!DNL Azure] BLOBストレージ先を構成します。

#### モバイルアプリデプロイメント

1. Adobe Campaign Classic向けAdobe CampaignSDKまたはAdobe Campaign Standard向けExperience PlatformSDKを実装します。 Experience Platform Launchが存在する場合は、Experience PlatformSDKでAdobe Campaign ClassicまたはAdobe Campaign Standardの拡張機能を使用することをお勧めします。


### Journey Orchestration

1. カスタマージャーニーを開始するために使用されるストリーミングデータは、最初に Journey Orchestration 内で設定して、オーケストレーション ID を取得する必要があります。このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます。
1. 外部データソースを設定します。
1. カスタムアクションを設定します。

### Adobe Campaign Standard

1. 適切なパーソナライズ設定でメッセージングテンプレートを設定します。
1. エクスポートワークフローを設定して、トランザクションメッセージログをエクスポートします。最大でも 4 時間ごとに実行することをお勧めします。


## 関連ドキュメント

* [Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Journey Orchestration ドキュメント](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=ja)
* [Adobe Campaign Classic文書](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Adobe Campaign Standard文書](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
* [Experience Platform Launch ドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
