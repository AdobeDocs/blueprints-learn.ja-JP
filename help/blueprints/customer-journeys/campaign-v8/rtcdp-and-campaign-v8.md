---
title: Real-Time CDP と Adobe Campaign v8 の統合パターン
description: Adobe Experience Platform とそのリアルタイム顧客プロファイル、および一元化されたセグメント化ツールを Adobe Campaign v8 と併用して、パーソナライズされた会話を提供する方法を紹介します。
solution: Real-Time Customer Data Platform, Campaign
exl-id: d0291088-02ed-4e7e-b538-018ea40e38c6
TQID: https://experienceleague.adobe.com/LANKBKui1B5RfyNI8ufsgjrC98TXpAf74IB-alwDTnk
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 264
ht-degree: 76%

---

# [!DNL Real-Time CDP] （Adobe [!DNL Campaign] v8統合パターン）

Adobe [!DNL Experience Platform]とそのリアルタイム顧客プロファイルおよび一元化されたセグメンテーションツールをAdobe Campaignで活用して、パーソナライズされた会話を提供する方法を紹介します。

## アプリケーション

* アドビ [!DNL Experience Platform Real-Time CDP]
* Adobe [!DNL Campaign] v8

## アーキテクチャ

<img src="images/rtcdp-campaign-v8-architecture.svg" alt="バッチメッセージおよび Adobe Experience Platform 統合パターンの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 前提条件

* 顧客は、有効な IMS 組織を持つ Experience Cloud のプロビジョニングが必要です
* Adobe Experience Platformと[!DNL Campaign]は、シングルログイン URL用に同じIMS組織でプロビジョニングすることをお勧めします
* お客様は[!DNL Campaign]のV8 インスタンスをプロビジョニングする必要があります
* 顧客は、RTCDP、ソース、宛先に対する資格があり、アクセス権を持っている必要があります。
* Adobe [!DNL Campaign]製品コンテキストが存在する必要があります

<br>

## 実装手順

Campaign v8 ソースコネクタを Adobe Experience Platform に設定し、Real-time Customer Data Platform 宛先コネクタを Campaign v8 に設定する方法については、次のドキュメントを参照してください。
[Campaign と AEP コネクタ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=ja)

## ガードレール

### Adobe Campaign

* Campaign ソースコネクタのドキュメント、[Campaign ソースコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=ja)を参照してください。
* Adobe Campaign の単一の組織単位デプロイメントのみをサポートします


### Experience Platform Real-time Customer Data Platform セグメント共有

* RTCDP Campaign の宛先コネクタ - [RTCDP Campaign 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=ja)を参照してください。

* AEP のプロファイルとデータ取り込みガードレール ‐ [リンク](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)を参照してください。
