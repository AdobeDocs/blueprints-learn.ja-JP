---
title: オーディエンスとプロファイルのアクティベーション
description: Real-time Customer Data Platform を使用して、オーディエンスがアクティブでプロファイル中心の顧客エクスペリエンスを提供します。
solution: Experience Platform, Real-time Customer Data Platform
kt: null
thumbnail: null
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
source-git-commit: d0fd2d638ad14b1cfd3b48d82093b676de465286
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 99%

---


# オーディエンスとプロファイルのアクティベーション

データドリブン型マーケティングでは、オーディエンスとプロファイルのアクティベーションが成功のカギです。ただし、多くのブランドでは、依然としてチャネルファーストのアクティベーションに注力し、多くの場合、リーチやパーソナライズ機能に一貫性がありません。

チャネルファーストのアプローチでは、各チャネルは他チャネルと連携せずに機能し、パーソナライズの取り組みは、そのチャネルのブランドとやり取りする顧客のみをターゲットにします。このアプローチは、顧客が多くの異なるタッチポイントをまたいでブランドとやり取りしているという現実を反映していません。オーディエンスとプロファイルのアクティベーションでは、ブランドは、複数のチャネルをまたいで顧客インタラクションを結びつけ、すべてのチャネルに対してアクティベーションできる一元化されたプロファイルとオーディエンスを実現できます。

| ブループリント | 説明 | Experience Cloud アプリケーション |
|---|---|---|
| **[匿名オーディエンスアクティベーション](anonymous.md)** | <ul><li>匿名および行動顧客データについて、web および広告チャネルをまたいでオーディエンスをターゲットします。</li><li>サードパーティオーディエンスデータと統合して、パーソナライズ機能を強化します。</li></ul> | <ul><li>Adobe Audience Manager</li></ul> |
| **[既知の顧客のアクティベーション](known.md)** | <ul><li>既知のプロファイルベースの宛先（電子メールプロバイダー、ソーシャルネットワーク、広告など）に対してアクティブ化します。 </li><li>オンライン行動と共に、オフライン属性およびイベント（オフラインの注文、トランザクション、CRM、ロイヤリティデータなど）を、オンラインターゲティングとパーソナライズ機能に使用します。</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager（オプション）</li></ul> |
| **[Experience Cloud アプリケーションを使用したオーディエンスとプロファイルのアクティベーション](platform-and-applications.md)** | <ul><li>Experience Platform でプロファイルおよびオーディエンスを管理し、Experience Cloud アプリケーションを使用して共有します</li><li>Experience Platform でリッチな顧客セグメントおよびインサイトを構築および共有し、Experience Cloud アプリケーションを使用して共有します</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Real-time Customer Data Platform]</li><li>Experience Platform Activation</li><li>Experience Cloud アプリケーション</li></ul> |

## リアルタイム顧客プロファイルアーキテクチャ

以下の図に、Experience Platform のリアルタイム顧客プロファイルのコアコンポーネントの概要を示します。

<img src="assets/profile_architecture.jpg" alt="リアルタイム顧客プロファイルの参照アーキテクチャ" style="border:1px solid #4a4a4a" width="90%"/>

最初のデータソースが Experience Platform に取り込まれます。データソースがプロファイル処理用に設定されている場合、リアルタイム顧客プロファイルにフィードされます。各データソース用に設定される各データソースおよび各プライマリ ID レコード用に、単一のプロファイルフラグメントまたはドキュメントが作成されます。さらに、データがプロファイルに取り込まれるので、ID サービスでも処理されます。スキーマで複数の ID がマークされ、対応する値がレコードに入力されているデータソースからのレコードは、ID サービス内の ID 関係として処理されます。

1 つの ID のみを持つレコードは、さらにグラフに入力するための ID リンクを持たないので、ID サービスで処理されないことに注意してください。また、ID サービスは、プライマリ ID とセカンダリ ID を区別しないことにも注意してください。単に ID をまたいだ ID 関係が処理されます。

ID グラフは、関連付けられた様々なソースプロファイルフラグメントをまたいで関係を提供するので、プロファイルフラグメントの結合が発生します。フラグメントが結合されているので、結合ポリシーが、使用されるソースフラグメントと ID グラフを決定します。確実に最新のプロファイルの結合を表示するために、プロファイルにアクセスするといつでも、プロファイルフラグメントの結合が発生します。ガバナンスおよびポリシールールにより、認証されたセグメントおよび属性のみを、指定された宛先に対して確実にアクティブ化できます。

## セグメント化と宛先の概要

次の図に、様々なセグメント化メソッドと、様々なプロファイルおよびオーディエンスのアクティベーションパターンの概要を示します。

<img src="assets/segmentation_destination_overview.png" alt="リアルタイム顧客プロファイルの参照アーキテクチャ" style="border:1px solid #4a4a4a" width="90%"/>

## オーディエンスとプロファイルのアクティベーションブループリントのガードレール

* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)


### 属性と ID のアクティブ化

* [!UICONTROL Real-time Customer Data Platform] は、オーディエンスのメンバーシップをアクティブにするほか、アクティベーション対象として選択したセグメントのメンバーであるプロファイルに対して発生する、属性および ID の変更をアクティブにできます。属性やアイデンティティをアクティブ化することが目的の場合は、属性やアイデンティティのアップデートが送信されるすべてのプロファイルを含むグローバルセグメントを定義する必要があります。この時点で、セグメントと目的の属性を選択し、宛先設定の一部としてアクティブ化できます。
* バッチ宛先は、属性のみを変更するイベントのアクティベーションをサポートしていません。完全または増分的なオーディエンスメンバーシップは、アクティベーションのために選択した属性と共に送信できます。

### ストリーミング宛先へのバッチセグメントのアクティブ化

* ストリーミング宛先へのバッチセグメントアクティベーションがサポートされています。プロファイルがバッチセグメントジョブのオーディエンスメンバーシップの対象として認定されると、それらの適合はストリーミングアクティベーションを通じてアクティブ化できます。

### バッチ宛先へのストリーミングセグメントのアクティブ化

* バッチ宛先へのストリーミングセグメントアクティベーションがサポートされます。バッチ宛先スケジュールは、バッチ宛先スケジュールに基づいてプロファイルセグメントメンバーシップをエクスポートします。これには、ストリーミングメソッドとバッチメソッドで決定されたセグメントメンバーシップの両方が含まれます。

### エクスペリエンスイベントのアクティブ化

* 未加工のエクスペリエンスイベントのアクティブ化はサポートされていません。エクスペリエンスイベントに対してアクティブ化するには、エクスペリエンスイベントロジックを含めるまたは除外するための必要なルールを使用して、セグメントを作成する必要があります。これにより、エクスペリエンスイベントに対して定義されたセグメントが作成され、セグメントのメンバーシップは、生のエクスペリエンスのイベントをアクティブ化するプロキシとしてアクティブ化できます。また、[!UICONTROL Launch サーバーサイド]を使用して、SDK を介して収集した未加工のエクスペリエンスイベントのアクティブ化も検討してください。


## 関連するブログ投稿

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
