---
title: '"[!DNL Journey Optimizer]  — トリガーされたメッセージとAdobe Experience Platformブループリント»'
description: ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとして Adobe Experience Platform を使用して、トリガーされるメッセージとエクスペリエンスを実行します。
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: a1f3aef5b508575019bd651b9706efc7d6db5306
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 53%

---

# [!DNL Journey Optimizer] ブループリント

Adobe [!DNL Journey Optimizer] は、マーケティングチームが顧客の行動にリアルタイムで反応し、現在の場所で顧客を満たすためのシステムです。 データ管理機能は、Adobeに移動されました [!DNL Experience Platform] マーケティングチームが最善の行動（世界最高水準のカスタマージャーニーとパーソナライズされた会話）に集中できるようにすること。

このブループリントは、アプリケーションの技術的機能の概要を説明し、を構成する様々なアーキテクチャコンポーネントについて詳しく説明します [!DNL Journey Optimizer].

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
| [サードパーティメッセージング](3rd-party-messaging.md) | Adobe [!DNL Journey Optimizer] は、パーソナライズされた通信を調整および送信するためにサードパーティのメッセージングシステムと共に使用できます | 顧客のブランドや企業とのインタラクションに応じて、1：1 のパーソナライズされたコミュニケーションを提供します<br><br>注意点：<br><ul><li>サードパーティシステムは、認証のためにベアラートークンをサポートする必要があります。</li><li>マルチテナントアーキテクチャが原因で静的 IP がサポートされません</li><li>1 秒あたりの API 呼び出しに関しては、サードパーティシステムのアーキテクチャの制約にご注意ください。お客様がサードパーティベンダーから追加のボリュームを購入して、からのボリュームをサポートする必要が生じる場合があります。 [!DNL Journey Optimizer]</li><li>メッセージまたはペイロードの意思決定管理をサポートしていません</li></ul> |

<br>

## 統合パターン

| 統合 | 説明 | 機能 |
| :-- | :--- | :--- |
| [[!DNL Journey Optimizer] Adobe Campaignと](ajo-and-campaign.md) | Adobeの使用方法を示します [!DNL Journey Optimizer] リアルタイム顧客プロファイルを利用して 1:1 エクスペリエンスを調整し、ネイティブのAdobe Campaignトランザクションメッセージングシステムを活用してメッセージを送信する | リアルタイムの顧客プロファイルとの力を活用する [!DNL Journey Optimizer] Adobe Campaignのネイティブリアルタイムメッセージング機能を利用してラストマイル通信を行いながら、瞬時のエクスペリエンスで調整する<br><br>注意点：<br><ul><li>Campaign アプリケーションは、v7 ビルドが 21.1 より上か v8 のどちらかである必要があります</li><li>メッセージングスループット</li><ul><li>Campaign v7 - 1 時間あたり最大 50,000</li><li>Campaign v8 - 1 時間あたり最大 100,000</li><li>Campaign Standard - 1 時間あたり最大 50,000</li></ul><li>スロットルは実行されないので、ユースケースではエンタープライズアーキテクトによる技術的な検証が必要です</li><li>Campaign から送信されたメッセージの 意思決定管理 を利用するサポートはありません</li></ul> |

<br>

## 前提条件

Adobe [!DNL Experience Platform]:

* スキーマとデータセットは、設定する前にシステムで設定する必要があります [!DNL Journey Optimizer] データソース
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、「オーケストレーション eventID」フィールドグループを追加します
* 個々のプロファイルクラスベースのスキーマの場合、「プロファイルテストの詳細」フィールドグループを追加して、で使用するテストプロファイルを読み込めるようにします。 [!DNL Journey Optimizer]

電子メール：

* メッセージ送信に使用するサブドメインの準備が整っている必要があります
* サブドメインは、アドビに完全にデリゲートすることも（推奨）、CNAME を使用してアドビ固有の DNS サーバー（カスタム）を指すこともできます
* Google TXT レコードは、配信品質を高めるために各サブドメインに必要

モバイルプッシュ：

* 顧客は、モバイルデベロッパーを使用してアプリを作成できる必要があります
* Adobe Experience Platform Mobile SDK

## ガードレール

[[!DNL Journey Optimizer] Guardrails 製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[ガードレールとエンドツーエンドの待ち時間のガイダンス](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 関連ドキュメント

* [[!DNL Experience Platform] ドキュメント](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ja)
* [[!DNL Experience Platform] タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [[!DNL Experience Platform Mobile SDK] ドキュメント](https://experienceleague.adobe.com/docs/mobile.html?lang=ja)
* [[!DNL Journey Optimizer] ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ja)
* [[!DNL Journey Optimizer] 製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
