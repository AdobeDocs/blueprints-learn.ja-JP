---
title: オンライン/オフラインAudience Activationのブループリント
description: オンライン／オフライン Audience Activation。
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 81%

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
* バッチセグメントジョブは、あらかじめ決められたスケジュールに基づいて、1 日に 1 回実行します。セグメントのエクスポートジョブは、スケジュールされた宛先へ配信する前に実行されます。バッチセグメントジョブと宛先への配信ジョブは、別々に実行されることに注意してください。バッチセグメントジョブおよびエクスポートジョブのパフォーマンスは、プロファイル数、プロファイルサイズおよび評価されるセグメントの数によって決まります。
* ストリーミングセグメントジョブは、ストリーミングデータがプロファイルに届いてから数分で評価され、即座にセグメントメンバーシップをプロファイルに記述して、アプリケーションが登録するためのイベントを送信します。
* ストリーミングセグメントメンバーシップは、ストリーミング宛先で即座に適用され、宛先の取り込みパターンに応じて、単一のセグメントメンバーシップイベントまたは複数のプロファイルイベントのマイクロバッチのいずれかで配信されます。スケジュールされた宛先は、スケジュールされたバッチセグメント配信を介して配信されるストリーミングにて評価される任意のセグメントに対して、配信する前にプロファイルからセグメントのエクスポートジョブを開始します。
* [!UICONTROL Real-time Customer Data Platform]のセグメントメンバーシップをAudience Managerに共有する場合、セグメントのストリーミングに関しては数分以内に、バッチセグメント用のバッチセグメント評価が完了した時点で数分以内に発生します。
* Experience Platform から Audience Manager に共有されたセグメントは、ストリーミングかバッチ評価方法かにかかわらず、セグメント適合から数分以内に共有されます。Experience PlatformとAudience Managerの間で、最初にセグメントを作成した後、最初にセグメントの設定を同期できます。4時間後に、Experience PlatformセグメントのメンバーシップがAudience Managerプロファイルで実現され始めます。 Experience Platform と Audience Manager のオーディエンス共有が設定される前または Experience Platform から Audience Manager にオーディエンスメタデータが同期される前に適合されるオーディエンスメンバーシップは、「既存」のセグメントメンバーシップが共有される後続のセグメントジョブまで、Audience Manager で適合されません。
* バッチセグメントジョブからのバッチまたはストリーミング宛先ジョブは、セグメントメンバーシップだけでなく、プロファイル属性の更新も共有できます。
* ストリーミング宛先へのストリーミングセグメント化ジョブは、セグメントメンバーシップの更新のみを共有します。

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
* [セグメント化ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ja)
* [宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ja)

## 関連ビデオおよびチュートリアル

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ja)
* [[!UICONTROL リアルタイム顧客データプラットフォームのデモ]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ja)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ja)
