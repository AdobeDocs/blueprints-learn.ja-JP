---
title: Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション
description: Enterprise Destinationsへのオーディエンスおよびプロファイルアクティベーション
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: 2f35195b875d85033993f31c8cef0f85a7f6cccc
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 15%

---

# Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション

[!UICONTROL Real-time Customer Data Platform]から企業のデータ・ストアやアプリケーションに、ストリーミングまたはバッチでプロファイルとオーディエンスの変更とイベントを共有します。 これらのプロファイルおよびオーディエンスイベントは、廃棄された申し込みプロセスやウェビナー登録のフォローアップ、[!UICONTROL Real-time Customer Data Platform]の最新の顧客属性とインテリジェンスを使用したエンタープライズアプリケーションの更新など、顧客に対する販売またはサポート活動を開始するために使用できます。

## ユースケース

* プロファイルおよびオーディエンスのアクティベーションをクラウドストレージの宛先に送信するか、エンタープライズトラッキング、ストレージ、分析、顧客データおよびインサイトのアクティベーションのためのストリーミング送信先に送信します。

## アプリケーション

* Adobe Experience Platform アクティベーション

## 構造

<img src="assets/enterprise_destination.svg" alt="エンタープライズアクティベーションシナリオのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

[プロファイルおよびセグメント化ガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

### セグメントの評価とアクティベーションのためのガードレール

|セグメントタイプ |頻度 |スループット |遅延（セグメント評価） |遅延(セグメントアクティベーション) |アクティベーションペイロード |
|-|-|-|-|-|-|
|エッジセグメント |エッジセグメントは現在ベータ版です。有効なリアルタイムセグメントをExperience Platformエッジネットワークで評価し、Adobe TargetとAdobeJourney Optimizerを介した同じページ判定をリアルタイムで行うことができます。 |  | ～100 ms |Adobe Targetでのパーソナライゼーション、エッジプロファイルでのプロファイル検索、cookieベースの宛先を介したアクティベーションに対して、すぐに利用できます。 |オーディエンスメンバーシップは、プロファイルの検索やCookieベースの宛先に使用できます。<br>オーディエンスのメンバーシップとプロファイル属性は、Adobe TargetとJourney Optimizerで利用できます。|
|ストリーミングセグメント |新しいストリーミングイベントまたは記録がリアルタイム顧客プロファイルに取り込まれるたびに、そのセグメント定義が有効なストリーミングセグメントになります。 <br>ストリーミングセグメントの条件に関するガイダンスについては、 [セグメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja) 化に関するドキュメントを参照してください。 | 1秒あたり最大1,500イベント| ～ p95 &lt;5分 |ストリーミング送信先：ストリーミングオーディエンスのメンバーシップは、宛先の要件に基づいて約10分またはマイクロバッチ処理内にアクティブ化されます。<br>予定されている宛先：ストリーミングオーディエンスのメンバーシップは、スケジュールされた宛先配信時間に基づいて、バッチでアクティブ化されます。|ストリーミング送信先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。<br>予定されている宛先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。|
|増分セグメント |前回の増分またはバッチセグメントの評価以降にリアルタイム顧客プロファイルに取り込まれた新しいデータは、1時間に1回です。 |  |  |ストリーミング送信先：増分オーディエンスメンバーシップは、宛先の要件に基づいて約10分またはマイクロバッチ処理内にアクティブ化されます。<br>予定されている宛先：増分オーディエンスメンバーシップは、スケジュールされた宛先の配信時間に基づいてバッチでアクティブ化されます。|ストリーミング送信先：オーディエンスメンバーシップの変更とID値のみ。<br>予定されている宛先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。|
|バッチセグメント |システムセットのスケジュールが事前に決まっているか、APIを使用して手動で開始したad hoc。 |  |ジョブあたり約1時間(最大10 TBのプロファイルストアサイズ)。10 TB ～ 100 TBのプロファイルストアサイズでは、ジョブあたり2時間。 バッチセグメントジョブのパフォーマンスは、プロファイル数、プロファイルのサイズ、評価対象のセグメント数に依存します。 |ストリーミング送信先：バッチオーディエンスメンバーシップは、セグメント化の評価が完了した後、または宛先の要件に基づいてマイクロバッチ処理が完了した後、約10回アクティブ化されます。<br>予定されている宛先：バッチオーディエンスのメンバーシップは、予定されている宛先配信時間に基づいてアクティブ化されます。|ストリーミング送信先：オーディエンスメンバーシップの変更とID値のみ。<br>予定されている宛先：オーディエンスメンバーシップの変更、ID値およびプロファイル属性。 |



## 実装手順

1. 取り込むデータのスキーマを作成します。
1. 取り込むデータのデータセットを作成します。
1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに正しい ID および ID 名前空間を設定します。
1. プロファイル処理のスキーマとデータセットを有効にします。
1. データ取り込み用に任意のソースを設定します。
1. Experience Platformでのセグメントの作成。バッチまたはストリーミングで評価されます。 システムは、セグメントをバッチとして、またはストリーミングとして評価するかを自動的に判定します。
1. プロファイル属性およびオーディエンスメンバーシップを目的の宛先に共有するための宛先を設定します。

## 実装のための考慮事項

属性とIDのアクティブ化

* [!UICONTROL Real-time Customer Data ] Platformは、オーディエンスのメンバーシップをアクティブにするほか、アクティベーション対象として選択したセグメントのメンバーであるプロファイルに対して発生する属性およびIDの変更をアクティブにできます。属性またはIDをアクティブにする場合は、属性やIDの更新を送信するすべてのプロファイルを含むグローバルセグメントを定義する必要があります。 この時点で、セグメントと目的の属性を選択し、宛先設定の一部としてアクティブ化できます。
* バッチ宛先は、属性のみの変更イベントのアクティベーションをサポートしていません。 オーディエンスの全メンバーシップまたは増分メンバーシップは、アクティベーションのために選択した属性と共に送信できますが、バッチ宛先を使用して属性のみの変更イベントをアクティブにすることはできません。

ストリーミング送信先へのバッチセグメントのアクティブ化

* ストリーミング送信先へのバッチセグメントアクティベーションがサポートされています。 バッチセグメントジョブは、セグメントジョブがストリーミングアクティベーション用に完了すると、パイプラインにメッセージを配置します

バッチ宛先へのストリーミングセグメントのアクティブ化

* バッチ宛先へのセグメントアクティベーションのストリーミングがサポートされます。 バッチ宛先スケジュールは、バッチ宛先スケジュールに基づいてプロファイルセグメントメンバーシップをエクスポートします。 これには、ストリーミングメソッドとバッチメソッドで決定されたセグメントメンバーシップの両方が含まれます。

エクスペリエンスイベントのアクティブ化

* 生のエクスペリエンスイベントのアクティブ化はサポートされていません。 エクスペリエンスイベントに対してアクティブ化するには、エクスペリエンスイベントロジックを含むまたは除外する必要なルールを使用してセグメントを作成する必要があります。 これにより、エクスペリエンスのイベントに対して定義されたセグメントが作成され、セグメントのメンバーシップは、生のエクスペリエンスのイベントをアクティブ化するプロキシとしてアクティブ化できます。 また、[!UICONTROL Launch Server Side]を使用して、SDKで収集した生のエクスペリエンスイベントをアクティブにすることも検討してください。

## 関連ドキュメント

* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)
* [クラウドストレージの宛先の概要](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP宛先](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [リアルタイム顧客データプラットフォーム製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルと分類のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## 関連ビデオおよびチュートリアル

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL リアルタイム顧客データプラットフォームのデモ]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)
