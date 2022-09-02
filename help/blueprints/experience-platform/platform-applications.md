---
title: Adobe Experience Platform およびアプリケーションアーキテクチャ図
description: このアーキテクチャ図に、Adobe Experience Platform が他の Adobe Experience Cloud アプリケーションおよびアプリケーションサービスとどのように関わっているかを示します。
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Real-time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 4c66e906b9faf4bd9b1ee75fcf263b8a35d3b782
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 68%

---

# Adobe Experience Platform およびアプリケーション

## Adobe Experience Platform およびアプリケーションアーキテクチャ図

このアーキテクチャ図に、Adobe Experience Platform が Adobe Experience Cloud アプリケーションおよびアプリケーションサービスとどのように関わっているかを示します。

<img src="assets/aep+apps_vertical.svg" alt="Experience Platform およびアプリケーション" style="border:1px solid #4a4a4a; width:90%;" />

## Adobe Experience Platform およびアプリケーションの詳細アーキテクチャ図

<img src="assets/aep+apps_horizontal.svg" alt="Experience Platform およびアプリケーション" style="border:1px solid #4a4a4a; width:90%;" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Adobe Experience Platform および Experience Cloud アプリケーションの統合

<table class="relative-table wrapped" style="width: 100%;">
<colgroup>
<col style="width: 16.0202%;" />
<col style="width: 29.3423%;" />
<col style="width: 33.5582%;" />
<col style="width: 21.0793%;" />
</colgroup>
<tbody>
<tr>
<th>アプリケーション</th>
<th>Experience Platform からアプリケーションへ</th>
<th>アプリケーションから Experience Platform へ</th>
<th>関連するブループリント</th>
</tr>
<tr>
<td colspan="1">Ad Cloud</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform で定義されたオーディエンスは、Audience Manager を使用したターゲティング用に、Ad Cloud と共有できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>現在の統合はありません</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=ja">匿名オーディエンスアクティベーション</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=ja">オンライン／オフラインオーディエンスアクティベーション</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=ja">Experience Platform およびアプリケーションを使用したアクティベーション</a></li>
</ul>
</td>
</tr>
<tr>
<td>Analytics</td>
<td>
<ul>
<li>現在の統合はありません</li>
</ul>
</td>
<td>
<ul>
<li>Analytics によって収集されたデータは、Experience Platform データレイクおよびプロファイルストアに送信できます。<a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ja">Analytics データコネクタ</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=ja">Experience Platform データフロー</a></li>
</ul>
</td>
</tr>
<tr>
<td>Audience Manager</td>
<td>
<ul>
<li>Real-time Customer Data Platform で定義されたオーディエンスは、サードパーティ cookie の宛先に対するアクティベーション用に、Audience Manager と共有できます。</li>
</ul>
</td>
<td>
<ul>
<li>収集されたデータおよび評価されたオーディエンスメンバーシップは、Experience Platform データレイクおよびプロファイルストアと共有できます。<a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ja">Audience Manager ソースコネクタ</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">匿名オーディエンスアクティベーション</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform およびアプリケーションを使用したアクティベーション</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Classic</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform で定義されたオーディエンスは、キャンペーンを開始するために、オーディエンスとして Campaign Classic と共有できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Campaign で収集されたインタラクションおよびキャンペーンデータは、Experience Platformにデータソースとして取り込み、Real-time Customer Data Platformを介したオーディエンスの構築や、Customer Journey AnalyticsおよびExperience Platformクエリサービスを介した分析でさらに使用できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/batch-messaging.html?lang=ja">バッチメッセージ</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Standard</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform で定義されたオーディエンスは、キャンペーンを開始するために、オーディエンスとして Campaign Standard と共有できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Campaign で収集されたインタラクションおよびキャンペーンデータは、Experience Platformにデータソースとして取り込み、Real-time Customer Data Platformを介したオーディエンスの構築や、Customer Journey AnalyticsおよびExperience Platformクエリサービスを介した分析でさらに使用できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/batch-messaging.html?lang=en">バッチメッセージ</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Customer Journey Analytics</td>
<td colspan="1">
<ul>
<li>Experience Platform データレイクに収集され、取り込まれたデータは、Customer Journey Analytics で処理できるようになります。 </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>顧客ジャーニー分析でオーディエンスを構築し、オーディエンスの結果をReal-time Customer Data Platformと共有します。 <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=en">CJA オーディエンスの公開</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=ja">Real-time Customer Data Platform を使用した</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Experience Manager</td>
<td colspan="1">
<ul>
<li>Experience Platform プロファイルは、サーバーサイドに直接アクセスして、Experience Manager を使用して配信された、パーソナライズされたエクスペリエンスを強化できます。パーソナライゼーションアクティビティは、通常 Target 統合を通じて、Experience Manager で配信されることに注意してください。 </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Experience Manager Sites で実行される現在の統合、行動およびインタラクションは、Experience Platform Web および Mobile SDK では直接収集されません。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Journey Optimizer</td>
<td colspan="1">
<ul>
<li>Experience Platform に取り込まれたデータイベントおよびプロファイルは、Journey Optimizer でジャーニーを開始および強化するために Journey Optimizer で使用できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Journey Optimizerで生成されたインタラクションとキャンペーンのデータは、Real-time Customer Data Platformを介したオーディエンスの構築や、Customer Journey AnalyticsおよびExperience Platformクエリサービスを介した分析でさらに使用できるように、Experience Platformに収集されます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=ja">Journey Optimizer</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Magento</td>
<td colspan="1">
<ul>
<li>現在の統合はありません</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Magentoにネイティブなデータは、Magentoソースコネクタを介してExperience Platformに送信できます。 </li>
</ul>
</td>
<td colspan="1">現在の統合はありません</td>
</tr>
<tr>
<td colspan="1">Marketo</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform で定義されたオーディエンスは、Marketo キャンペーンを開始したり、Marketo オブジェクトを更新したりするために、オーディエンスとして Marketo と共有できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Marketoのアカウント、連絡先、商談データは、Marketoが生成したインタラクションおよびキャンペーンデータと共にExperience Platformに取り込まれ、B2B-CDP を介したオーディエンス構築や、Customer Journey AnalyticsおよびExperience Platformクエリサービスを介した分析でさらに使用できます。<a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=ja">Marketo Engage コネクタ</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li>B2B アクティベーション - 開発中</li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Real-time CDP</td>
<td colspan="1">
<ul>
<li>Experience Platform に取り込まれ、収集されたデータは、Real-time Customer Data Platform を強化するリアルタイム顧客プロファイルを構築するためのデータソースです。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>オーディエンスおよびプロファイル指標は、プロファイルインサイトレポートダッシュボードを強化するために、Experience Platform データレイクに送信されます。</li>
<li>データレイクのオーディエンスとプロファイルデータは、クエリサービスとCustomer Journey Analyticsを通じてさらにインサイトを得るために使用できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform およびアプリケーションを使用したアクティベーション</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Target</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platformで定義されたオーディエンスとプロファイル属性は、Target と共有し、Target が提供するパーソナライゼーションおよびターゲティングエクスペリエンスで使用できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Target のエクスペリエンスおよびインタラクション用に収集されたデータは、Web/Mobile SDKExperience Platformを通じてExperience Platformに収集できます。 このデータは、Real-time Customer Data Platformを介したオーディエンス構築で、また、Customer Journey AnalyticsおよびExperience Platformクエリサービスを介した分析に使用できます。</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform およびアプリケーションを使用したアクティベーション</a></li>
</ul>
</td>
</tr>
</tbody>
</table>