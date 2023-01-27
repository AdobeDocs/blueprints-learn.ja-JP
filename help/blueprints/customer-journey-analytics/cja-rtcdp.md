---
title: Customer Journey Analytics（Real-time Customer Data Platform 付き） ブループリント
description: Customer Journey Analytics のカスタマージャーニー全体からデータと顧客行動を統合および分析し、CJA から RTCDP にオーディエンスを公開します。
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: b18d491fdefc57762932d1570401b5437bf97c76
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 93%

---

# Real-time Customer Data Platform を使用した Customer Journey Analytics ブループリント

Customer Journey Analytics（CJA）で識別されたオーディエンスを作成し、Adobe Experience Platform のリアルタイム顧客プロファイルに公開して、顧客のターゲティングとパーソナライゼーションを実現します。Customer Journey Analytics の詳細なフィルターおよび計算済みフィールドから、履歴データの使用や、より絞り込まれたオーディエンスを使用てのオーディエンスの作成に最適です。

## Customer Journey Analyticsオーディエンス公開ガイド

Customer Journey Analytics から Real-time Customer Data Platform へのオーディエンスの公開に関する実装と設定ガイダンスについては、次のドキュメントを参照してください。[ドキュメント](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ja)

## Customer Journey Analyticsブループリントのアーキテクチャ

![アーキテクチャ図](assets/CJA_RTCDP.svg)

## Customer Journey Analyticsブループリントのガードレール図

* ガードレールの詳細とエンドツーエンドの遅延については、[デプロイメントガードレールドキュメント](../experience-platform/deployment/guardrails.md)を参照してください

![ガードレール図](../experience-platform/assets/CJA_guardrails.svg)

## よくある質問

* CJA が送信した RTCDP に対応するプロファイルが存在しない場合、新しいプロファイルが作成されますか、それとも既に存在するプロファイルの CJA からのみ視聴者が記録されますか。はい、新しいプロファイルが作成されます。その結果、RTCDP 実装が既知の顧客のみを対象としている場合、既知の ID を持つプロファイルのみをフィルタリングするように CJA オーディエンスルールを作成する必要があります。これにより、RTCDP プロファイルカウントが、望まれていない場合には、匿名プロファイルから増加しないことが保証されます。

* CJA は、オーディエンスデータをパイプラインイベントとして送信しますか、それともデータレイクにも送信されるフラットファイルですか。CJA オーディエンスは、パイプラインを介して RTCDP プロファイルサービスにストリーミングされますが、データもデータセットとしてデータレイクに保存されます。

* CJA はどの ID を送信しますか。CJA は、CJA の設定時に「ユーザー ID」として設定された ID を介して送信します。

* 何がプライマリ ID として設定されますか。CJA をプライマリ「人」ID として設定した際にユーザーが選択した ID です。

* ID サービスは CJA メッセージも処理しますか。すなわち、CJA は、オーディエンス共有を通じてプロファイル ID グラフに ID を追加することができますか。いいえ。ID サービスは CJA メッセージを処理しません。

## 関連するブログ投稿

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184)
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17)
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1)
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281)
* [[!DNL Demonstrating the Power of Adobe's New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34)
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9)
