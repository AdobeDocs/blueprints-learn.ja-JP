---
title: オンラインとオフラインのデータを使用したアクティベーションブループリント
description: オンライン／オフラインオーディエンスアクティベーション。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: c4adcc5d23bb0482a348d7b5b2b70b06ff2873e8
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 79%

---

# オンラインとオフラインのデータを使用したアクティベーションブループリント

オンライン行動と共に、オフライン属性およびイベント（オフラインの注文、トランザクション、CRM、ロイヤリティデータなど）を、オンラインターゲティングとパーソナライズ機能に使用します。

既知のプロファイルベースの宛先（電子メールプロバイダー、ソーシャルネットワーク、広告など）に対して、オーディエンスをアクティブ化します。

オンラインとオフラインのデータを使用したアクティベーションブループリントは、[Experience Cloud アプリケーションを使用したオーディエンスとプロファイルのアクティベーションブループリント](platform-and-applications.md)と密接に連携しています。追加の詳細は、Experience Platform と Experience Cloud アプリケーションの間の統合に特有な、[Experience Cloud アプリケーションを使用したオーディエンスとプロファイルのアクティベーションブループリント](platform-and-applications.md)で提供されます。

## ユースケース

* ソーシャルおよび広告の宛先の既知のオーディエンスに対するオーディエンスターゲティング。
* オンラインおよびオフライン属性を使用したオンラインパーソナライズ機能。
* 既知のチャネル（電子メール、SMS など）に対するオーディエンスをアクティブ化。

## アプリケーション

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## アーキテクチャ

### 宛先を使用したオンラインとオフラインのデータのアクティベーション

<img src="assets/online_offline_activation.svg" alt="オンライン／オフラインオーディエンスアクティベーションブループリントの参照アーキテクチャ" style="width:80%; border:1px solid #4a4a4a" />
<br>

## ガードレール

[オーディエンスとプロファイルのアクティベーションの概要ページに説明されているガードレールを参照してください。](overview.md)

## 実装手順

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに[正しい ID および ID 名前空間を設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. Experience Platform に[データを取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ja)。
1. Experience Platform で定義されたオーディエンスが Audience Manager に共有されるように、[Experience Platform と Audience Manager の間の [!UICONTROL Real-time Customer Data Platform の]セグメント共有を](https://www.adobe.com/go/audiences)プロビジョニングします。
1. Experience Platform で[セグメントを作成します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)セグメントをバッチとして、またはストリーミングとして評価するかを、システムが自動的に判定します。
1. プロファイル属性およびオーディエンスメンバーシップを目的の宛先に共有するための[宛先を設定します。](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=ja)

## 実装に関する考慮事項

* プロファイルデータを宛先に共有するには、宛先ペイロードの宛先で使用される特定の ID 値を含める必要があります。ターゲットの宛先に必要な ID は、Platform に取り込まれ、[!UICONTROL リアルタイム顧客プロファイル]の ID として設定される必要があります。

### Real-time Customer Data Platform から Audience Manager へのオーディエンスの共有

* RT-CDP のオーディエンスメンバーシップは、セグメント評価が完了し、セグメント評価がバッチで行われたかストリーミングで行われたかに関わらず、リアルタイム顧客プロファイルに書き込まれるとすぐに、ストリーミング方式で Audience Manager に共有されます。選定されたプロファイルに、関連するプロファイルデバイスの地域ルーティング情報が含まれる場合、RTCDP からのオーディエンスメンバーシップは、関連する Audience Manager エッジ上でストリーミング方式で選定されます。If the regional routing information was applied to a profile with a timestamp in the past 14 days it will be evaluate on the Audience Manager Edge in streaming. If the profiles from RTCDP do not contain regional routing information or the regional routing information is greater than 14 days old, then the profile memberships are sent to the Audience Manager hub location for batch based evaluation and activation. Profiles that are eligible for Edge activation will activate within minutes of segment qualification from RTCDP, profiles that do not qualify for Edge activation will qualify in the Audience Manager hub and may have a 12-24 hour timeframe for processing.

* Regional routing information for which Edge the Audience Manager profile is stored on can be collected to Experience Platform from Audience Manager, the Visitor ID Service, Analytics, Launch, or directly from the Web SDK as a separate profile record class dataset using the &quot;data capture region information&quot; XDM field group.

* Experience Platform から Audience Manager にオーディエンスが共有されるアクティベーションシナリオでは、次の ID が自動的に共有されます。IDFA、GAID、AdCloud、Google、ECID、EMAIL_LC_SHA256。現在、カスタムの名前空間は共有されません。

必須の宛先 ID が[!UICONTROL リアルタイム顧客プロファイル]に含まれている場合、または[!UICONTROL リアルタイム顧客プロファイル]内の ID が Audience Manager でリンクされる必須の宛先 ID と関連付けられる場合、Experience Platform からのオーディエンスは、Audience Manager 宛先を使用して共有できます。

## 関連ドキュメント

* [[!UICONTROL Real-time Customer Data Platform] 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [[!UICONTROL Real-time Customer Data Platform] の概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL Real-time Customer Data Platform] のデモ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
