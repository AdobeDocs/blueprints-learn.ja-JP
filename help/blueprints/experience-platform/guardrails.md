---
title: Experience Platform およびアプリケーションガードレール
description: ガードレールは、Adobe Experience Platform およびアプリケーション内のコンポーネントとサービスに対するパフォーマンスの期待値と影響を定義します
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
TQID: https://experienceleague.adobe.com/ZSHbFR3sEy4C-876IU3yN8U5vOUVvDWIP-O3l-wKm78
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2: id: d1823595-9241-4128-8a33-e4ac3bf08773id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74id: ee602049-8a18-43df-9299-a689a025a371
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a99add31cc9f485db119ca00426798545e6a7316
workflow-type: tm+mt
source-wordcount: 486
ht-degree: 14%

---

# ガードレール

ガードレールには、システムの制約、予想される遅延、パフォーマンスへの期待が反映されており、顧客アーキテクチャとユースケースのパフォーマンスを最適化し、安定性を確保し、エラーや予期しない結果を回避するのに役立ちます。

## ガードレールの種類

| ガードレール型 | 説明 |
|---|---|
| パフォーマンスガードレール（ソフトリミット） | パフォーマンスガードレールとは、ユースケースの範囲に関連し、通常の条件下で期待されるパフォーマンスを概説する使用制限です。 これを超えると、パフォーマンスの低下や遅延が発生する場合があります。 パフォーマンスガードレールは、以下に概説するように、各ソリューションのガードレールのセクションの下にあるExperience League ドキュメントに記載されています。 |
| 静的制限（ハードリミット） | これらは、超過できないシステムによって強制される制限です。 静的制限は通常、契約上拘束され、顧客契約および[製品説明](https://helpx.adobe.com/legal/product-descriptions.html)に概説されています。 |

>[!NOTE]
>
> ガードレールは、サービスレベル契約ではなく、最適な構成と想定されるシステム動作に関するガイダンスです。 システムまたは契約上の制限またはサービスレベル契約であるガードレールは、顧客契約および製品説明に具体的に記載されます。 カスタム制限について詳しくは、カスタマーケア担当者にお問い合わせください。

>[!NOTE]
>
> 遅延やパフォーマンスに関して厳格なニーズがあるユースケースについては、Adobeのアカウントチームと導入パートナーと詳細について話し合うことを推奨しています。 各顧客の設定は、データ取り込みパターン、プロファイル数とリッチネス、セグメントルール、アクティベーションチャネルによって異なります。 そのため、ユースケースを構築してテストすることで、パフォーマンスを最適化し、期待されるパフォーマンス特性を完全に把握することが重要です。

## Adobe Experience Platform およびアプリケーションのガードレール参照ドキュメント

次のページでは、Adobe Experience Platformの機能、サービス、アプリケーションに関するガードレールについて説明します。

**Experience Platform アプリケーション**

* [Real-Time CDP ガードレールの概要](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Customer Journey Analyticsのオーディエンス共有のガードレール](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Customer Journey Analytics データ取り込みのガードレール](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizerのガードレール](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Experience Platform サービス**

* [データ取り込みのガードレール](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network]個のAPI ガードレール](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [リアルタイムの顧客プロファイルとセグメンテーションガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [IDのガードレール](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=ja)
* [クエリサービスガードレール](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ja)
* [宛先アクティベーションガードレール](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ja)

## エンドツーエンドの待ち時間図 {#end-to-end-latency}

### Experience Platform Edge Networkとハブプライマリの観測された遅延 {#edge-hub-latencies}

次の図は、Experience Platformおよびアプリケーションでユースケースを構築する際に認識する、プライマリエッジおよびハブで観察される遅延を示しています。

![Experience Platform [!DNL Edge Network]およびハブ プライマリ監視の遅延。](/help/blueprints/experience-platform/assets/aep_edge_hub_latency_v1.svg "Experience Platform Edge Networkおよびハブ プライマリ監視の遅延"){width="1000" zoomable="yes"}