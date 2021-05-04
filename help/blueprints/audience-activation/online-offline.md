---
title: オンライン/オフラインAudience Activationのブループリント
description: オンライン／オフライン Audience Activation。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: da21d1796eb9a2c9c0f087d82606874ca55bd4ea
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 74%

---

# オンライン/オフラインAudience Activationのブループリント

オンライン行動と共に、オフライン属性およびイベント（オフラインの注文、トランザクション、CRM、ロイヤリティデータなど）を、オンラインターゲティングとパーソナライズ機能に使用します。

既知のプロファイルベースの宛先（電子メールプロバイダー、ソーシャルネットワーク、広告など）に対して、オーディエンスをアクティベーションします。

## ユースケース

* ソーシャルおよび広告の宛先の既知のオーディエンスに対するオーディエンスターゲティング。
* オンラインおよびオフライン属性を使用したオンラインパーソナライズ機能。
* 既知のチャネル（電子メール、SMS など）に対するオーディエンスのアクティベーション。

## アプリケーション

* Adobe Experience Platform
* [!UICONTROL リアルタイム顧客データプラットフォーム]

## 構造

### 宛先を含むオンライン/オフラインAudience Activation

<img src="assets/online_offline_activation.svg" alt="オンライン/オフラインAudience ActivationのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />
<br>

### Experience Cloudアプリケーションを使用したオンライン/オフラインAudience Activation

<img src="assets/activation+apps.svg" alt="Experience Cloudアプリケーションを使用したオンライン/オフラインAudience ActivationのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

「オーディエンスとプロファイルのアクティベーションの概要」ページで説明されているガードレールを参照してください。[LINK](overview.md)

## 実装手順

1. Experience Platform でスキーマおよびデータセットを設定します。
1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに正しい ID および ID 名前空間を設定します。
1. プロファイル用のスキーマおよびデータセットを有効にします。
1. Platform にデータを取り込みます。
1. Experience PlatformとAudience Managerの間で[!UICONTROL Real-time Customer Data Platform]のセグメント共有をプロビジョニングし、Experience Platformで定義されたオーディエンスをAudience Managerに共有します。
1. Experience Platform の作成者セグメントが、バッチまたはストリーミングで評価されます。システムは、セグメントをバッチとして、またはストリーミングとして評価するかを自動的に判定します。
1. プロファイル属性およびオーディエンスメンバーシップを目的の宛先に共有するための宛先を設定します。

## 実装のための考慮事項

* プロファイルデータを宛先に共有するには、宛先ペイロードの宛先で使用される特定の ID 値を含める必要があります。ターゲットの宛先に必要なIDはすべて、プラットフォームに取り込まれ、[!UICONTROL リアルタイムカスタマープロファイル]のIDとして設定する必要があります。

* オーディエンスが Experience Platform から Audience Manager に共有されるアクティベーションシナリオでは、[!UICONTROL リアルタイム顧客プロファイル]に含まれるすべての ID が、Audience Manager に共有されます。必須の宛先 ID が[!UICONTROL リアルタイム顧客プロファイル]に含まれている場合、または[!UICONTROL リアルタイム顧客プロファイル]内の ID が Audience Manager でリンクされる必須の宛先 ID と関連付けられる場合、Experience Platform からのオーディエンスは、Audience Manager 宛先を使用して共有できます。

## 関連ドキュメント

* [リアルタイム顧客データプラットフォーム製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルと分類のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL リアルタイム顧客データプラットフォームのデモ]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)
