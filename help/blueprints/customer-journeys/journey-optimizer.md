---
title: '[!DNL Journey Optimizer] - トリガーメッセージングとAdobe Experience Platformのブループリント'
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: f8b9cc115739b53bba71d06b228dcce57df9dd7b
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 53%

---

# [!DNL Journey Optimizer] ブループリント

Adobe[!DNL Journey Optimizer] は、マーケティングチームがお客様の行動にリアルタイムで反応し、どこにいても対応するための目的構築されたシステムです。 マーケティングチームは、データ管理機能がAdobeに移行 [!DNL Experience Platform]、最も効果が高いカスタマージャーニーやパーソナライズされた会話を生み出しているカスタマージャーニーに集中できるようになりました。

このブループリントでは、アプリケーションの技術的機能の概要を説明し、ア [!DNL Journey Optimizer] ットを構成する様々なアーキテクチャコンポーネントについて詳しく説明します。

## ユースケース

* トリガーされるメッセージ
* 「ようこそ」と「登録」の確認
* 買い物かごおよび申請フォームの破棄
* 場所でトリガーされるメッセージ
* 競技場での体験
* 旅行と接客の、到着前および滞在のエクスペリエンス

## アーキテクチャ

<img src="assets/ajo-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## ブループリントのシナリオ

| シナリオ | 説明 | 機能 |
| :-- | :--- | :--- |
| [サードパーティメッセージング](3rd-party-messaging.md) | Adobe[!DNL Journey Optimizer] をサードパーティのメッセージングシステムと共に利用して、パーソナライズされたコミュニケーションを編成および送信する方法を示します | 顧客のブランドや企業とのインタラクションに応じて、1：1 のパーソナライズされたコミュニケーションを提供します<br><br>注意点：<br><ul><li>サードパーティシステムは、認証のためにベアラートークンをサポートする必要があります。</li><li>マルチテナントアーキテクチャが原因で静的 IP がサポートされません</li><li>1 秒あたりの API 呼び出しに関しては、サードパーティシステムのアーキテクチャの制約にご注意ください。お客様は、[!DNL Journey Optimizer] からのボリュームをサポートするために、サードパーティベンダーから追加ボリュームを購入する必要がある場合があります</li><li>メッセージまたはペイロードの意思決定管理をサポートしていません</li></ul> |

<br>

## 統合パターン

| 統合 | 説明 | 機能 |
| :-- | :--- | :--- |
| [[!DNL Journey Optimizer] Adobe Campaignを使用 ](ajo-and-campaign.md) | Adobe[!DNL Journey Optimizer] を使用して、リアルタイム顧客プロファイルを利用して 1 対 1 のエクスペリエンスを調整し、ネイティブのAdobe Campaign トランザクションメッセージシステムを活用してメッセージを送信する方法を示します | リアルタイム顧客プロファイルと [!DNL Journey Optimizer] の機能を活用して、即座にエクスペリエンスを調整すると同時に、Adobe Campaignのネイティブなリアルタイムメッセージ機能を活用してラストマイルでのコミュニケーション <br><br> 考慮事項：<br> を行います<ul><li>Campaign アプリケーションは、v7 ビルドが 21.1 より上か v8 のどちらかである必要があります</li><li>メッセージングスループット</li><ul><li>Campaign v7 - 1 時間あたり最大 50,000</li><li>Campaign v8 - 1 時間あたり最大 100,000</li><li>Campaign Standard - 1 時間あたり最大 50,000</li></ul><li>スロットルは実行されないので、ユースケースではエンタープライズアーキテクトによる技術的な検証が必要です</li><li>Campaign から送信されたメッセージの 意思決定管理 を利用するサポートはありません</li></ul> |

<br>

## 前提条件

Adobe[!DNL Experience Platform]:

* [!DNL Journey Optimizer] データソースを設定する前に、システムでスキーマとデータセットを設定する必要があります
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーション eventID」フィールドグループを追加します
* 個々のプロファイルクラスベースのスキーマの場合は、「プロファイルテストの詳細」フィールドグループを追加して、[!DNL Journey Optimizer] で使用するテストプロファイルを読み込むことができます

メール：

* メッセージ送信に使用するサブドメインの準備が整っている必要があります
* サブドメインは、アドビに完全にデリゲートすることも（推奨）、CNAME を使用してアドビ固有の DNS サーバー（カスタム）を指すこともできます
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要

モバイルプッシュ：

* 顧客は、モバイルデベロッパーを使用してアプリを作成できる必要があります
* Adobe Experience Platform Mobile SDK

## ガードレール

[[!DNL Journey Optimizer]  ガードレール製品リンク ](https://experienceleague.adobe.com/ja/docs/journey-optimizer/using/get-started/guardrails)

[ ガードレールとエンドツーエンドの待ち時間のガイダンス ](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=ja)

## 関連ドキュメント

* [[!DNL Experience Platform]  ドキュメント ](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [[!DNL Experience Platform]  タグのドキュメント ](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [[!DNL Experience Platform Mobile SDK]  ドキュメント ](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
* [[!DNL Journey Optimizer]  ドキュメント ](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [[!DNL Journey Optimizer]  製品の説明 ](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
