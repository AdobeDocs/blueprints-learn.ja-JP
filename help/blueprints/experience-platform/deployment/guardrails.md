---
title: Experience Platform およびアプリケーションガードレール
description: ガードレールは、Adobe Experience Platform およびアプリケーション内のコンポーネントとサービスに対するパフォーマンスの期待値と影響を定義します
solution: Experience Platform, Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: f8b9cc115739b53bba71d06b228dcce57df9dd7b
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 10%

---


# ガードレール

ガードレールは、システムの制約、予想される待ち時間、パフォーマンスの期待を反映して、顧客のアーキテクチャとユースケースのパフォーマンスを最適化し、安定性を確保してエラーや予期しない結果を避けるのに役立ちます。

## ガードレールのタイプ

| ガードレール タイプ | 説明 |
|---|---|
| パフォーマンスガードレール（ソフトリミット） | パフォーマンスガードレールは、ユースケースのスコープに関連する使用制限で、通常の条件下で期待されるパフォーマンスの概要を示します。 この値を超えると、パフォーマンスの低下や待ち時間が発生する場合があります。 パフォーマンスガードレールは、以下に概説されているように、各ソリューションのガードレールのセクションの下にあるExperience Leagueドキュメントに記載されています。 |
| 静的制限（ハードリミット） | これらは、超過できないシステムによって適用される制限です。 静的制限は、通常、顧客の契約および [ 製品の説明 ](https://helpx.adobe.com/legal/product-descriptions.html) で契約的に結ばれ、概要が説明されています。 |

>[!NOTE]
>
> ガードレールは、SLA （Service Level Agreement）ではなく、最適な設定と期待されるシステム動作のガイダンスを目的としています。 システム上または契約上の制限や SLA （Service Level Agreement）に該当するガードレールは、お客様の契約および製品の説明に特別に記載されています。 カスタムの上限について知りたい場合は、カスタマーケア担当者にお問い合わせください。

>[!NOTE]
>
> 待ち時間が厳密なユースケースやパフォーマンスニーズがある場合は、Adobeは詳細についてAdobeアカウントチームや実装パートナーと話し合うことをお勧めします。 各顧客の設定は、データ取り込みパターン、プロファイル数とリッチネス、セグメントルール、アクティベーションチャネルによって異なる場合があります。 したがって、ユースケースを構築およびテストして、そのパフォーマンスを最適化し、期待されるパフォーマンス特性を完全に理解することが重要です。

## Adobe Experience Platform およびアプリケーションのガードレール参照ドキュメント

次のページでは、Adobe Experience Platformの機能、サービスおよびアプリケーションのガードレールについて説明します。

**Experience Platformアプリケーション**

* [Real-Time CDP ガードレールの概要 ](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Customer Journey Analyticsオーディエンス共有ガードレール ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Customer Journey Analyticsデータ取り込みガードレール ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizerガードレール ](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Experience Platformサービス**

* [データ取り込みガードレール](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [[!DNL Edge Network] API ガードレール ](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [ リアルタイム顧客プロファイルとセグメント化ガードレール ](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [ID ガードレール](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=ja)
* [クエリサービスガードレール](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ja)
* [宛先のアクティベーションガードレール](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ja)

## エンドツーエンドの待ち時間図 {#end-to-end-latency}

### Experience PlatformEdge Networkとハブプライマリで発生した待ち時間 {#edge-hub-latencies}

次の図は、Experience Platformとアプリケーションでユースケースを構築する際に注意する必要がある、主要なエッジとハブで観測された待ち時間を示しています。

![Experience Platform [!DNL Edge Network] とハブ プライマリで観察された待ち時間。](/help/blueprints/experience-platform/deployment/assets/aep_edge_hub_latency_v1.svg "Experience PlatformEdge Networkとハブのプライマリ監視待ち時間 "){width="1000" zoomable="yes"}

### データ取り込み {#data-ingestion}

次の図は、データをReal-Time CDPに取り込む際に、[ ストリーミング取り込み ](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) および [ バッチ取り込み ](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=ja) を通じて予測されるデータ取り込み待ち時間の値を示しています。 画像をクリックすると、高解像度バージョンが表示されます。

![ データ取り込みの全体的なビジュアル概要。](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg " データ取り込みの大まかな視覚的な概要と待ち時間の値 "){width="1000" zoomable="yes"}

### セグメント化 {#segmentation}

次の図は、[Real-Time CDP セグメント化サービス ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja) でオーディエンスを操作する際に予想される待ち時間の値を示しています。 画像をクリックすると、高解像度バージョンが表示されます。

![ セグメント化の全体的なビジュアルの概要。](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg " セグメント化の大まかな視覚的な概要と待ち時間の値 "){width="1000" zoomable="yes"}

### Real-time Customer Data Platformと [!DNL Edge Network] {#adobe-edge-latency}

次の図は、[!DNL Edge Network] を活用する際に予想される待ち時間の値を示しています。例えば、[Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja) で RTCDP オーディエンスを活用する場合です。 画像をクリックすると、高解像度バージョンが表示されます。

![Adobe Edge ネットワークとExperience Platformの概要：視覚的な概要](/help/blueprints/experience-platform/deployment/assets/RTCDP_Edge_guardrails.svg "Adobe Targetへのオーディエンスの書き出しの概要と待ち時間 "){width="1000" zoomable="yes"}

### Customer Journey Analytics {#customer-journey-analytics}

次の図は、[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en) を使用する場合に期待される待ち時間の値を示しています。 画像をクリックすると、高解像度バージョンが表示されます。

![Customer Journey Analyticsの操作の全体的なビジュアル概要。](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Customer Journey Analyticsの大まかなビジュアル概要と待ち時間の値の操作 "){width="1000" zoomable="yes"}

### Journey Optimizer {#journey-optimizer}

次の図は、[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en) を使用する場合に予想される待ち時間の値を示しています。 画像をクリックすると、高解像度バージョンが表示されます。

![Adobe Journey Optimizerの操作の全体的なビジュアルの概要。](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Adobe Journey Optimizerの大まかなビジュアル概要と待ち時間の値の操作 "){width="1000" zoomable="yes"}