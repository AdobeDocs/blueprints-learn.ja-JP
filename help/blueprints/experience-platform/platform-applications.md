---
title: Adobe Experience Platform およびアプリケーションアーキテクチャ図
description: このアーキテクチャ図に、Adobe Experience Platform が他の Adobe Experience Cloud アプリケーションおよびアプリケーションサービスとどのように関わっているかを示します。
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Offer Decisioning, Real-time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 6c4b72159d4ba2a171215678e4e4842956d82745
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 11%

---

# Adobe Experience Platform およびアプリケーション

## Adobe Experience Platform およびアプリケーションアーキテクチャ図

このアーキテクチャ図に、Adobe Experience Platform が Adobe Experience Cloud アプリケーションおよびアプリケーションサービスとどのように関わっているかを示します。

<img src="assets/aep+apps_vertical.svg" alt="Experience Platform およびアプリケーション" style="border:1px solid #4a4a4a; width:80%;" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Adobe Experience Platform およびアプリケーションの詳細アーキテクチャ図

<img src="assets/aep+apps_horizontal.svg" alt="Experience Platform およびアプリケーション" style="border:1px solid #4a4a4a; width:80%;" />

## Adobe Experience PlatformとExperience Cloudアプリケーションの統合

<table class="relative-table wrapped" style="width: 100%;" >
   <colgroup>
    <col style="width: 16.0202%;"/>
    <col style="width: 29.3423%;"/>
    <col style="width: 33.5582%;"/>
    <col style="width: 21.0793%;"/>
  </colgroup>
  <tbody>
    <tr>
      <th>適用</th>
      <th>Experience Platform</th>
      <th>Experience Platform</th>
      <th>関連するブループリント</th>
    </tr>
    <tr>
      <td colspan="1">Ad Cloud</td>
      <td colspan="1">
        <ul>
          <li>リアルタイム顧客データプラットフォームで定義されたオーディエンスは、Ad Cloudと共有して、Audience Managerを介したターゲティングをおこなうことができます。</li>
        </ul>
      </td>
      <td colspan="1">現在の統合はありません</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">匿名オーディエンスアクティベーション</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platformとアプリケーションを使用したアクティベーション</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Analytics</td>
      <td>現在の統合はありません</td>
      <td>
        <ul>
          <li>Analyticsが収集したデータは、Experience Platformデータレイクとプロファイルストアに送信できます。 <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en">Analytics Data Connector</a>
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=en">Experience Platformデータフロー</a>
          </li>
        </ul>
        <p>
          <br/>
        </p>
      </td>
    </tr>
    <tr>
      <td>Audience Manager</td>
      <td>
        <ul>
          <li>リアルタイム顧客データプラットフォームで定義されたオーディエンスは、サードパーティCookieの宛先に対してアクティブ化するために、Audience Managerに共有できます。</li>
        </ul>
      </td>
      <td>
        <ul>
          <li>収集および評価されたオーディエンスメンバーシップは、Experience Platformデータレイクとプロファイルストアに共有できます。 <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en">Audience Manager ソースコネクタ</a>
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">匿名オーディエンスアクティベーション</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platformとアプリケーションを使用したアクティベーション</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Campaign Classic</td>
      <td colspan="1">
        <ul>
          <li>リアルタイム顧客データプラットフォームで定義されたオーディエンスは、キャンペーンを開始するオーディエンスとしてCampaign Classicに共有できます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Campaignで収集されたインタラクションおよびキャンペーンデータは、リアルタイム顧客データプラットフォームを介したExperience Platform構築や、Customer Journey AnalyticsおよびExperience PlatformクエリサービスとData Science Workspaceを介した分析でさらに使用するために、データソースとしてオーディエンスに取り込みます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/batch-messaging.html?lang=en">バッチメッセージ</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Campaign Standard</td>
      <td colspan="1">
        <ul>
          <li>リアルタイム顧客データプラットフォームで定義されたオーディエンスは、キャンペーンを開始するオーディエンスとしてCampaign Standardに共有できます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Campaignで収集されたインタラクションおよびキャンペーンデータは、リアルタイム顧客データプラットフォームを介したExperience Platform構築や、Customer Journey AnalyticsおよびExperience PlatformクエリサービスとData Science Workspaceを介した分析でさらに使用するために、データソースとしてオーディエンスに取り込みます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/batch-messaging.html?lang=en">バッチメッセージ</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Customer Journey Analytics</td>
      <td colspan="1">
        <ul>
          <li>収集され、Experience Platformデータレイクに取り込まれたデータは、Customer Journey Analyticsへの処理に使用できます。 </li>
        </ul>
      </td>
      <td colspan="1">現在使用できる統合はありません。 オーディエンスの結果をCustomer Journey AnalyticsからExperience Platformに共有する機能は、ロードマップに追加されています。</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=en">Customer Journey Analytics </a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Adobe Experience Manager</td>
      <td colspan="1">
        <ul>
          <li>Experience Platformプロファイルは、サーバー側から直接アクセスして、Experience Managerを通じて提供されるパーソナライズされたエクスペリエンスを強化できます。 パーソナライゼーションアクティビティは、最も一般的に、Target統合を通じてExperience Managerを介して提供されます。 </li>
        </ul>
      </td>
      <td colspan="1">現在の統合、Experience Managerサイトで実行されるビヘイビアーとインタラクションは、Experience PlatformWebおよびMobile SDKを介して直接収集されます。</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Journey Optimizer</td>
      <td colspan="1">
        <ul>
          <li>Experience Platformに取り込まれたデータイベントとプロファイルは、Journey OptimizerでJourney Optimizerでジャーニーを開始し、パワージャーニーを開始するために使用できます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Journey Optimizerが生成したインタラクションとキャンペーンデータは、リアルタイム顧客データプラットフォームを介したオーディエンス構築や、Customer Journey Analytics、Experience Platformクエリサービス、Data Science Workspaceを介した分析でさらに使用するためにExperience Platformに収集されます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/triggered-messaging.html?lang=en">トリガーされたメッセージ</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Magento</td>
      <td colspan="1">現在の統合はありません</td>
      <td colspan="1">現在の統合はありません</td>
      <td colspan="1">現在の統合はありません</td>
    </tr>
    <tr>
      <td colspan="1">Marketo</td>
      <td colspan="1">
        <ul>
          <li>リアルタイム顧客データプラットフォームで定義されたオーディエンスは、Marketoキャンペーンを開始しMarketoオブジェクトを更新するオーディエンスとしてMarketoに共有できます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Marketoのアカウント、連絡先、オポチュニティデータと、Marketoが生成したインタラクションおよびキャンペーンデータが、B2B-CDPを介したExperience Platform構築や、Customer Journey Analytics、Experience Platformクエリサービス、Data Science Workspaceを介した分析で使用できるようにに取り込まれます。 <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=en">Marketo Engageコネクタ</a>
          </li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>B2Bアクティベーション — 開発中</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">リアルタイムCDP</td>
      <td colspan="1">
        <ul>
          <li>Experience Platformに取り込まれ、収集されたデータは、リアルタイム顧客データプラットフォームを強化するリアルタイム顧客プロファイルを組み立てるためのデータソースです。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>オーディエンス指標とプロファイル指標がExperience Platformデータレイクに送信され、プロファイルインサイトレポートダッシュボードが強化されます。</li>
          <li>データレークのオーディエンスとプロファイルデータは、クエリサービス、Data Science Workspace、Customer Journey Analyticsを介したさらなるインサイトに使用できます。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platformとアプリケーションを使用したアクティベーション</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Target</td>
      <td colspan="1">
        <ul>
          <li>リアルタイム顧客データプラットフォームで定義されたオーディエンスは、Targetと共有し、Targetが提供するパーソナライゼーションおよびターゲティングエクスペリエンスで使用できます。 </li>
          <li>リアルタイムのセグメントメンバーシップとプロファイル属性アクセスのための、Targetとの直接Experience Edge統合は、ロードマップに記載されています。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Targetのエクスペリエンスおよびインタラクション用に収集されたデータは、Experience PlatformWeb SDKを介してExperience Platformに収集できます。 このデータは、リアルタイム顧客データプラットフォームを介したオーディエンス構築や、Customer Journey Analyticsを介した分析に使用できます。  Experience PlatformクエリサービスとData Science Workspaceを参照してください。</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">オンライン／オフラインオーディエンスアクティベーション</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platformとアプリケーションを使用したアクティベーション</a>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
