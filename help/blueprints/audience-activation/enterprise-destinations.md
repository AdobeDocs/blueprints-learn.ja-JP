---
title: Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション
description: Enterprise Destinationsへのオーディエンスおよびプロファイルアクティベーション
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: 8bcd82eac5e8837c3cd84524174cf5792d73ac6e
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Enterprise Destinations Blueprintへのオーディエンスとプロファイルのアクティベーション

アクティベーションおよびレポートの使用例に応じて、プロファイルおよびオーディエンスの変更をエンタープライズ・データ・ストアにレプリケーションおよび更新します。

リアルタイム顧客データプラットフォームからエンタープライズシステムやアプリケーションに対する顧客行動を通知することで、顧客に対する販売またはサポート行動を開始します。

## 使用例

* 企業の追跡、ストレージ、分析、および顧客データとインサイトのアクティベーションを行うための、クラウドストレージのアクティベーション先またはストリーミングの宛先へのプロファイルおよびオーディエンスの管理。

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
1日に1回、またはAPIを使用して手動で開始する

* ジョブあたり約1時間(最大10 TBのプロファイルストアサイズ)
* 10 TB ～ 100 TBのプロファイル・ストア・サイズでジョブあたり約2時間

## 導入手順

1. 取り込むデータのスキーマを作成する
1. データを取り込むためのデータセットの作成
1. スキーマ上の正しいIDとIDの名前空間を設定し、取り込んだデータを統合プロファイルに確実に結合できるようにします。
1. プロファイル処理のスキーマとデータセットを有効にします。
1. データ取り込み用のソースの設定
1. Experience Platform内の作成者セグメント。バッチまたはストリーミングで評価されます。 セグメントがバッチとストリーミングのどちらとして評価されるかは、システムによって自動的に判断されます。
1. プロファイル属性とオーディエンスのメンバーシップを目的の宛先に共有する宛先を設定します。

## 実装に関する考慮事項

属性とIDのアクティベーション

* Real-time Customer Data Platformでは、オーディエンスのメンバーシップと、アクティベーション対象として選択されたセグメントのメンバーであるプロファイルに対して発生する属性とIDの変更の両方をアクティブ化できます。 したがって、属性やIDをアクティブにする場合は、属性やIDの更新を送信するプロファイルをすべて含むグローバルセグメントを定義する必要があります。 この設定を行うと、セグメントと、アクティブ化する必要のある属性を宛先設定の一部として選択できます。
* バッチ宛先は、属性の変更イベントのみのアクティベーションをサポートしていません。 オーディエンスメンバーシップのフルまたはインクリメンタルは、アクティベーションのために選択した属性と共に送信できますが、属性の変更イベントのみをバッチ宛先を介してアクティブ化することはできません。

ストリーミング先へのセグメントアクティベーションのバッチ

* ストリーミング送信先へのバッチセグメントアクティベーションがサポートされています。 バッチセグメントジョブは、セグメントジョブがストリーミングアクティベーション用に完了すると、パイプラインにメッセージを配置します

バッチ宛先へのセグメントアクティベーションのストリーミング

* バッチ宛先へのセグメントアクティベーションのストリーミングがサポートされます。 バッチ宛先スケジュールは、バッチ宛先スケジュールに基づいてプロファイルのセグメントメンバーシップをエクスポートします。 これには、ストリーミングメソッドとバッチメソッドで決定されたセグメントメンバーシップの両方が含まれます。

エクスペリエンスイベントのアクティベーション

* 生のエクスペリエンスイベントのアクティベーションは現在サポートされていません。 エクスペリエンスイベントに対してアクティブ化するには、アクティブ化するエクスペリエンスイベントロジックを含む/除外する必要なルールを使用してセグメントを作成する必要があります。 これにより、エクスペリエンスのイベントに対して定義されたセグメントが作成されます。セグメントのメンバーシップは、生のエクスペリエンスのイベントをアクティブ化する代わりにアクティブ化できます。 また、SDKで収集した生のエクスペリエンスイベントをアクティベーションする場合は、起動サーバー側を利用することも検討してください。

## 関連ドキュメント

* [Destinationsドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [Enterprise Cloudストレージの宛先](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP宛先](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [リアルタイム顧客データプラットフォーム製品の説明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルとセグメント化のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [セグメントドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## 関連するビデオとTutorials

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [リアルタイム顧客データプラットフォームのデモ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
