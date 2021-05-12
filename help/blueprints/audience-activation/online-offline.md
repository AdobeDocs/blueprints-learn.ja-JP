---
title: オンライン／オフラインオーディエンスアクティベーションブループリント
description: オンライン／オフラインオーディエンスアクティベーション。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: f527b23587e4ec893532997c3c99270946d7fa31
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 77%

---

# オンライン／オフラインオーディエンスアクティベーションブループリント

オンライン行動と共に、オフライン属性およびイベント（オフラインの注文、トランザクション、CRM、ロイヤリティデータなど）を、オンラインターゲティングとパーソナライズ機能に使用します。

既知のプロファイルベースの宛先（電子メールプロバイダー、ソーシャルネットワーク、広告など）に対して、オーディエンスをアクティブ化します。

オンライン/オフラインAudience Activationのブループリントは、[オーディエンスとプロファイルのアクティベーションと、Experience CloudアプリケーションのBlueprint](platform-and-applications.md)と密接に連携しています。 詳細は、[オーディエンスとプロファイルのアクティベーションに、Experience CloudアプリケーションのBlueprint](platform-and-applications.md)と共に記載されています。   Experience PlatformアプリケーションとExperience Cloudアプリケーションの間の統合に固有です。

## ユースケース

* ソーシャルおよび広告の宛先の既知のオーディエンスに対するオーディエンスターゲティング。
* オンラインおよびオフライン属性を使用したオンラインパーソナライズ機能。
* 既知のチャネル（電子メール、SMS など）に対するオーディエンスをアクティブ化。

## アプリケーション

* Adobe Experience Platform
* [!UICONTROL リアルタイム顧客データプラットフォーム]

## アーキテクチャ

### 宛先を含むオンライン/オフラインAudience Activation

<img src="assets/online_offline_activation.svg" alt="オンライン／オフラインオーディエンスアクティベーションブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />
<br>

## ガードレール

[「オーディエンスとプロファイルのアクティベーションの概要」ページで説明されているガードレールを参照してください。](overview.md)

## 実装手順

1. [取り込むデータのスキーマを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html)
1. [取り込むデータのデータセットを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
1. [取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに正しい ID および ID 名前空間を設定します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html)
1. [プロファイルのスキーマとデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html)。
1. [データを Experience Platform に取り込みます。](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
1. [Experience Platform で定義されたオーディエンスが Audience Manager に共有されるように、Experience Platform と Audience Manager の間の[!UICONTROL リアルタイム顧客データプラットフォーム]のセグメント共有をプロビジョニングします。](https://www.adobe.com/go/audiences)
1. [Experience Platformで](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja) セグメントを作成します。セグメントをバッチとして、またはストリーミングとして評価するかを、システムが自動的に判定します。
1. [プロファイル属性およびオーディエンスメンバーシップを目的の宛先に共有するための宛先を設定します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html)

## 実装に関する考慮事項

* プロファイルデータを宛先に共有するには、宛先ペイロードの宛先で使用される特定の ID 値を含める必要があります。ターゲットの宛先に必要な ID は、Platform に取り込まれ、[!UICONTROL リアルタイム顧客プロファイル]の ID として設定される必要があります。

* オーディエンスが Experience Platform から Audience Manager に共有されるアクティベーションシナリオでは、[!UICONTROL リアルタイム顧客プロファイル]に含まれるすべての ID が、Audience Manager に共有されます。必須の宛先 ID が[!UICONTROL リアルタイム顧客プロファイル]に含まれている場合、または[!UICONTROL リアルタイム顧客プロファイル]内の ID が Audience Manager でリンクされる必須の宛先 ID と関連付けられる場合、Experience Platform からのオーディエンスは、Audience Manager 宛先を使用して共有できます。

## 関連ドキュメント

* [[!UICONTROL リアルタイム顧客データプラットフォーム]製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [[!UICONTROL リアルタイム顧客データプラットフォーム]の概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL リアルタイム顧客データプラットフォーム]のデモ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
