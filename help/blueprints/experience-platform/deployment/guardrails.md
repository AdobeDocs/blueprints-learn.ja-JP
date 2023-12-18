---
title: Experience Platform およびアプリケーションガードレール
description: ガードレールは、Adobe Experience Platform およびアプリケーション内のコンポーネントとサービスに対するパフォーマンスの期待値と影響を定義します
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 5a4827244b7d8414b1f1a0bf9b3cd8308bde8c60
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 18%

---

# ガードレール

Guardrails は、Adobe Experience Platformおよびアプリケーションでのデータ、監視された待ち時間、システム使用量に関するガイダンスを提供する推奨しきい値です。 Guardrail は、顧客のアーキテクチャと使用例のパフォーマンスを最適化するために、システムの制約とパフォーマンスに対する期待を反映し、エラーや予期しない結果を回避するのに役立ちます。 Guardrail は、サービスレベル契約に含まれるものではありません。サービスレベル契約は、以下のリンクにある製品の説明と、顧客ライセンス契約に記載されています。 Guardrail は、安定性と実行を確保するために、特定のお客様の使用例に合わせてソリューションを構築する際のガイダンスを提供することを目的としています。

アプリケーションおよび機能に関する特定の SLA(Service Level Agreement) の詳細については、 [アプリケーションと機能の説明](#application-feature-descriptions) 」セクションをクリックします。

厳密な遅延またはボリューム要件を持つお客様の使用例の場合は、Adobeのアカウントチームおよび実装パートナーに使用例の詳細を確認することをお勧めします。 実稼動環境でのデータ取り込みの性質や範囲など、様々な要因が存在するので、使用事例の実装の前に特定の使用例の実装をテストして確認し、期待される動作を観察および理解することをお勧めします。 したがって、使用例の待ち時間とパフォーマンスの要件に従って適切なアーキテクチャと実装を確保するために、期待されるパフォーマンスを事前に確立してテストすることをお勧めします。


## Adobe Experience Platform およびアプリケーションのガードレール参照ドキュメント

以下のページでは、Adobe Experience Platformの機能、サービスおよびアプリケーションのガードレールについて説明します。

**Experience Platform**

* [Real-Time CDP Guardrails の概要](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [Customer Journey Analyticsオーディエンス共有ガードレール](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Customer Journey Analyticsデータ取り込みガードレール](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer Guardrails](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Experience Platformサービス**

* [データ取り込みガードレール](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [Edge Network API ガードレール](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [リアルタイム顧客プロファイルとセグメント化ガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [ID ガードレール](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=ja)
* [クエリサービスガードレール](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ja)
* [宛先のアクティベーションガードレール](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ja)

## エンドツーエンドの待ち時間図 {#end-to-end-latency}

### データ取り込み {#data-ingestion}

次の図に、 [ストリーミング取得](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) および [バッチ取得](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=ja) Real-Time CDPにデータを取り込むとき。 画像をクリックして高解像度バージョンを表示します。

![データ取り込みの概要レベルの視覚的概要。](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "データ取り込みの概要レベルの視覚的概要と待ち時間の値"){width="1000" zoomable="yes"}

### セグメント化 {#segmentation}

次の図は、 [Real-Time CDP segmentation service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ja). 画像をクリックして高解像度バージョンを表示します。

![セグメントの概要レベルの視覚的な概要。](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "セグメントの概要レベルの視覚的概要と待ち時間の値"){width="1000" zoomable="yes"}

### Real-time Customer Data Platform および Adobe Target {#adobe-target-latency}

以下の図に、Real-Time CDPからにオーディエンスを書き出す際に予想される遅延値を示します [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja). 画像をクリックして高解像度バージョンを表示します。

![Adobe Targetへの高レベルの視覚的概要の書き出し。](/help/blueprints/experience-platform/deployment/assets/RTCDP_Target_guardrails.svg "オーディエンスのAdobe Targetの概要レベルのビジュアル概要と待ち時間の値へのエクスポート"){width="1000" zoomable="yes"}

### Customer Journey Analytics {#customer-journey-analytics}

以下の図に、を操作する際に予想される待ち時間の値を示します。 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en). 画像をクリックして高解像度バージョンを表示します。

![Customer Journey Analyticsの概要レベルの視覚的な概要の操作](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Customer Journey Analyticsの概要レベルの視覚的概要と待ち時間の値の使用"){width="1000" zoomable="yes"}

### Journey Optimizer {#journey-optimizer}

以下の図に、を操作する際に予想される待ち時間の値を示します。 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en). 画像をクリックして高解像度バージョンを表示します。

![Adobe Journey Optimizerの概要レベルの視覚的な概要の操作](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Adobe Journey Optimizerの高レベルの視覚的概要と待ち時間の値の使用"){width="1000" zoomable="yes"}

## アプリケーションと機能の説明 {#application-feature-descriptions}

機能固有の SLA(Service Level Agreement) の詳細については、以下の製品説明を参照してください。

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
