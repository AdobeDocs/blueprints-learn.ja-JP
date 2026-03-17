---
title: Customer Experience Orchestration のユースケース、アーキテクチャ図、ブループリント
description: Adobe Experience Platformとアプリケーションの主なビジネス目標、ユースケースのパターン、業界のユースケースを確認します。 ビジュアルアーキテクチャの図とブループリントは、システム統合、データフロー、ソリューション設計のテクニカルリファレンスを提供し、ビジネス価値を実装に結び付けます。
doc-type: overview-page
exl-id: 52898310-9723-4ec2-ba10-f45fefe29e93
source-git-commit: 63154ca158b773287f0d1a7f88a81ac3181c43a0
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 2%

---

# カスタマーエクスペリエンスオーケストレーションのビジネスオブジェクト、ユースケース、アーキテクチャ図

このサイトには **主要なビジネス目標** が含まれています。この目標は、Adobe Experience Platformおよびアプリケーションで実現できる主要なビジネス価値および目標の例を示しています。**ユースケースパターン** 繰り返し可能な実装アプローチを使用した、プラットフォームとアプリケーションの一般的な機能の説明。**業界の使用例** 垂直固有のビジネスシナリオにパターンを適用します。**アーキテクチャ図とブループリントは** システム統合ポイント、データとコンテンツのフロー、操作のシーケンスを示す視覚的なアーキテクチャ図とデータフロー参照図で、ソリューション設計の技術的なリファレンスを提供します。 これらのレイヤーを組み合わせることで、ビジネス価値が実装の依存関係やアーキテクチャに結び付けられます。

## 主なビジネス目標

組織がデジタルエクスペリエンスイニシアチブを通じて達成しようとする戦略的成果。 各目標は、Adobe Experience Platformとアプリケーションの実装方法を説明するユースケースパターンにマッピングされます。

<table>
<tr>
  <td><a href="business-objectives/overview.md#acquisition--growth"><strong>獲得と成長</strong></a></td>
  <td><a href="business-objectives/overview.md#revenue--monetization"><strong>収益と収益化</strong></a></td>
  <td><a href="business-objectives/overview.md#cost--efficiency"><strong>コストと効率</strong></a></td>
</tr>
<tr>
  <td><a href="business-objectives/overview.md#customer-experience"><strong>顧客体験</strong></a></td>
  <td><a href="business-objectives/overview.md#analytics--insights"><strong>分析とインサイト</strong></a></td>
  <td><a href="business-objectives/overview.md#qualification--sales-b2b"><strong>選定およびセールス（B2B）</strong></a></td>
</tr>
</table>

[すべてのビジネス目標を表示](business-objectives/overview.md)

## ユースケースパターン

特定の機能、その機能を実現するファンクションチェーン、関連するアプリケーションを説明する、繰り返し可能な実装アプローチ。

<table>
<tr>
  <td><a href="use-case-patterns/overview.md#audience-building--activation"><strong>オーディエンスの構築とアクティベーション</strong></a></td>
  <td><a href="use-case-patterns/overview.md#personalization"><strong>パーソナライズ機能</strong></a></td>
  <td><a href="use-case-patterns/overview.md#campaign-management--orchestration"><strong>キャンペーンの管理とオーケストレーション</strong></a></td>
</tr>
<tr>
  <td><a href="use-case-patterns/overview.md#analysis"><strong>分析</strong></a></td>
  <td><a href="use-case-patterns/overview.md#conversational-experience"><strong>会話経験</strong></a></td>
  <td></td>
</tr>
</table>

[すべてのユースケースパターンの表示](use-case-patterns/overview.md)

## 業界別に調査

特定の業界に合わせてカスタマイズされたユースケースで、実装パターンやビジネス目標にマッピングするもの。

<table>
<tr>
  <td><a href="industry-use-cases/retail/retail-overview.md"><strong>小売</strong></a></td>
  <td><a href="industry-use-cases/financial-services/financial-services-overview.md"><strong>金融サービス</strong></a></td>
  <td><a href="industry-use-cases/healthcare/healthcare-overview.md"><strong>ヘルスケア</strong></a></td>
</tr>
<tr>
  <td><a href="industry-use-cases/automotive/automotive-overview.md"><strong>自動車用</strong></a></td>
  <td><a href="industry-use-cases/travel-hospitality/travel-hospitality-overview.md"><strong>旅行およびホスピタリティ</strong></a></td>
  <td><a href="industry-use-cases/telecommunications/telecommunications-overview.md"><strong>通信</strong></a></td>
</tr>
<tr>
  <td><a href="industry-use-cases/media-entertainment/media-entertainment-overview.md"><strong>メディアとエンターテイメント</strong></a></td>
  <td><a href="industry-use-cases/insurance/insurance-overview.md"><strong>保険</strong></a></td>
  <td><a href="industry-use-cases/b2b/b2b-overview.md"><strong>B2B</strong></a></td>
</tr>
</table>

[業界のすべてのユースケースを表示](industry-use-cases/use-case-catalog.md)

## アーキテクチャ図とブループリント

Adobe Experience Platformとアプリケーションのシステム統合ポイント、データとコンテンツのフロー、および操作のシーケンスを示したビジュアルアーキテクチャとデータフローのリファレンス図です。

<table>
<tr>
  <td>
    <a href="experience-platform/guardrails.md">
      <img alt="Experience Platform Hub とEdgeのアーキテクチャ" src="experience-platform/assets/aep_edge_hub_latency_v1.svg" />
    </a>
    <div>
      <a href="experience-platform/guardrails.md">
    <strong>Experience Platform ハブとEdgeのアーキテクチャとガードレールの図 </strong>
    </a>
    </div>
  </td>
   <td>
    <a href="experience-platform/deployment/websdk.md">
      <img alt="Edge シーケンス図" src="experience-platform/deployment/assets/web_sdk_sequence.svg" />
    </a>
    <div>
      <a href="experience-platform/deployment/websdk.md">
    <strong>Web SDKとEdge Networkのシーケンス図 </strong>
    </a>
    </div>
  </td>
  <td>
    <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
      <img alt="Journey Optimizerの概要図" src="customer-journeys/journey-optimizer/images/ajo-architecture.svg" />
    </a>
    <div>
      <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
    <strong>Adobe Journey Optimizerの概要図 </strong>
    </a>
    </div>
  </td>
</tr>
</table>