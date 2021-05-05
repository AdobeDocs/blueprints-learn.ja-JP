---
title: Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション
description: Enterprise Destinationsへのオーディエンスおよびプロファイルアクティベーション
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: d6eaf978a8f587b881480c14f192cb9e29e3c7e2
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション

[!UICONTROL Real-time Customer Data Platform]から企業のデータ・ストアやアプリケーションに、ストリーミングまたはバッチでプロファイルとオーディエンスの変更とイベントを共有します。 これらのプロファイルおよびオーディエンスイベントは、廃棄された申し込みプロセスやウェビナー登録のフォローアップ、[!UICONTROL Real-time Customer Data Platform]の最新の顧客属性とインテリジェンスを使用したエンタープライズアプリケーションの更新など、顧客に対する販売またはサポート活動を開始するために使用できます。

## ユースケース

* プロファイルおよびオーディエンスのアクティベーションをクラウドストレージの宛先に送信するか、エンタープライズトラッキング、ストレージ、分析、顧客データおよびインサイトのアクティベーションのためのストリーミング送信先に送信します。

## アプリケーション

* Adobe Experience Platform アクティベーション

## 構造

<img src="assets/enterprise_destination_activation.svg" alt="エンタープライズアクティベーションシナリオのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />


## ガードレール

「オーディエンスとプロファイルのアクティベーションの概要」ページで説明されているガードレールを参照してください。[LINK](overview.md)

## 実装手順

1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) スキーマを作成します。
1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) データセットを作成します。
1. [取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに正しい ID および ID 名前空間を設定します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)
1. [プロファイルのスキーマとデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html)。
1. [データを Experience Platform に取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. [Experience Platform で定義されたオーディエンスが Audience Manager に共有されるように、Experience Platform と Audience Manager の間のリアルタイム顧客データプラットフォームセグメント共有をプロビジョニングします。](https://www.adobe.com/go/audiences)
1. [Experience Platformで](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja) セグメントを作成します。システムは、セグメントをバッチとして、またはストリーミングとして評価するかを自動的に判定します。
1. [プロファイル属性およびオーディエンスメンバーシップを目的の宛先に共有するための宛先を設定します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html)

## 関連ドキュメント

* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)
* [クラウドストレージの宛先の概要](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP宛先](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [リアルタイム顧客データプラットフォーム製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルと分類のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL リアルタイム顧客データプラットフォームのデモ]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
