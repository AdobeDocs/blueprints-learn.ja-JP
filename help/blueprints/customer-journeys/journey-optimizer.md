---
title: Journey Optimizer — トリガーされたメッセージとAdobe Experience Platformブループリント
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: dc13a1fe9a32f70497c5c73485618e6989b7a644
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 49%

---

# Journey Optimizer

Adobe Journey Optimizerは、マーケティングチームが顧客の行動にリアルタイムで反応し、現在の場所でマーケティングチームに会うための目的に特化したシステムです。 データ管理機能がAdobe Experience Platformに移行され、マーケティングチームは、次のような最善の行動に集中できます。これは、世界最高クラスのカスタマージャーニーと、パーソナライズされた会話を生み出しています。  このブループリントは、アプリケーションの技術的機能の概要を説明し、Adobe Journey Optimizerを構成する様々なアーキテクチャコンポーネントについて深く掘り下げます。

## ユースケース

* トリガーされるメッセージ
* 登録確認
* 買い物かごおよび申請フォームの破棄
* 場所でトリガーされるメッセージ

## アーキテクチャ

<img src="assets/journey-optimizer.png" alt="トリガーされるメッセージおよび Adobe Experience Platform ブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />

## 統合パターン

* Adobe Experience Platform/Journey Optimizer

## 前提条件

1. 有効なIMS組織を持つExperience Cloudのプロビジョニングが必要
1. モバイルプッシュ

* お客様は、モバイルデベロッパーを使用してアプリを作成できる必要があります
* Adobe Experience Platform Mobile SDK
* Adobe開始
   * モバイルプロパティ
      * 拡張機能：
         * Adobe Journey Optimizer Extension
         * Adobe Experience Platform Edge Network
         * ID
         * モバイルコア
         * プロファイル
   * アプリの設定
   * データストリーム
      * Experience Platform
      * イベントデータセット — 一般的なモバイル動作の収集に使用
      * プロファイルデータセット — AJOプッシュプロファイルデータセット（異なる値は使用できません）

## ガードレール

* 制限について詳しくは、リンクを参照してください
* バッチセグメント — 認定されたユーザーの1日あたりの量を把握し、宛先システムがジャーニーごとおよびすべてのジャーニーでバーストスループットを処理できることを確認する必要がある
* ストリーミングセグメント — ジャーニーごとおよびすべてのジャーニーにわたる日別のストリーミング認定量と共に、プロファイル認定の初期バーストを確実に処理する必要がある
* プロファイル更新アクティビティ — リアルタイム顧客プロファイルは、ジャーニー内からネイティブに更新できます。  プロファイルストアへの更新の処理には、最大1分の遅延があります
* ビジネスイベント — JOシステムへの外部呼び出しに基づいて、読み取りセグメントベースのジャーニーをトリガーし、開始できます
* ネイティブでは、Offer decisioningのみをサポートします。 ネイティブ・アクションによる将来のサポート
* サポートされるチャネル：
   * 電子メール
   * プッシュ(FCM/APNS)
   * Rest APIエンドポイント
* 1秒あたり5,000件のイベントを処理し、水平方向にスケーリング（ウォレットは制限）
* A/Bテストは、2つの配信を使用し、QSまたはCJAを使用して結果を決定することでおこなわれます
* Litmus統合 — 統合を活用するには、Litmusのアカウントが必要です。

## 実装手順

### Adobe Experience Platform

#### スキーマ／データセット

1. 顧客提供データに基づき、Experience Platform で[個人プロファイル、エクスペリエンスイベントおよびマルチエンティティスキーマを設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html?lang=ja)。
1. broadLog、trackingLog、配信不能アドレスおよびプロファイル環境設定用に Adobe Campaign スキーマを作成します（オプション）。
1. Experience Platform で取り込む[データセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)
1. ガバナンス用のデータセットに、Experience Platform で[データ使用ラベルを追加します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ja)
1. 宛先のガバナンスを実施する[ポリシーを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ja)

#### プロファイル／ID

1. [任意の顧客専用の名前空間を作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)
1. [スキーマに ID を追加します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. [!UICONTROL リアルタイム顧客プロファイル]の様々な表示用に[結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します（オプション）。
1. キャンペーン使用状況用のセグメントを作成します。

#### ソース／宛先

1. ストリーミング API およびソースコネクタを使用して、[Experience Platform にデータを取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)。 1. Adobe Campaign で使用する [!DNL Azure] Blob ストレージ宛先を設定します。

#### モバイルアプリデプロイメント

1. Adobe Campaign Classic 用の Adobe Campaign SDK または Adobe Campaign Standard 用の Experience Platform SDK を実装します。Experience Platform Launch がある場合は、Adobe Campaign Classic または Adobe Campaign Standard 拡張と Experience Platform SDK を使用することをお勧めします。


### Journey Orchestration

1. カスタマージャーニーの開始に使用するストリーミングデータは、オーケストレーションIDを取得するために、まずJourney Optimizer内で設定する必要があります。 このオーケストレーション ID は、取り込みに使用するためにデベロッパーに供給されます。
1. 外部データソースを設定します。
1. カスタムアクションを設定します。

## 関連ドキュメント

* [Adobe Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Journey Optimizerドキュメント](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=ja)
* [Experience Platform Launch ドキュメント](https://experienceleague.adobe.com/docs/launch.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
