---
title: Real-Time CDP と Adobe Campaign v7 および Campaign Standard の統合パターン
description: Adobe Experience Platform とそのリアルタイム顧客プロファイル、および一元化されたセグメント化ツールを Adobe Campaign と併用して、パーソナライズされた会話を提供する方法を紹介します。
solution: Real-Time Customer Data Platform, Campaign
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: ae7347be5095ca4a7f99f9371dd94d87097112b0
workflow-type: ht
source-wordcount: '804'
ht-degree: 100%

---

# Real-Time CDP と Adobe Campaign の統合パターン

Adobe Experience Platform とそのリアルタイム顧客プロファイル、および一元化されたセグメント化ツールを Adobe Campaign と併用して、パーソナライズされた会話を提供する方法を紹介します。

<br>

## アプリケーション

* Adobe Experience PlatformReal-Time CDP
* Adobe Campaign v7 または Campaign Standard

<br>

## アーキテクチャ

<img src="assets/rtcdp-campaign-architecture.svg" alt="バッチメッセージおよび Adobe Experience Platform 統合パターンの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 前提条件

* Experience Platform と Campaign は、同じ IMS Org でプロビジョニングし、ユーザーアクセスに Adobe Admin Console を使用することを推奨します。また、マーケティング UI 内からソリューション切り替えボタンを使用しても、
これにより、顧客がマーケティング UI 内からソリューションスイッチャーを利用することも可能になります

<br>

## ガードレール

### Adobe Campaign

* Adobe Campaign の単一の組織単位デプロイメントのみをサポートします
* Adobe Campaign は、すべてのアクティブなプロファイルに関する信頼できるソースです。つまり、プロファイルは Adobe Campaign に存在する必要があるため、Experience Platform セグメントに基づいた新しいプロファイルを作成しないでください。
* Campaign エクスポートワークフローは最大でも 4 時間ごとに実行します
* Adobe Campaign broadLog、trackingLogs および配信不能アドレスの XDM スキーマとデータセットは、初期設定では使用できず、設計および構築する必要があります

### Experience Platform CDP セグメント共有

* 20 セグメントに制限することをお勧めします
* アクティベーションは、24 時間ごとに制限されます
* アクティベーションには、結合スキーマ属性のみを使用できます（配列／マップ／エクスペリエンスイベントはサポートされません）
* セグメントあたり 20 個以下の属性にすることを推奨します
* セグメントメンバーシップが「実現」された全プロファイルの、セグメントごとに 1 つのファイル、またはセグメントメンバーシップがファイルの属性として追加されている場合、「実現」したプロファイルと「終了」したプロファイルの両方
* 増分およびフルセグメント書き出しがサポートされます
* ファイルの暗号化はサポートされません

<br>

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)
1. broadLog、trackingLog、配信不能アドレスおよびプロファイル環境設定用に Adobe Campaign スキーマを作成します（オプション）。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. Adobe Campaign 使用状況用のセグメントを作成します。

#### ソース／宛先

1. [Experience Platform と Campaign Standard のソースと宛先](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ja)
1. [Experience Platform と Campaign v7 のソースと宛先](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html?lang=ja)
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
   * Campaign Mobile SDK
* Experience Platform Mobile SDK ルート：
   * アドビタグと Campaign Classic 拡張機能を活用して、Experience Platform Mobile SDK との統合を設定します。
   * アドビタグとデータ収集に関する実務知識が必要です
   * SDK のデプロイ、FCM（Android）および APNS（iOS）との統合によるプッシュトークンの取得、プッシュ通知を受け取るためのアプリの設定、プッシュインタラクションの処理など、Android および iOS でのプッシュ通知に関するモバイル開発経験が必要です。
* Campaign Mobile SDK
   * 詳しくは、[Campaign SDK ドキュメント]を参照（Campaign モバイル SDK。ここで説明するデプロイメントドキュメントに従ってください）。

  >[!IMPORTANT]
  >Campaign SDK をデプロイし、他の Experience Cloud アプリケーションと連携する場合は、データ収集に Experience Platform Mobile SDK を使用する必要があります。これにより、デバイス上でクライアント側の呼び出しが重複します。

## 関連ドキュメント

* [Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Campaign Classic ドキュメント](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ja)
* [Campaign Standard ドキュメント](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ja)
* [Experience Platform Launch ドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
