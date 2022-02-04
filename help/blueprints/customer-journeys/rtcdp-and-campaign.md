---
title: Real-Time CDPとAdobe Campaignブループリント
description: Adobe Experience Platformとそのリアルタイム顧客プロファイルおよび一元化されたセグメント化ツールをAdobe Campaignと共に使用して、パーソナライズされた会話を提供する方法を紹介します。
solution: Experience Platform, Campaign v8, Campaign Classic v7, Campaign Standard
source-git-commit: 1c46cbdfc395de4fc9139966cf869ba1feeceaaa
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 56%

---

# Real-Time CDPとAdobe Campaignブループリント

Adobe Experience Platformとそのリアルタイム顧客プロファイルおよび一元化されたセグメント化ツールをAdobe Campaignと共に使用して、パーソナライズされた会話を提供する方法を紹介します。

<br>

## アプリケーション

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v7 またはCampaign Standard

<br>

## アーキテクチャ

<img src="assets/rtcdp-campaign-architecture.svg" alt="バッチメッセージおよび Adobe Experience Platform ブループリントの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 前提条件

* Experience Platformとキャンペーンは、同じ IMS Org でプロビジョニングし、ユーザーアクセスにAdobe Admin Consoleを使用することをお勧めします。 また、マーケティング UI 内からソリューション切り替えボタンを使用しても、

<br>

## ガードレール

### Adobe Campaign

* Adobe Campaign単一の組織単位のデプロイメントのみをサポート
* Adobe Campaign は、すべてのアクティブなプロファイルに関する信頼できるソースです。つまり、プロファイルは Adobe Campaign に存在する必要があるため、Experience Platform セグメントに基づいた新しいプロファイルを作成しないでください。
* Campaign エクスポートワークフローは最大でも 4 時間ごとに実行します
* Adobe Campaign broadLog、trackingLogs および配信不能アドレスの XDM スキーマとデータセットは、初期設定では使用できず、設計および構築する必要があります

### Experience PlatformCDP セグメント共有

* 20 セグメント制限の推奨
* 有効化は 24 時間ごとに制限されます
* アクティベーションに使用できる和集合スキーマ属性のみ（配列、マップ、エクスペリエンスのイベントはサポートされません）
* セグメントあたり 20 個以下の属性に関するレコメンデーション
* 「適合された」セグメントメンバーシップを含むすべてのプロファイルのセグメントごとに 1 ファイル、またはセグメントメンバーシップがファイルの属性として追加されている場合は、「適合」および「既存」の両方のプロファイルのセグメントごとに 1 ファイル
* 増分および完全なセグメントの書き出しがサポートされます
* ファイルの暗号化はサポートされません

<br>

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. broadLog、trackingLog、配信不能アドレスおよびプロファイル環境設定用に Adobe Campaign スキーマを作成します（オプション）。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. Adobe Campaign 使用状況用のセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)
1. Adobe Campaign で使用する [!DNL Azure] Blob ストレージ宛先を設定します。

#### Adobe Campaign

1. プロファイル、ルックアップデータおよび関連する配信パーソナライズ機能データ用にスキーマを設定します。

>[!IMPORTANT]
>
>この時点で、Experience Platform 内にあるプロファイルおよびイベントデータ用のデータモデルを把握し、Adobe Campaign で必要になるデータを知っておくことが重要です。

#### インポートワークフロー

1. シンプル化されたプロファイルデータを Adobe Campaign sFTP に読み込んで取り込みます。
1. オーケストレーションおよびメッセージングパーソナライズ機能データを Adobe Campaign sFTP に読み込んで取り込みます。
1. ワークフローを使用して [!DNL Azure] Blob から Experience Platform セグメントを取り込みます。

#### エクスポートワークフロー

1. ワークフローを使用して、4 時間ごとに Experience Platform に Adobe Campaign ログを返します（broadLog、trackingLog、配信不能アドレス）。
1. コンサルティングが作成したワークフローを使用して、4 時間ごとに Experience Platform にプロファイル環境設定を返します（オプション）。


### モバイルプッシュ設定

* プッシュ通知用にモバイルデバイスとの統合に関してサポートされる 2 つの方法を示します。
   * Experience Platform Mobile SDK
   * Campaign モバイル SDK
* Experience Platformモバイル SDK のルート：
   * AdobeタグとCampaign Classic拡張機能を活用して、Experience PlatformMobile SDK との統合を設定します。
   * Adobeタグとデータ収集に関する実務知識が必要
   * SDK のデプロイには Android とiOSの両方でプッシュ通知を使用したモバイル開発エクスペリエンスが必要で、FCM(Android) や APNS(iOS) と統合してプッシュトークンを取得し、プッシュ通知を受信してプッシュインタラクションを処理するにはアプリを設定
* Campaign モバイル SDK
   * 詳しくは、 [Campaign SDK ドキュメント]（Campaign モバイル SDK。ここで説明するデプロイメントドキュメントに従ってください）

   >[!IMPORTANT]
   >Campaign SDK をデプロイし、他のExperience Cloudアプリケーションと連携する場合は、データ収集にExperience Platformの Mobile SDK を使用する必要があります。 これにより、デバイス上でクライアント側の呼び出しが重複します。

## 関連ドキュメント

* [Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Campaign Classic ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign Standard ドキュメント](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
* [Experience Platform Launch ドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
