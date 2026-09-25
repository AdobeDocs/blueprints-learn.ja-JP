---
title: Adobe Customer Journey AnalyticsとAdobe Journey Optimizerの統合
description: Adobe Customer Journey AnalyticsでAdobe Journey Optimizerのキャンペーンとジャーニーのインサイトを分析し、オーディエンスを公開してジャーニーを展開するためのアーキテクチャ。
solution: Customer Journey Analytics, Journey Optimizer, Experience Platform
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%
---
# Adobe Customer Journey AnalyticsとAdobe Journey Optimizerの統合

このアーキテクチャでは、Adobe Journey Optimizerの配信データとインタラクションデータが、Adobe Experience Platformを通じてCustomer Journey Analyticsに流れ込み、キャンペーンとジャーニーのインサイトを得る方法を示します。 Customer Journey Analyticsで作成されたオーディエンスは、Real-Time CDPを通じて公開し、Journey Optimizerで使用できます。

## キャンペーンとジャーニーのインサイトのアーキテクチャ

Journey Optimizerの配信データとインタラクションデータを、Experience PlatformおよびCustomer Journey Analyticsと連携させ、レポート、分析、オーディエンスを作成できます。

![Adobe Customer Journey AnalyticsとAdobe Journey Optimizerの統合アーキテクチャ &#x200B;](assets/cja_ajo_integration.png){width="1000" zoomable="yes"}

## プライマリデータフローと統合ポイント

- Journey Optimizerの配信、インタラクション、有効性データは、Experience Platformデータサービスに共有されます。
- Experience Platformのデータは、CJA接続を通じてCustomer Journey Analyticsに取り込まれます。
- Customer Journey Analyticsのデータビューと分析機能は、adobe campaignとadobe journey insightを提供します。
- Customer Journey Analyticsで作成されたオーディエンスは、Real-Time CDPに公開されます。
- Real-Time CDP オーディエンスは、Journey Optimizer ジャーニーの実行とパーソナライゼーションに使用できます。

## サポートされるユースケースパターン

- [顧客分析とinsight generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) — チャネル全体でキャンペーンとジャーニーの動作を分析します。
- [&#x200B; イベント トリガーのメッセージ &#x200B;](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) – 顧客およびジャーニーのシグナルを使用して、オーケストレーションされたメッセージをサポートします。

## 関連トピックス

- [Journey Optimizer レポート](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/reports/sharing-overview)
- [Customer Journey Analyticsの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Customer Journey Analytics オーディエンスの公開](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
