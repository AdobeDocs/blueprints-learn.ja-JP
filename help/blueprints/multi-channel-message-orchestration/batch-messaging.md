---
title: Batch MessagingとAdobe Experience PlatformBlueprint
description: Adobe Experience Platformを顧客のプロファイルとセグメント化の中心として使用し、スケジュール済みおよびバッチメッセージングキャンペーンを実行します。
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 844fff1cefe367575beb5c03aa0f0d026eb9f39b
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Batch MessagingとAdobe Experience PlatformBlueprint

Adobe Experience Platformを顧客のプロファイルとセグメント化の中心として使用し、スケジュール済みおよびバッチメッセージングキャンペーンを実行します。

## 使用例

* スケジュールされた電子メールキャンペーン
* オンボーディングとリマーケティングのキャンペーン

## アプリ

* Adobe Experience Platform
* Adobe Campaign Classicまたは標準

## 統合パターン

* Adobe Experience Platform→Adobe Campaign Classic
* Adobe Experience Platform→Adobe Campaign Standard

## 建築

<img src="assets/aepbatch.svg" alt="バッチメッセージングとAdobe Experience Platformシナリオのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* キャンペーン単一の組織単位の導入のみをサポート
* キャンペーンは、プロファイルがキャンペーン内に存在する必要があることを意味するすべてのアクティブなプロファイルにとって真実の源であり、Experience Platformセグメントに基づいて新しいプロファイルを作成してはならない。
* Experience Platformからのセグメントメンバーシップの実現は、バッチ（1日1回）とストリーミング（約5分）の両方で遅延します。

**キャンペーンとのReal-time Customer Data Platformセグメントの共有：**

* 20セグメントの制限に関する推奨事項
* アクティベーションは24時間ごとに制限されます
* アクティベーションに使用できる和集合スキーマ属性のみ(配列、マップ、エクスペリエンスイベントはサポートされません)。
* セグメントあたりの属性の数は20以下にすることを推奨します。
* 「実現」セグメントメンバーシップを持つすべてのプロファイルのセグメントごとに1つのファイル、またはセグメントのメンバーシップがファイルの属性として追加されている場合は「実現」と「終了」の両方のプロファイル
* 増分またはフルセグメントのエクスポートがサポートされます
* ファイルの暗号化はサポートされていません
* 最大4時間に実行するキャンペーンエクスポートワークフロー
* [Experience Platformのプロファイルとデータ取り込みのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)を参照

## 導入手順

### Adobe Experience Platform

#### スキーマ/データセット

1. お客様が提供するデータに基づいて、Experience Platform内の個々のプロファイル、エクスペリエンスのイベント、およびマルチエンティティのスキーマを設定します。
1. broadLog、trackingLog、配信不能アドレス、プロファイル環境設定（オプション）用のキャンペーンスキーマを作成します。
1. データ追加使用量ラベルを管理用のデータセットに貼り付けます。
1. 宛先にガバナンスを適用するポリシーを作成します。

#### プロファイル/ID

1. 顧客固有の名前空間を作成します。
1. ID追加をスキーマに送信します。
1. プロファイルのスキーマとデータセットを有効にします。
1. 様々な表示のリアルタイム顧客プロファイル用にマージルールを設定します（オプション）。
1. キャンペーンに使用するセグメントを作成します。

#### ソース/宛先

1. ストリーミングAPIおよびソースコネクタを使用して、Experience Platformにデータを取り込みます。
1. キャンペーンで使用する[!DNL Azure] BLOBストレージ先を構成します。

#### モバイルアプリの展開

1. Campaign Classic用キャンペーンSDKまたはCampaign Standard用Experience PlatformSDKを実装します。 Experience Platform Launchが存在する場合は、Experience PlatformSDKでCampaign Classic/標準拡張を使用することをお勧めします。

#### Campaign

1. プロファイル、参照データ、および関連する配信のパーソナライズデータのスキーマを設定します。

>[!IMPORTANT]
>
>この時点で、プロファイルとイベントのデータに関するExperience Platform内のデータモデルが何かを理解し、キャンペーンにどのデータが必要かを把握することが重要です。

#### ワークフローの読み込み

1. シンプル化されたプロファイルデータをキャンペーンのSFTPに読み込み、取り込みます。
1. オーケストレーションとメッセージングのパーソナライズデータをキャンペーンのSFTPに読み込んで取り込みます。
1. ワークフローを介して[!DNL Azure] BLOBからExperience Platformセグメントを取り込みます。

#### 書き出しワークフロー

1. キャンペーンログを4時間ごとにワークフロー経由でExperience Platformに送り返します（broadLog、trackingLog、配信不能なアドレス）。
1. コンサルティングによって構築されたワークフローを4時間ごとに使用して、プロファイルの環境設定をExperience Platformに戻します（オプション）。


## 関連ドキュメント

* [Adobe Experience Platform文書](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classicドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standardドキュメント](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launchドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience PlatformモバイルSDKドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
