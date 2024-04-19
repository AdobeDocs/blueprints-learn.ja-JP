---
title: オーディエンスおよびプロファイルのアクティベーションのブループリント
description: Real-time Customer Data Platform を使用して、オーディエンスがアクティブでプロファイル中心の顧客エクスペリエンスを提供します。
solution: Real-Time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
source-git-commit: 62dc3dff69bbf88b025373b4fdc893cc77b73594
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 76%

---


# オーディエンスおよびプロファイルのアクティベーションのブループリント

データドリブン型マーケティングでは、オーディエンスとプロファイルのアクティベーションが成功のカギです。ただし、多くのブランドでは、依然としてチャネルファーストのアクティベーションに注力し、多くの場合、リーチやパーソナライズ機能に一貫性がありません。

チャネルファーストのアプローチでは、各チャネルは他チャネルと連携せずに機能し、パーソナライズの取り組みは、そのチャネルのブランドとやり取りする顧客のみをターゲットにします。このアプローチは、顧客が多くの異なるタッチポイントをまたいでブランドとやり取りしているという現実を反映していません。オーディエンスとプロファイルのアクティベーションでは、ブランドは、複数のチャネルをまたいで顧客インタラクションを結びつけ、すべてのチャネルに対してアクティベーションできる一元化されたプロファイルとオーディエンスを実現できます。

オーディエンスとプロファイルのアクティベーションのブループリント

- [匿名オーディエンスアクティベーション](/help/blueprints/audience-activation/anonymous.md)
- 既知のカスタマーアクティベーション（RTCDP）
   - [概要](/help/blueprints/audience-activation/known.md)
   - [ソーシャルおよび広告チャネルに対するアクティベーション](/help/blueprints/audience-activation/advertising-activation.md)
   - [ファイルおよびエンタープライズストリーミング宛先に対するアクティベーション](/help/blueprints/audience-activation/enterprise-destinations.md)
   - [顧客アクティビティハブ](/help/blueprints/audience-activation/customer-activity.md)
   - [セグメントの一致](/help/blueprints/audience-activation/segment-match.md)
   - [Experience Cloudアプリケーションを使用したアクティベーション](/help/blueprints/audience-activation/platform-and-applications.md)


## リアルタイム顧客プロファイルアーキテクチャ

以下の図に、Experience Platform のリアルタイム顧客プロファイルのコアコンポーネントの概要を示します。

プロファイル、セグメント化、アクティベーションに関連するその他のドキュメントについては、 [RTCDP 概要ドキュメント](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/home) および [リアルタイム顧客プロファイルの概要](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home) ページ。

<img src="assets/profile_architecture.jpg" alt="リアルタイム顧客プロファイルの参照アーキテクチャ" style="border:1px solid #4a4a4a" width="90%"  class="modal-image"/>

## オーディエンスとプロファイルのアクティベーションブループリントのガードレール

* ガードレールの詳細とエンドツーエンドの遅延については、[デプロイメントガードレールドキュメント](../experience-platform/deployment/guardrails.md)および[プロファイルとセグメント化ガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)を参照してください。