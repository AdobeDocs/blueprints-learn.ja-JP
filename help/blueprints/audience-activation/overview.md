---
title: オーディエンスとプロファイルのアクティベーション
description: リアルタイムの顧客データプラットフォームを使用して、オーディエンスがアクティブでプロファイル中心の顧客エクスペリエンスを提供します。
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
translation-type: tm+mt
source-git-commit: 5471d9c0f6fdef6fbac72d5d35f32353ea5a5ee8
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 28%

---


# オーディエンスプロファイルアクティベーション

オーディエンスとプロファイルのアクティベーションは、データに基づくマーケティングの世界を成功させる鍵となります。 ただし、多くのブランドでは、依然としてチャネルファーストのアクティベーションに注力し、多くの場合、リーチやパーソナライズ機能に一貫性がありません。

チャネルファーストのアプローチでは、各チャネルは分断して機能し、パーソナライズの取り組みは、そのチャネルのブランドとやり取りする顧客のみをターゲットにします。このアプローチは、顧客が多くの異なるタッチポイントをまたいでブランドとやり取りしているという現実を反映していません。オーディエンスとプロファイルのアクティベーションにより、ブランドは複数のチャネル間で顧客とのやり取りを結び付け、すべてのチャネルに対してアクティブ化できる一元的なプロファイルとオーディエンスを提供できます。

| Blueprint | 説明 | Experience Cloud アプリケーション |
|---|---|---|
| **[匿名 Audience Activation](anonymous.md)** | <ul><li>匿名および行動顧客データについて、web および広告チャネルをまたいでオーディエンスをターゲットできます。</li><li>サードパーティオーディエンスデータと統合して、パーソナライズ機能を強化します。</li></ul> | <ul><li>Adobe Audience Manager</li></ul> |
| **[オンライン／オフライン Audience Activation](online-offline.md)** | <ul><li>電子メールプロバイダー、ソーシャルネットワーク、広告先など、既知のプロファイルベースの送信先に対してアクティブ化します。 </li><li>オフライン注文、トランザクション、CRM、忠誠度データなどのオフライン属性やイベントを、オンラインでのターゲティングとパーソナライゼーションのためのオンライン行動と共に使用します。</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL リアルタイム顧客データプラットフォーム]</li><li>Adobe Audience Manager（オプション）</li></ul> |
| **[Enterprise Destinationsへのオーディエンスおよびプロファイルアクティベーション](enterprise-destinations.md)** | <ul><li>アクティベーションおよびレポートの使用例に応じて、プロファイルおよびオーディエンスの変更をエンタープライズ・データ・ストアにレプリケーションおよび更新します。 </li></ul><ul><li>[!UICONTROL リアルタイム顧客データプラットフォーム]からエンタープライズシステムやアプリケーションに対する顧客行動の通知を通じて、顧客に対する販売またはサポート活動を開始します。</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL リアルタイム顧客データプラットフォーム]</li><li>Experience Platformアクティベーション</li><li>Adobe Audience Manager（オプション）</li></ul> |
| **[Experience Cloudアプリケーションとのオーディエンスとプロファイルのアクティベーション](platform-and-applications.md)** | </ul><li>Experience Platform内のプロファイルとオーディエンスを管理し、Experience Cloudアプリケーションと共有する</li><li>豊富な顧客セグメントとインサイトをExperience Platformで作成して共有し、Experience Cloudアプリケーションと共有します。</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL リアルタイム顧客データプラットフォーム]</li><li>Experience Platformアクティベーション</li><li>Experience Cloud アプリケーション</li></ul> |
| **[顧客アクティビティハブ](customer-activity.md)** | <ul><li>担当者がサポートするインタラクションに、詳細な消費者コンテキスト（サポートおよび販売エクスペリエンスなど）を提供する。Experience Platformに対するプロファイル参照を使用すると、エージェントは、最近の購入、キャンペーンインタラクション、性癖、オーディエンスのメンバーシップ、およびリアルタイム顧客プロファイルに保存されている他の属性やインサイトなど、消費者に関するより多くのコンテキストを受け取ることができます。</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |



## オーディエンスおよびプロファイルアクティベーションの設計図用ガードレール

* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)


### 属性とIDのアクティブ化

* [!UICONTROL Real-time Customer Data ] Platformは、オーディエンスのメンバーシップをアクティブにするほか、アクティベーション対象として選択したセグメントのメンバーであるプロファイルに対して発生する属性およびIDの変更をアクティブにできます。属性またはIDをアクティブにする場合は、属性やIDの更新を送信するすべてのプロファイルを含むグローバルセグメントを定義する必要があります。 この時点で、セグメントと目的の属性を選択し、宛先設定の一部としてアクティブ化できます。
* バッチ宛先は、属性のみの変更イベントのアクティベーションをサポートしていません。 オーディエンスの全メンバーシップまたは増分メンバーシップは、アクティベーションのために選択した属性と共に送信できますが、バッチ宛先を使用して属性のみの変更イベントをアクティブにすることはできません。

### ストリーミング送信先へのバッチセグメントのアクティブ化

* ストリーミング送信先へのバッチセグメントアクティベーションがサポートされています。 バッチセグメントジョブは、セグメントジョブがストリーミングアクティベーション用に完了すると、パイプラインにメッセージを配置します

### バッチ宛先へのストリーミングセグメントのアクティブ化

* バッチ宛先へのセグメントアクティベーションのストリーミングがサポートされます。 バッチ宛先スケジュールは、バッチ宛先スケジュールに基づいてプロファイルセグメントメンバーシップをエクスポートします。 これには、ストリーミングメソッドとバッチメソッドで決定されたセグメントメンバーシップの両方が含まれます。

### エクスペリエンスイベントのアクティブ化

* 生のエクスペリエンスイベントのアクティブ化はサポートされていません。 エクスペリエンスイベントに対してアクティブ化するには、エクスペリエンスイベントロジックを含むまたは除外する必要なルールを使用してセグメントを作成する必要があります。 これにより、エクスペリエンスのイベントに対して定義されたセグメントが作成され、セグメントのメンバーシップは、生のエクスペリエンスのイベントをアクティブ化するプロキシとしてアクティブ化できます。 また、[!UICONTROL Launch Server Side]を使用して、SDKで収集した生のエクスペリエンスイベントをアクティブにすることも検討してください。


## 関連するブログ投稿

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
