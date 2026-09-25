---
title: Adobe Customer Journey AnalyticsとAdobe Real-Time CDPの連携
description: Customer Journey Analytics のカスタマージャーニー全体からデータと顧客行動を統合および分析し、CJA から RTCDP にオーディエンスを公開します。
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
TQID: https://experienceleague.adobe.com/gbNXsco0cQIcn5O83ofB-rb0PF65v7kaTZ7mTngqHks
product_v2:
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
    internal-label: Customer Journey Analytics
feature_v2:
  - id: ce577701-5b9e-4fe4-8fa3-4eedea976da4
    internal-label: Components
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 8%
---

# Adobe Customer Journey Analytics

Adobe Customer Journey Analyticsは、Adobe Experience Platformなどのソースからの顧客インタラクションデータを、ジャーニーベースの分析サービスに統合します。 このアーキテクチャでは、クロスチャネル分析、B2B CJA派生、CJAオーディエンスのReal-Time CDPへの公開のためのコアリファレンスを提供します。

## Customer Journey Analytics アーキテクチャ

この図は、接続、データビュー、分析、オーディエンスの作成のために、顧客インタラクションデータをCustomer Journey Analyticsに取り込む主要な流れを示しています。

![Adobe Customer Journey Analytics コアアーキテクチャ &#x200B;](assets/cja.png){width="1000" zoomable="yes"}

## アーキテクチャの派生

- B2B Customer Journey Analyticsは、アカウントベースの分析のために、アカウント、オポチュニティ、購買グループ、人物のディメンションを含むコアアーキテクチャを拡張します。
- CJA オーディエンス共有は、アクティベーションやダウンストリームのジャーニー実行のために、Customer Journey Analyticsから作成されたオーディエンスをReal-Time CDPに公開します。

## プライマリデータフローと統合ポイント

- 顧客インタラクションに関するデータは、web、モバイル、コマース、CRMなどのソースからAdobe Experience Platformに収集されます。
- Experience Platform データセットは、Customer Journey Analytics接続で選択されます。
- データビューでは、クロスチャネル分析のために指標、ディメンション、計算フィールドが表示されます。
- Customer Journey Analytics オーディエンスは、Real-Time CDPに公開してアクティベーションできます。
- Customer Journey Analyticsのインサイトは、専用の統合アーキテクチャを通じて、Journey Optimizerで活用できます。

## サポートされるユースケースパターン

- [B2B分析](/help/blueprints/use-case-patterns/b2b/account-analytics.md) — B2B ディメンションを使用して、アカウント、商談、個人レベルのジャーニーを分析します。
- [顧客分析とinsight generation](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) — クロスチャネルの行動を分析し、ジャーニーのインサイトを生成します。

## 関連トピックス

- [Customer Journey Analyticsの概要](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Customer Journey Analyticsとの連携](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Customer Journey Analytics オーディエンスの公開](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
