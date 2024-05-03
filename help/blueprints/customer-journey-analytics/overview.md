---
title: Customer Journey Analyticsブループリント
description: カスタマージャーニー全体を通して得られたデータと顧客行動を統合して分析します。
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 3bb2dada-f4cd-43f7-a0d0-f276510ad224
source-git-commit: b69e73349741b829f05d04cfac70aa0161ef7684
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 90%

---

# Customer Journey Analyticsブループリント

Customer Journey Analytics は、ブランドが様々なインタラクションチャネルやソースから顧客データと行動を統合して、あらゆる顧客インタラクションのジャーニーベースのビューを作成する方法を示します。レポートおよび分析は、Customer Journey Analytics アプリケーションサービスで実行でき、顧客インタラクションおよび行動パターンを評価してインサイトを得ることができます。

Customer Journey Analytics の使用例の完全なリストについては、こちらにある Customer Journey Analytics ドキュメントを参照してください。

## Customer Journey Analytics ユースケース

[一般的なユースケースを次に示します。](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cja-usecases.html?lang=ja)

* オーディエンスの作成と Real-time Customer Data Platform への公開
* トップ／ボトムコンバージョンパス
* チャネルのエンゲージメントとコンバージョン
* 閲覧数上位のコンテンツ
* 上位のカテゴリおよび製品
* コンバージョンおよびエンゲージメント向上につながったキャンペーン
* セルフサービスエクスペリエンスを最適化するためのツール使用状況分析

## Customer Journey Analytics のアーキテクチャ

![アーキテクチャ図](assets/CJA.svg){zoomable=&quot;yes&quot;}

主なユースケースの例を次に示します。

| ブループリント | 説明 | Experience Cloud アプリケーション |
|---|---|---|
| **[クロスチャネルジャーニー分析](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cross-channel.html?lang=ja)** | <ul><li>Web、モバイルおよびオフラインの様々なプロパティからのデータを統合することで、複数のチャネルをまたいだ顧客行動を単一の統合されたビューに表示します。</li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li><li>Adobe Analytics（オプション）</li></ul> |
| **[Real-time Customer Data Platformへのオーディエンスの公開](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ja)** | <ul><li>Customer Journey Analytics（CJA）で識別されたオーディエンスを作成し、Adobe Experience Platform のリアルタイム顧客プロファイルに公開して、顧客のターゲティングとパーソナライゼーションを実現します。Customer Journey Analytics の詳細なフィルターおよび計算済みフィールドから、履歴データの使用や、より絞り込まれたオーディエンスを使用てのオーディエンスの作成に最適です。</li></ul> | <ul><li>Real-time Customer Data Platform</li><li>Customer Journey Analytics</li> |
| **[着信転送ジャーニー解析](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/call-center.html?lang=ja)** | <ul><li>コールセンターデータを Web、モバイルおよびその他のインタラクションデータと組み合わせることで、どのような行動が担当者による通話に最も影響を与えるかを判別する。</li><li>最適化されたセルフサービスコンテンツおよびツールを使用することで、これらのインサイトは、カスタマーエクスペリエンスの最適化や、担当者のサポートを受けるまでの道のりを短縮するために使用できます。  </li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li> |

## Customer Journey Analytics ブループリントのガードレール図

* ガードレールの詳細とエンドツーエンドの遅延については、[デプロイメントガードレールドキュメント](../experience-platform/deployment/guardrails.md)を参照してください

![ガードレール図](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable=&quot;yes&quot;}

## 関連するブログ投稿

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184){target="_blank"}
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17){target="_blank"}
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1){target="_blank"}
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281){target="_blank"}
* [[!DNL Demonstrating the Power of Adobe's New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34){target="_blank"}
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9){target="_blank"}
