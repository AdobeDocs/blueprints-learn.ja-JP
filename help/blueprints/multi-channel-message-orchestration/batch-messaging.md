---
title: Batch MessagingとAdobe Experience PlatformBlueprint
description: Adobe Experience Platform を顧客プロファイルおよびセグメント化の中央ハブとして使用して、スケジュールされたキャンペーンおよびバッチメッセージキャンペーンを実行します。
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 59%

---

# Batch MessagingとAdobe Experience PlatformBlueprint

Adobe Experience Platform を顧客プロファイルおよびセグメント化の中央ハブとして使用して、スケジュールされたキャンペーンおよびバッチメッセージキャンペーンを実行します。

## ユースケース

* スケジュールされた電子メールキャンペーン
* オンボーディングおよびリマーケティングキャンペーン

## アプリケーション

* Adobe Experience Platform
* Adobe Campaign Classic または Standard

## 統合パターン

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## 構造

<img src="assets/aepbatch.svg" alt="Batch MessagingとAdobe Experience PlatformのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* Adobe Campaign単一の組織単位の導入のみをサポート
* Adobe Campaignは、プロファイルがAdobe Campaign内に存在する必要があることを意味するすべてのアクティブなプロファイルにとって真実の源であり、Experience Platformセグメントに基づいて新しいプロファイルを作成してはならない。
* Experience Platform からのセグメントメンバーシップ適合は、バッチ（1 日 1 回）およびストリーミング（5 分以内）の両方に対して待ち時間があります

**[!UICONTROL Adobe Campaignとのリアルタイム顧客データ] プラットフォームセグメント共有：**

* 20 セグメントに制限することをお勧めします
* アクティベーションは、24 時間ごとに制限されます
* アクティベーションには、結合スキーマ属性のみを使用できます（配列／マップ／エクスペリエンスイベントはサポートされません）。
* セグメントあたり 20 個以下の属性にすることをお勧めします
* 「適合された」セグメントメンバーシップを含むすべてのプロファイルのセグメントごとに 1 ファイル、またはセグメントメンバーシップがファイルの属性として追加されている場合は、「適合」および「既存」の両方のプロファイルのセグメントごとに 1 ファイル
* 増分またはフルセグメント書き出しがサポートされます
* ファイルの暗号化はサポートされません
* 最大4時間に実行するAdobe Campaignエクスポートワークフロー
* [Experience Platform のプロファイルおよびデータ取り込みのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)を参照してください

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づいて、Experience Platform で個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します。
1. broadLog、trackingLog、配信不能アドレス、プロファイル環境設定（オプション）用のAdobe Campaignスキーマを作成します。
1. ガバナンス用に、データセットにデータ使用ラベルを追加します。
1. 宛先のガバナンスを実施するポリシーを作成します。

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

#### Adobe Campaign

1. プロファイル、ルックアップデータおよび関連する配信パーソナライズ機能データ用にスキーマを設定します。

>[!IMPORTANT]
>
>この時点で、プロファイルとイベントのデータに関するExperience Platform内のデータモデルが何かを理解し、Adobe Campaignにどのデータが必要かを把握することが重要です。

#### インポートワークフロー

1. シンプル化されたプロファイルデータをAdobe CampaignのSFTPに読み込み、取り込みます。
1. オーケストレーションとメッセージングのパーソナライズデータをAdobe CampaignのSFTPに読み込んで取り込みます。
1. ワークフローを使用して [!DNL Azure] Blob から Experience Platform セグメントを取り込みます。

#### エクスポートワークフロー

1. Adobe Campaignログを4時間ごとにワークフロー経由でExperience Platformに送り返します（broadLog、trackingLog、配信不能なアドレス）。
1. コンサルティングが作成したワークフローを使用して、4 時間ごとに Experience Platform にプロファイル環境設定を返します（オプション）。


## 関連ドキュメント

* [Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Campaign Classic ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign Standard ドキュメント](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
* [Experience Platform Launch ドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
