---
title: トリガーされたメッセージングとAdobe Experience PlatformのBlueprint
description: Adobe Experience Platformをストリーミングデータ、顧客プロファイル、セグメントの中心として、トリガーされたメッセージとエクスペリエンスを実行します。
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# トリガーされたメッセージングとAdobe Experience PlatformのBlueprint

Adobe Experience Platformをストリーミングデータ、顧客プロファイル、セグメントの中心として、トリガーされたメッセージとエクスペリエンスを実行します。

## 使用例

* トリガーされたメッセージ
* 登録確認
* 買い物かごと申し込みフォームの放棄
* トリガーされた場所のメッセージ

## 建築

<img src="assets/triggered.svg" alt="トリガーされたメッセージングとAdobe Experience PlatformのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## 統合パターン

* Adobe Experience Platform->Journey Orchestration

## 前提条件

* Adobe Experience Platform
* Journey Orchestration

## ガードレール

### Journey Orchestration

* [制限の詳細は](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en#starting-with-journeys)のリンクを参照
* キャッピングは、API設定を通じて使用でき、障害発生時点まで宛先システムの飽和状態が発生しないようにします。 上限を超えたメッセージは完全に破棄され、送信されなくなります。 ジョブ数の制限はまだサポートされていません。
   * 最大接続数：宛先で処理できるHTTP/s接続の最大数
   * 最大呼び出し数：periodInMsパラメーターで実行される最大呼び出し数
   * periodInMs:時間（ミリ秒）
* セグメントメンバーシップ開始ジャーニーは、次の2つのモードで動作できます。
   * バッチセグメント（24時間ごとに更新）
   * ストリーミングセグメント（5分未満の認定）
* バッチセグメント：1日の条件を満たすユーザー数を把握し、対象のシステムがジャーニーごとおよびすべてのジャーニーにわたってバーストスループットを処理できることを確認する
* ストリーミングセグメント：プロファイルの条件の初期バーストを、各ジャーニーおよびすべてのジャーニーで日別のストリーミング認定ボリュームと共に処理できるようにする
* 最終宛先はREST APIおよびJSONペイロードをサポートする必要があります
* 現在、Offer decisioningをサポートしていません
* [Experience Platformのプロファイルとデータ取り込みのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)を参照

### Adobe Campaign Standard

* スループットは14 tps（1時間あたり50,000）のみサポート可能
* セグメントメンバーシップ開始ジャーニーはサポートされていません
* トランザクションメッセージのオープン/クリックに対するリアクションイベントは、Journey Orchestration内でサポートされています。
* トランザクションメッセージングログは、現在Experience Platformとネイティブに同期されていないため、手動の設定が必要です。 ログの書き出しは、最大4時間ごとに行うことをお勧めします。


## 導入手順

### Adobe Experience Platform

#### スキーマ/データセット

1. お客様が提供するデータに基づいて、Experience Platformで個々のプロファイル、エクスペリエンスのイベント、および複数のエンティティに関するスキーマを設定します。
1. 次のAdobe Campaignスキーマを作成します。broadLog、trackingLog、配信不能アドレス、プロファイル環境設定（オプション）。
1. データ追加使用量ラベルを管理用のデータセットに貼り付けます。
1. 宛先にガバナンスを適用するポリシーを作成します。

#### プロファイル/ID

1. 顧客固有の名前空間を作成します。
1. ID追加をスキーマに送信します。
1. プロファイルのスキーマとデータセットを有効にします。
1. 異なる表示の[!UICONTROL リアルタイム顧客プロファイル]（オプション）にマージルールを設定します。
1. Adobe Campaignに使用するセグメントを作成します。

#### ソース/宛先

1. ストリーミングAPIおよびソースコネクタを使用して、Experience Platformにデータを取り込みます。
1. Adobe Campaignで使用する[!DNL Azure] BLOBストレージ先を構成します。

#### モバイルアプリの展開

1. Adobe Campaign Classic向けAdobe CampaignSDKまたはAdobe Campaign Standard向けExperience PlatformSDKを実装します。 Experience Platform Launchが存在する場合は、Experience PlatformSDKでAdobe Campaign ClassicまたはAdobe Campaign Standardの拡張機能を使用することをお勧めします。


### Journey Orchestration

1. 顧客ジャーニーの開始に使用するストリーミングデータは、オーケストレーションIDを取得するために、まずJourney Orchestration内で構成する必要があります。 次に、このオーケストレーションIDをインジェストで使用する開発者に提供します。
1. 外部データソースを設定します。
1. カスタムアクションを設定

### Adobe Campaign Standard

1. 適切なパーソナライゼーション設定でメッセージングテンプレートを設定します。
1. 書き出しワークフローの書き出しトランザクションメッセージログを設定します。 レコメンデーションは、最大4時間ごとに実行することをお勧めします。


## 関連ドキュメント

* [Adobe Experience Platform文書](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Orchestrationドキュメント](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Adobe Campaign Classic文書](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Adobe Campaign Standard文書](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launchドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience PlatformモバイルSDKドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
