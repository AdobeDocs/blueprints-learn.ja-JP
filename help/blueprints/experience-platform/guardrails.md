---
title: Experience Platform およびアプリケーションガードレール
description: ガードレールは、Adobe Experience Platform およびアプリケーション内のコンポーネントとサービスに対するパフォーマンスの期待値と影響を定義します
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 13%

---


# ガードレール

ガードレールは、システムの制約、予想される待ち時間、パフォーマンスの期待を反映して、顧客のアーキテクチャとユースケースのパフォーマンスを最適化し、安定性を確保してエラーや予期しない結果を避けるのに役立ちます。

## ガードレールのタイプ

| ガードレール タイプ | 説明 |
|---|---|
| パフォーマンスガードレール（ソフトリミット） | パフォーマンスガードレールは、ユースケースのスコープに関連する使用制限で、通常の条件下で期待されるパフォーマンスの概要を示します。 この値を超えると、パフォーマンスの低下や待ち時間が発生する場合があります。 パフォーマンスガードレールは、以下に示すように、各ソリューションのガードレールの節の下にあるExperience League ドキュメントに記載されています。 |
| 静的制限（ハードリミット） | これらは、超過できないシステムによって適用される制限です。 静的制限は、通常、顧客の契約および [ 製品の説明 ](https://helpx.adobe.com/jp/legal/product-descriptions.html) で契約的に結ばれ、概要が説明されています。 |

>[!NOTE]
>
> ガードレールは、SLA （Service Level Agreement）ではなく、最適な設定と期待されるシステム動作のガイダンスを目的としています。 システム上または契約上の制限や SLA （Service Level Agreement）に該当するガードレールは、お客様の契約および製品の説明に特別に記載されています。 カスタムの上限について知りたい場合は、カスタマーケア担当者にお問い合わせください。

>[!NOTE]
>
> 待ち時間が厳密なユースケースやパフォーマンスニーズがある場合は、AdobeのAdobe アカウントチームや実装パートナーと詳細について話し合うことをお勧めします。 各顧客の設定は、データ取り込みパターン、プロファイル数とリッチネス、セグメントルール、アクティベーションチャネルによって異なる場合があります。 したがって、ユースケースを構築およびテストして、そのパフォーマンスを最適化し、期待されるパフォーマンス特性を完全に理解することが重要です。

## Adobe Experience Platform およびアプリケーションのガードレール参照ドキュメント

次のページでは、Adobe Experience Platformの機能、サービスおよびアプリケーションのガードレールについて説明します。

**Experience Platform アプリケーション**

* [Real-Time CDP ガードレールの概要 ](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html?lang=ja)
* [Customer Journey Analytics オーディエンス共有ガードレール ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ja#latency)
* [Customer Journey Analytics データ取り込みガードレール ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ja#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizerガードレール ](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=ja)

**Experience Platform サービス**

* [データ取り込みガードレール](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=ja)
* [[!DNL Edge Network] API ガードレール ](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html?lang=ja)
* [ リアルタイム顧客プロファイルとセグメント化ガードレール ](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [ID ガードレール](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=ja)
* [クエリサービスガードレール](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ja)
* [宛先のアクティベーションガードレール](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ja)

## エンドツーエンドの待ち時間図 {#end-to-end-latency}

### Experience Platform Edge Networkとハブプライマリで遅延が発生しました {#edge-hub-latencies}

次の図は、Experience Platformとアプリケーションでユースケースを構築する際に注意する必要がある、プライマリエッジとハブで観測された待ち時間を示しています。

![Experience Platform [!DNL Edge Network] とハブ プライマリで観察された待ち時間。](/help/blueprints/experience-platform/assets/aep_edge_hub_latency_v1.svg "Experience Platform Edge Networkと hub のプライマリ監視待ち時間 "){width="1000" zoomable="yes"}