---
title: オーディエンスとプロファイルのアクティベーション
description: リアルタイムの顧客データプラットフォームを使用して、アクティブ化されたプロファイル中心のオーディエンス体験を提供​します。
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
translation-type: tm+mt
source-git-commit: 844fff1cefe367575beb5c03aa0f0d026eb9f39b
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# オーディエンスとAudience Activation

プロファイルとオーディエンス優先のアクティベーションは、データ主導型マーケティングの世界を成功させる鍵となります。 ただし、多くのブランドでは、チャネル優先のアクティベーションに注力しており、多くの場合、リーチとパーソナライゼーションに一貫性がないことがあります。 チャネル優先のアプローチでは、各チャネルは、パーソナライズ取り組みターゲットがそのチャネルでブランドと対話した顧客のみを対象とするサイロとして機能します。 このアプローチは、様々なタッチポイントにわたって顧客がブランドを操作するという現実を反映していません。 プロファイルとオーディエンス優先のアクティベーションにより、ブランドは複数のチャネル間で顧客とのやり取りを結び付け、すべてのチャネルに対してアクティブ化できる一元的なプロファイルとオーディエンスを提供できます。

## ブループリント

| Blueprint | 説明 | Experience Cloudアプリ |
|---|---|---|
| **[匿名Webおよび広告Audience Activation](anonymous.md)** | <ul><li>Webおよび広告チャネルにわたるターゲットオーディエンス。匿名顧客データや行動顧客データに使用できます。</li><li>サードパーティのオーディエンスデータとの統合により、パーソナライゼーションを向上。</li></ul> | <ul><li>Adobe Audience Manager</li></ul> |
| **[オンライン/オフライン+ PIIプロファイルとAudience Activation](online-offline.md)** | <ul><li>電子メールプロバイダー、ソーシャルネットワーク、広告先など、既知のプロファイルベースの送信先に対してアクティブ化します。 </li><li>オフライン注文、トランザクション、CRM、忠誠度データなどのオフライン属性やイベントを、オンラインでのターゲティングとパーソナライゼーションのためのオンライン行動と共に使用します。</li></ul> | <ul><li>Adobe Experience Platform</li><li> リアルタイム顧客データプラットフォーム</li><li>Adobe Audience Manager（オプション）</li></ul> |
| **[プロファイルとAudience Activation](enterprise-destinations.md)** | <ul><li>アクティベーションおよびレポートの使用例に応じて、エンタープライズ・データ・ストアに対するプロファイル変更のレプリケーションと更新を行います。 </li></ul><ul><li>リアルタイム顧客データプラットフォームからエンタープライズシステムやアプリケーションに対する顧客行動を通知することで、顧客に対する販売またはサポート行動を開始します。</li></ul> | <ul><li>Adobe Experience Platform</li><li>リアルタイム顧客データプラットフォーム</li><li>Experience Platformアクティベーション</li><li>Adobe Audience Manager（オプション）</li></ul> |
| **[顧客アクティビティハブ](customer-activity.md)** | <ul><li>サポートや販売体験など、エージェントがサポートするインタラクションに対して、より深い消費者コンテキストを提供します。 Experience Platformに対するプロファイル参照を使用すると、エージェントは、最近の購入、キャンペーンインタラクション、傾向、オーディエンスのメンバーシップ、およびリアルタイム顧客プロファイルに保存された他の属性やインサイトなど、消費者に関するより多くのコンテキストを受け取ることができます。</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |

## 関連するブログ投稿

* [Adobe Experience PlatformのAudience Activationの青写真](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [Adobe Experience Platformの予測オーディエンスがパーソナライズされたエクスペリエンスをどのように改善するか](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [オーディエンス管理用Adobe Experience PlatformWeb SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
