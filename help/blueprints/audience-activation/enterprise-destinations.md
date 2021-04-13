---
title: Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション
description: Enterprise Destinationsへのオーディエンスおよびプロファイルアクティベーション
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: a63da7d5da3038cf66b5f2c99e117d4aa5b21cc1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション

アクティベーションおよびレポートの使用例に応じて、プロファイルおよびオーディエンスの変更をエンタープライズ・データ・ストアにレプリケーションおよび更新します。<!-- This sentence is difficult to mentally process because there's no verb. Describe what the customer can do with this feature. The first paragraph on a page should not be an abstract description.-->

[!UICONTROL リアルタイム顧客データプラットフォーム]からエンタープライズシステムやアプリケーションに対する顧客行動の通知を通じて、顧客に対する販売またはサポート活動を開始します。<!-- What kinds of sales or support actions? You might add a "For example...." The content in these blueprints should be more simple and friendly.-->

## 使用例

* プロファイルおよびオーディエンスのアクティベーションをクラウドストレージの宛先に送信するか、エンタープライズトラッキング、ストレージ、分析、顧客データおよびインサイトのアクティベーションのためのストリーミング送信先に送信します。

## アプリ

* Adobe Experience Platformアクティベーション

## 建築

<img src="assets/enterprise_destination.svg" alt="エンタープライズアクティベーションシナリオのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

[プロファイルとセグメント化のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

待ち時間とスループットのしきい値：

ストリーミングセグメント：

* ストリーミングセグメント化の場合は最大5分、1秒あたり最大1500イベント
* ストリーミングアクティベーションの場合は最大11分

バッチセグメント：
1日に1回、またはAPIを使用して手動で開始するアドホック。

* ジョブあたり約1時間(最大10 TBのプロファイルストアサイズ)
* 10 TB ～ 100 TBのプロファイル・ストア・サイズでジョブあたり約2時間

## 導入手順

1. 取り込むデータのスキーマを作成します。<!-- Cross-references to these topics would be helpful -->
1. 取り込むデータのデータセットを作成します。
1. スキーマ上の正しいIDとIDの名前空間を設定し、取り込んだデータを統合プロファイルに確実に結合できるようにします。
1. プロファイル処理のスキーマとデータセットを有効にします。
1. データ取り込み用に任意のソースを設定します。
1. Experience Platformでのセグメントの作成。バッチまたはストリーミングで評価されます。 セグメントがバッチとストリーミングのどちらとして評価されるかは、システムによって自動的に判断されます。
1. プロファイル属性とオーディエンスのメンバーシップを目的の宛先に共有する宛先を設定します。

## 実装に関する考慮事項

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

* [Destinationsドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [クラウドストレージの宛先の概要](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP宛先](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [[!UICONTROL リアルタイム顧客データ] プラットフォーム製品の説明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルと分類のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [セグメントドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## 関連するビデオとTutorials

* [[!UICONTROL リアルタイム顧客データ] プラットフォームビュー](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [リアルタイム顧客データプラット [!UICONTROL フォームのデモ]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
