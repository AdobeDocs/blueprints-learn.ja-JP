---
title: Journey Optimizer - トリガーされるメッセージおよび Adobe Experience Platform ブループリント
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 5f9384abe7f29ec764428af33c6dd1f0a43f5a89
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 97%

---

# Journey Optimizerブループリント

Adobe Journey Optimizer は、マーケティングチームが顧客行動にリアルタイムで反応し、顧客が場所を問わずにアクセスできることを目的に構築されたシステムです。データ管理機能が Adobe Experience Platform に移行したことで、マーケティングチームは、世界最高クラスのカスタマージャーニーと、パーソナライズされたやり取りを生み出すことに全力で取り組むことができます。このブループリントは、アプリケーションの技術的機能の概要を説明し、Adobe Journey Optimizer を構成する様々なアーキテクチャコンポーネントについて深く掘り下げます。

<br>

## ユースケース

* トリガーされるメッセージ
* 「ようこそ」と「登録」の確認
* 買い物かごおよび申請フォームの破棄
* 場所でトリガーされるメッセージ
* 競技場での体験
* 旅行と接客の、到着前および滞在のエクスペリエンス

<br>

## アーキテクチャ

<img src="assets/ajo-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## ブループリントのシナリオ

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [サードパーティメッセージング](3rd-party-messaging.md) | Adobe Journey Optimizer をサードパーティのメッセージングシステムと共に使用して、パーソナライズされた通信を調整および送信する方法を示します | 顧客のブランドや企業とのインタラクションに応じて、1：1 のパーソナライズされたコミュニケーションを提供します<br><br>注意点：<br><ul><li>サードパーティシステムは、認証のためにベアラートークンをサポートする必要があります。</li><li>マルチテナントアーキテクチャが原因で静的 IP がサポートされません</li><li>1 秒あたりの API 呼び出しに関しては、サードパーティシステムのアーキテクチャの制約にご注意ください。顧客が Journey Optimizer からのボリュームをサポートするために、サードパーティベンダーから追加のボリュームを購入する必要が生じる場合があります</li><li>メッセージまたはペイロードの意思決定管理をサポートしていません</li></ul> |

<br>

## 統合パターン

| 統合 | 説明 | 機能 |
| :-- | :--- | :--- |
| [Journey Optimizer と Adobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizer を使用し、リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスの調整を行い、ネイティブの Adobe Campaign トランザクションメッセージングシステムを活用してメッセージを送信する方法を示します | リアルタイム顧客プロファイルと Journey Optimizer の機能を活用し、瞬時のエクスペリエンスで調整しながら、Adobe Campaign のネイティブリアルタイムメッセージング機能を利用して、ラストマイルのコミュニケーションを実現します。<br><br>注意点：<br><ul><li>Campaign アプリケーションは、v7 ビルドが 21.1 より上か v8 のどちらかである必要があります</li><li>メッセージングスループット</li><ul><li>Campaign v7 - 1 時間あたり最大 50,000</li><li>Campaign v8 - 1 時間あたり最大 100,000</li><li>Campaign Standard - 1 時間あたり最大 50,000</li></ul><li>スロットルは実行されないので、ユースケースではエンタープライズアーキテクトによる技術的な検証が必要です</li><li>Campaign から送信されたメッセージの 意思決定管理 を利用するサポートはありません</li></ul> |

<br>

## 前提条件

Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーション eventID」フィールドグループを追加します
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします

電子メール

* メッセージ送信に使用するサブドメインの準備が整っている必要があります
* サブドメインは、アドビに完全にデリゲートすることも（推奨）、CNAME を使用してアドビ固有の DNS サーバー（カスタム）を指すこともできます
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要

モバイルプッシュ

* 顧客は、モバイルデベロッパーを使用してアプリを作成できる必要があります
* Adobe Experience Platform Mobile SDK

<br>

## ガードレール

[Journey Optimizer ガードレール製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[ガードレールとエンドツーエンドの待ち時間のガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 関連ドキュメント

* [Experience Platform ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
* [Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [Journey Optimizer 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
