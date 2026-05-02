---
title: エンタープライズ宛先へのオーディエンスとプロファイルのアクティベーション
description: エンタープライズ宛先へのオーディエンスとプロファイルのアクティベーション
solution: Real-Time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
TQID: https://experienceleague.adobe.com/28T7zrLEqPQxq57ig8NAHVuSDD5UbbCh6dcqogkjG-A
product_v2:
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: ba929a52-9339-4154-9487-317dc875a3c7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 186
ht-degree: 72%

---

# エンタープライズ宛先へのオーディエンスとプロファイルのアクティベーション

>[!TIP]
>このブループリントは、「オーディエンスの構築とアクティベーション」の下の[&#x200B; ユースケースパターン &#x200B;](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)としても利用できます。

プロファイルとオーディエンスの変更とイベントを、[!UICONTROL Real-time Customer Data Platform] からエンタープライズデータストアやアプリケーションにストリーミングまたはバッチで共有します。 これらのプロファイルおよびオーディエンスイベントは、破棄された申し込みプロセスやウェビナー登録のフォローアップ、[!UICONTROL Real-time Customer Data Platform] の最新の顧客属性とインテリジェンスを使用したエンタープライズアプリケーションのアップデートなど、顧客に対する販売またはサポート活動を開始するために使用できます。

## ユースケース

* エンタープライズトラッキング、ストレージ、分析、顧客データおよびインサイトのアクティベーションに向けた、クラウドストレージ宛先またはストリーミング宛先へのプロファイルおよびオーディエンスのアクティベーション。

## アプリケーション

* Real-time Customer Data Platform

## アーキテクチャ

<img src="assets/known_activation.svg" alt="エンタープライズアクティベーションシナリオの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## 関連ドキュメント

クラウドストレージとエンタープライズ宛先の設定に関する追加の詳細については、[宛先ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/cloud-storage/overview)を参照してください。

## ガードレール

[ガードレール ページに記載されているガードレールを参照してください。](../experience-platform/guardrails.md)