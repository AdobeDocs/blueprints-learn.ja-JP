---
title: Adobe Customer Journey AnalyticsとAdobe Real-Time CDPの連携
description: Customer Journey Analytics のカスタマージャーニー全体からデータと顧客行動を統合および分析し、CJA から RTCDP にオーディエンスを公開します。
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
TQID: https://experienceleague.adobe.com/gbNXsco0cQIcn5O83ofB-rb0PF65v7kaTZ7mTngqHks
product_v2:
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
feature_v2:
  - id: ce577701-5b9e-4fe4-8fa3-4eedea976da4
subfeature_v2:
  - id: cc092ab1-90ba-4bbc-b4c6-6249d87daf5c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 157
ht-degree: 87%

---

# Adobe Customer Journey AnalyticsとAdobe Real-Time CDPの連携

Customer Journey Analytics（CJA）で識別されたオーディエンスを作成し、Adobe Experience Platform のリアルタイム顧客プロファイルに公開して、顧客のターゲティングとパーソナライゼーションを実現します。 Customer Journey Analytics の詳細なフィルターおよび計算済みフィールドから、履歴データの使用や、より絞り込まれたオーディエンスを使用てのオーディエンスの作成に最適です。

## Customer Journey Analytics オーディエンス公開ガイド

Customer Journey Analytics から Real-time Customer Data Platform へのオーディエンスの公開に関する実装と設定ガイダンスについては、次のドキュメントを参照してください。 [ドキュメント](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ja)

## Customer Journey Analytics ブループリントのアーキテクチャ

![アーキテクチャ図](assets/CJA.svg){zoomable="yes"}

## Customer Journey Analytics ブループリントのガードレール図

* ガードレールの詳細とエンドツーエンドの遅延については、[デプロイメントガードレールドキュメント](../experience-platform/guardrails.md)を参照してください