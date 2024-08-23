---
title: Experience Platform およびアプリケーションガードレール
description: ガードレールは、Adobe Experience Platform およびアプリケーション内のコンポーネントとサービスに対するパフォーマンスの期待値と影響を定義します
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 164793e15315d64cf38cb14928eac10cf6ae5c35
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 15%

---

# ガードレール

ガードレールは、Adobe Experience Platformやアプリケーションでデータ、観測された待ち時間、システムの使用状況に関するガイダンスを提供する、推奨されるしきい値です。 ガードレールは、システムの制約やパフォーマンスの期待を反映して、顧客のアーキテクチャやユースケースのパフォーマンスを最適化し、エラーや予期しない結果を避けるのに役立ちます。 ガードレールは、SLA （Service Level Agreement）を目的としたものではありません。SLA （Service Level Agreement）は、以下にリンクされている製品説明およびお客様のライセンス契約に記載されています。 ガードレールは、安定性と実行を確保するために、特定のお客様のユースケースに対応するソリューションを構築する際のガイダンスを提供することを目的としています。

アプリケーションおよび機能に関する特定の SLA （Service Level Agreement）については、このページの下部にある [ アプリケーションと機能の説明 ](#application-feature-descriptions) セクションを参照してください。

厳密な待ち時間またはボリュームの要件があるAdobeのユースケースの場合、アドビでは、Adobeアカウントチームおよび実装パートナーと詳細にユースケースを確認することをお勧めします。 場合によっては、ユースケースの実稼動版のローンチ前に、特定のユースケースの実装をテストして観察し、期待される動作を観察して理解することをお勧めします。お客様の各実装には、データ取り込みの性質とケイデンス、構築されるセグメントルールの詳細、様々なアクティベーションチャネルとペイロードなど、様々な要因があるからです。各ユースケースの実装は、様々なパフォーマンスを持ちます。 そのため、想定されるパフォーマンスを事前に確立およびテストして、ユースケースの待ち時間とパフォーマンスの要件に従って適切なアーキテクチャと実装を確認することをお勧めします。


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

## アプリケーションと機能の説明 {#application-feature-descriptions}

機能固有の SLA （Service Level Agreement）については、以下の製品の説明を参照してください。

* [Experience Platform Collection Enterprise](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-collection-enterprise.html)
* [Real-time Customer Data Platform](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [B2B 顧客データ Platform](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-b2b.html)
* [Experience Platform Activation](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform0.html)
* [Experience Platform インテリジェンス](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [インテリジェントサービス](https://helpx.adobe.com/jp/legal/product-descriptions/intelligent-services.html)
* [Data Distiller](https://helpx.adobe.com/jp/legal/product-descriptions/data-distiller.html)
* [Customer Journey Analytics](https://helpx.adobe.com/jp/legal/product-descriptions/customer-journey-analytics.html)
* [Journey Optimizer](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer.html)
* [Journey Orchestration](https://helpx.adobe.com/jp/legal/product-descriptions/journey-orchestration.html)
* [Offer Decisioning](https://helpx.adobe.com/jp/legal/product-descriptions/offer-decisioning-app-service.html)
