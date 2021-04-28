---
title: オンライン/オフラインAudience Activationのブループリント
description: オンライン／オフライン Audience Activation。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: db083e30d8add029e99cade25d561a26da78338e
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 34%

---

# オンライン/オフラインAudience Activationのブループリント

オンライン行動と共に、オフライン属性およびイベント（オフラインの注文、トランザクション、CRM、ロイヤリティデータなど）を、オンラインターゲティングとパーソナライズ機能に使用します。

既知のプロファイルベースの宛先（電子メールプロバイダー、ソーシャルネットワーク、広告など）に対して、オーディエンスをアクティベーションします。

## ユースケース

* ソーシャルおよび広告の宛先の既知のオーディエンスに対するオーディエンスターゲティング。
* オンラインおよびオフライン属性を使用したオンラインパーソナライズ機能。
* 既知のチャネル（電子メール、SMS など）に対するオーディエンスのアクティベーション。

## アプリケーション

* Adobe Experience Platform
* [!UICONTROL リアルタイム顧客データプラットフォーム]

## 構造

<img src="assets/onoff.svg" alt="オンライン/オフラインAudience ActivationのBlueprintのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* [プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

### セグメントの評価とアクティベーションのためのガードレール

| セグメントタイプ | 頻度 | スループット | 待ち時間（セグメント評価） | 待ち時間(セグメントアクティベーション) | アクティベーションペイロード |
|---|---|---|---|---|---|
| エッジセグメント | エッジセグメントは現在ベータ版であり、有効なリアルタイムセグメントをExperience Platformエッジネットワークで評価し、Adobe TargetとAdobeJourney Optimizerを介した同じページ判定をリアルタイムで行うことができます。 |  | ～100 ms | Adobe Targetでのパーソナライゼーション、エッジプロファイルでのプロファイル検索、cookieベースの宛先を介したアクティベーションに対して、すぐに使用できます。 | オーディエンスの検索とCookieベースの宛先に対して、Edgeで使用できるプロファイルメンバーシップ。<br>オーディエンスのメンバーシップとプロファイル属性は、Adobe TargetとJourney Optimizerで利用できます。 |
| ストリーミングセグメント化 | 新しいストリーミングイベントまたは記録がリアルタイム顧客プロファイルに取り込まれるたびに、そのセグメント定義が有効なストリーミングセグメントとなります。 <br>ストリーミングセグメントの条件に関するガイダンスについては、 [セグメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja) 化に関するドキュメントを参照してください。 | 1秒あたり最大1500イベント | ～ p95 &lt;5分 | ストリーミング先：ストリーミングオーディエンスのメンバーシップは、宛先の要件に基づいて約10分またはマイクロバッチ処理内にアクティブ化されます。<br>予定されている宛先：ストリーミングオーディエンスのメンバーシップは、スケジュールされた宛先配信時間に基づいて、バッチでアクティブ化されます。 | ストリーミング先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。<br>予定されている宛先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。 |
| 増分セグメント化 | 前回の増分またはバッチセグメントの評価後にリアルタイム顧客プロファイルに取り込まれた新しいデータに対して、1時間に1回。 |  |  | ストリーミング先：増分オーディエンスメンバーシップは、宛先の要件に基づいて約10分またはマイクロバッチ処理内にアクティブ化されます。<br>予定されている宛先：増分オーディエンスメンバーシップは、スケジュールされた宛先の配信時間に基づいてバッチでアクティブ化されます。 | ストリーミング先：オーディエンスメンバーシップの変更とID値のみ。<br>予定されている宛先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。 |
| バッチセグメント | 事前に定義されたシステムセットスケジュールに基づいて、またはAPIを介して手動で開始する1日に1回。 |  | ジョブあたり約1時間(最大10 TBのプロファイルストアサイズ)。10 TB ～ 100 TBのプロファイルストアサイズでは、ジョブあたり2時間。 バッチセグメントジョブのパフォーマンスは、プロファイル数、プロファイルのサイズ、評価対象のセグメント数に依存します。 | ストリーミング先：バッチオーディエンスメンバーシップは、セグメント化の評価が完了した後、または宛先の要件に基づいてマイクロバッチ処理が完了した後、約10回アクティブ化されます。<br>予定されている宛先：バッチオーディエンスのメンバーシップは、予定されている宛先配信時間に基づいてアクティブ化されます。 | ストリーミング先：オーディエンスメンバーシップの変更とID値のみ。<br>予定されている宛先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。 |

### アプリケーション間のオーディエンス共有のためのガードレール

| オーディエンスアプリケーションの統合 | 頻度 | スループット/ボリューム | 待ち時間（セグメント評価） | 待ち時間(セグメントアクティベーション) |
|---|---|---|---|---|
| リアルタイム顧客データプラットフォームからAudience Manager | セグメントタイプによって異なります。上のセグメント化ガードレールの表を参照してください。 | セグメントタイプによって異なります。上のセグメント化ガードレールの表を参照してください。 | セグメントタイプによって異なります。上のセグメント化ガードレールの表を参照してください。 | セグメント評価が完了してから数分以内に<br>リアルタイムの顧客データプラットフォームとAudience Managerの初期オーディエンス設定の同期には、約4時間かかります。<br>4時間の間に実現したオーディエンスのメンバーシップは、その後のバッチセグメントジョブに関するAudience Managerに対して、「既存の」オーディエンスのメンバーシップとして書き込まれます。 |
| リアルタイム顧客データプラットフォームからAd Cloud | Real-time Customer Data PlatformからAdobe Advertising Cloudにオーディエンスを共有するには、Audience Managerが必要です。 オーディエンス・マネージャへのリアルタイム顧客データ・プラットフォームの共有に適用されるのと同じガードレールは、リアルタイム顧客データ・プラットフォーム・オーディエンスのAdvertising Cloudへの統合に適用されます。 | - | - | - |
| Adobe Analyticsからリアルタイム顧客データプラットフォーム | 現在はご利用いただけません | 現在はご利用いただけません | 現在はご利用いただけません | 現在はご利用いただけません |
| Adobe AnalyticsからAudience Managerへ | - | 各Adobe Analyticsレポートスイートで共有できるオーディエンスは、デフォルトで最大75個です。 Audience Managerライセンスを使用する場合、Adobe AnalyticsとAdobe Target、Adobe Audience Manager、Adobe Target間で共有できるオーディエンスの数に制限はありません。 | - | - |






## 実装手順

1. Experience Platform でスキーマおよびデータセットを設定します。
1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに正しい ID および ID 名前空間を設定します。
1. プロファイル用のスキーマおよびデータセットを有効にします。
1. Platform にデータを取り込みます。
1. Experience PlatformとAudience Managerの間で[!UICONTROL Real-time Customer Data Platform]のセグメント共有をプロビジョニングし、Experience Platformで定義されたオーディエンスをAudience Managerに共有します。
1. Experience Platform の作成者セグメントが、バッチまたはストリーミングで評価されます。システムは、セグメントをバッチとして、またはストリーミングとして評価するかを自動的に判定します。
1. プロファイル属性およびオーディエンスメンバーシップを目的の宛先に共有するための宛先を設定します。

## 実装のための考慮事項

* プロファイルデータを宛先に共有するには、宛先ペイロードの宛先で使用される特定の ID 値を含める必要があります。ターゲットの宛先に必要なIDはすべて、プラットフォームに取り込まれ、[!UICONTROL リアルタイムカスタマープロファイル]のIDとして設定する必要があります。

* オーディエンスが Experience Platform から Audience Manager に共有されるアクティベーションシナリオでは、[!UICONTROL リアルタイム顧客プロファイル]に含まれるすべての ID が、Audience Manager に共有されます。必須の宛先 ID が[!UICONTROL リアルタイム顧客プロファイル]に含まれている場合、または[!UICONTROL リアルタイム顧客プロファイル]内の ID が Audience Manager でリンクされる必須の宛先 ID と関連付けられる場合、Experience Platform からのオーディエンスは、Audience Manager 宛先を使用して共有できます。

## 関連ドキュメント

* [リアルタイム顧客データプラットフォーム製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルと分類のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL リアルタイム顧客データプラットフォームのデモ]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)
