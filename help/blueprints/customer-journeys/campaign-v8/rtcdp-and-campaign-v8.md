---
title: Real-Time CDP と Adobe Campaign v8 の統合パターン
description: Adobe Experience Platform とそのリアルタイム顧客プロファイル、および一元化されたセグメント化ツールを Adobe Campaign v8 と併用して、パーソナライズされた会話を提供する方法を紹介します。
solution: Real-Time Customer Data Platform, Campaign
exl-id: d0291088-02ed-4e7e-b538-018ea40e38c6
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 64%

---

# Adobe [!DNL Campaign] v8 統合パターンとの [!DNL Real-Time CDP] 合

Adobe [!DNL Experience Platform] とそのリアルタイム顧客プロファイルおよび一元化されたセグメンテーションツールをAdobe Campaignとともに利用して、パーソナライズされた会話を提供する方法を紹介します。

## アプリケーション

* アドビ [!DNL Experience Platform Real-Time CDP]
* Adobe [!DNL Campaign] v8

## アーキテクチャ

<img src="images/rtcdp-campaign-v8-architecture.svg" alt="バッチメッセージおよび Adobe Experience Platform 統合パターンの参照アーキテクチャ" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 前提条件

* 顧客は、有効な IMS 組織を持つ Experience Cloud のプロビジョニングが必要です
* Adobe Experience Platformと [!DNL Campaign] は、1 つのログイン URL 用に同じ IMS 組織でプロビジョニングすることをお勧めします
* 顧客は [!DNL Campaign] の V8 インスタンスをプロビジョニングする必要があります
* 顧客は、RTCDP、ソース、宛先に対する資格があり、アクセス権を持っている必要があります。
* Adobe [!DNL Campaign] product context が存在する必要があります

<br>

## 実装手順

Campaign v8 ソースコネクタの Campaign v8 への設定および Real-time Customer Data Platform 宛先コネクタのAdobe Experience Platform v8 への設定については、次のドキュメントを参照してください。
[Campaign およびAEP コネクタ &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=ja)

## ガードレール

### Adobe Campaign

* Campaign ソースコネクタのドキュメント、[Campaign ソースコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=ja)を参照してください。
* Adobe Campaign の単一の組織単位デプロイメントのみをサポートします


### Experience Platform Real-time Customer Data Platform セグメント共有

* RTCDP Campaign の宛先コネクタ - [RTCDP Campaign 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=ja)を参照してください。

* AEP のプロファイルとデータ取り込みガードレール ‐ [リンク](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)を参照してください。
