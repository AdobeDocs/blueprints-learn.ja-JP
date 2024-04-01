---
title: 行動 Web パーソナライゼーションブループリント
description: オンライン行動とオーディエンスデータに基づいてコンテンツをパーソナライズする方法を見つけます。
landing-page-description: オンライン行動およびオーディエンスデータに基づいてパーソナライズする方法を説明します。
short-description: オンライン行動およびオーディエンスデータに基づいてパーソナライズする方法を説明します。
solution: Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection, Experience Platform
kt: 7085
thumbnail: thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 96%

---

# 行動 Web およびモバイルパーソナライゼーションブループリント

オンライン行動およびオーディエンスデータに基づいてパーソナライズします。

## ユースケース

* ランディングページの最適化
* 行動ターゲティング
* 以前の製品／コンテンツ表示、製品／コンテンツの親和性、環境属性、サードパーティオーディエンスデータおよび人口統計に基づいたパーソナライズ機能

## アプリケーション

* Adobe Target
* Adobe Analytics（オプション）
* Adobe Audience Manager（オプション）
* Adobe Real-time Customer Data Platform （オプション）

## アーキテクチャ

<img src="assets/behavioral_personalization.svg" alt="行動による web パーソナライズ機能ブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />


## 実装パターン

Web／モバイルパーソナライズ機能ブループリントは、以下に説明する方法で実装できます。

1. [!UICONTROL Platform Web SDK] または [!UICONTROL Platform Mobile SDK] と[!UICONTROL エッジネットワーク]を使用。[Experience Platform Web および Mobile SDK のブループリントを参照](../../experience-platform/deployment/websdk.md)
1. 従来のアプリケーション固有の SDK( 例：AppMeasurement.js) を使用する。 [アプリケーション固有の SDK ブループリントを参照](../../experience-platform/deployment/appsdk.md)

## 実装手順

1. Web またはモバイルアプリケーション用に [Adobe Target を実装](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ja)します。

### 実装手順 - Audience Manager または Adobe Analytics

1. [Adobe Audience Manager を実装](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ja)します
1. [Adobe Analytics を実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)します
1. [Experience Cloud ID サービスを実装](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=ja)します

   >[!NOTE]
   >
   >アプリケーション間のオーディエンス共有を許可するためには、各アプリケーションは、Experience Cloud ID を使用し、同じ Experience Cloud 組織に属している必要があります。

1. [ユーザーおよびオーディエンス共有サービス（共有オーディエンス）のプロビジョニングをリクエスト](https://www.adobe.com/go/audiences)します
1. [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html?lang=ja) または [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=ja) でセグメントを作成し、[これらのオーディエンスを Experience Cloud に共有するように設定](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)します（Audience Manager または Adobe Analytics を使用している場合）
1. オーディエンスが Adobe Target で使用できるようになったら、[Adobe Target によるターゲティングエクスペリエンス](https://experienceleague.adobe.com/docs/target/using/audiences/target.html?lang=ja)で使用できます

### 実装手順 - Real-time Customer Data Platform

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ja)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに[正しい ID および ID 名前空間を設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. Experience Platform に[データを取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)。
1. Experience Platform で定義されたオーディエンスが Audience Manager に共有されるように、[Experience Platform と Audience Manager の間の [!UICONTROL Real-time Customer Data Platform の]セグメント共有を](https://www.adobe.com/go/audiences)プロビジョニングします。
1. Experience Platform で[セグメントを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)セグメントをバッチとして、またはストリーミングとして評価するかを、システムが自動的に判定します。
1. プロファイル属性およびオーディエンスメンバーシップを目的の宛先に共有するための[宛先を設定します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=ja)


## 関連ドキュメント

* [Experience Cloud Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=ja)
* [Audience Manager と Adobe Target の統合](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=ja)
* [Adobe Audience Manager を使用した Adobe Analytics セグメント共有](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ja)
* [[!UICONTROL Real-time Customer Data Platform] の概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL Real-time Customer Data Platform] 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連するブログ投稿

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our "Customer Zero" Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
