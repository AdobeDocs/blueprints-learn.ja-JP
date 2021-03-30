---
title: オンライン/オフラインAudience Activationのシナリオ
description: オンライン/オフラインAudience Activation
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
translation-type: tm+mt
source-git-commit: c4bd4bbd40f2ae6b9ab980c5274a6e2007d976d3
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---


# オンライン/オフラインAudience Activationのシナリオ

オフライン注文、トランザクション、CRM、忠誠度データなどのオフライン属性やイベント、およびオンラインでのターゲット設定とパーソナライゼーションに関するオンラインビヘイビアーを使用します。

電子メールプロバイダー、ソーシャルネットワーク、広告先など、既知のプロファイルベースの送信先に対するオーディエンスをアクティブ化します。

## 使用例

* ソーシャルおよび広告のリンク先に関する既知のオーディエンスをターゲットにしたオーディエンスです。
* オンラインおよびオフラインの属性を使用したオンラインパーソナライゼーション。
* 電子メールやSMSなど、既知のチャネルに対するオーディエンスをアクティブにします。

## アプリ

* Adobe Experience Platform
* リアルタイム顧客データプラットフォーム

## 建築

<img src="assets/onoff.svg" alt="オンライン/オフラインAudience Activationシナリオのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

* [プロファイルとセグメント化のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* バッチセグメントジョブは、事前に決定されたスケジュールに基づいて1日に1回実行されます。 次に、セグメントエクスポートジョブは、スケジュールされた宛先配信の前に実行されます。 バッチセグメントジョブと宛先配信ジョブは、別々に実行されます。 バッチセグメントジョブと書き出しジョブのパフォーマンスは、プロファイル数、プロファイルのサイズ、評価対象のセグメント数に依存します。
* ストリーミングセグメントジョブは、プロファイルに到着するストリーミングデータの分単位で評価され、即座にセグメントのメンバーシップがプロファイルに書き込まれ、登録するアプリケーションのイベントが送信されます。
* ストリーミングセグメントのメンバーシップは、ストリーミング先に対して即座に行われ、単一のセグメントのメンバーシップイベントまたは宛先の取り込みパターンに依存する複数のプロファイルイベントのマイクロバッチで配信されます。 スケジュール済みの宛先は、配信前にプロファイルから、セグメントエクスポートジョブを開始します。ストリーミングで評価され、スケジュール済みのバッチセグメント配信を介して配信されるセグメントについて、
* RTCDPセグメントのメンバーシップをAudience Managerに共有する場合、この処理は、セグメントのストリーミングに関しては数分以内に、バッチセグメントに関するバッチセグメント評価が完了した時点で数分以内に行われます。
* Experience Platform間で共有されるセグメントは、セグメントの実現から数分以内に共有されます。セグメントの実現は、ストリーミングまたはバッチの評価の方法を使用して行われます。 AEPとAAMの間で、最初にセグメントが作成された後、最初にセグメント設定を同期することができます。約4時間後に、AAMプロファイルでAEPセグメントのメンバーシップが実現され始めます。 Experience PlatformとAudience Managerオーディエンスの共有の構成前、またはオーディエンスメタデータがExperience Platform間で同期される前に実現されたオーディエンスメンバーシップは、「既存」のセグメントメンバーシップが共有される次のセグメントジョブまでAudience Managerで実現されません。
* バッチセグメントジョブからの宛先ジョブをバッチまたはストリーミングする場合、プロファイル属性の更新とセグメントのメンバーシップを共有できます。
* ストリーミング送信先へのセグメント化ジョブは、セグメントメンバーシップの更新のみを共有します。

## 導入手順

1. Experience Platformでスキーマとデータセットを設定します。
1. スキーマ上の正しいIDとIDの名前空間を設定し、取り込んだデータを統合プロファイルに確実に結合できるようにします。
1. プロファイル用のスキーマとデータセットを有効にします。
1. データをプラットフォームに取り込みます。
1. Experience Platformで定義されたオーディエンスをAudience Managerに共有するために、Experience PlatformとAudience Managerの間でReal-time Customer Data Platformセグメント共有をプロビジョニングします。
1. Experience Platform内の作成者セグメント。バッチまたはストリーミングで評価されます。 セグメントがバッチとストリーミングのどちらとして評価されるかは、システムによって自動的に判断されます。
1. プロファイル属性とオーディエンスのメンバーシップを目的の宛先に共有する宛先を設定します。

## 実装に関する考慮事項

* 宛先にプロファイルデータを共有するには、宛先のペイロードで使用する特定のID値を宛先のペイロードに含める必要があります。 ターゲットの宛先に必要なIDはすべて、プラットフォームに取り込まれ、リアルタイム顧客プロファイルのIDとして設定する必要があります。

* オーディエンスをExperience Platform間で共有するアクティベーションシナリオでは、[!UICONTROL リアルタイム顧客プロファイル]に含まれるすべてのIDがAudience Managerに共有されます。 Experience Platformのオーディエンスは、必要な宛先IDが[!UICONTROL リアルタイム顧客プロファイル]に含まれる場合はAudience Manager先を通じて共有でき、[!UICONTROL リアルタイム顧客プロファイル]のIDがAudience Manager内でリンクされている必要な宛先IDと関連付けられる場合は共有できます。

## 関連ドキュメント

* [リアルタイム顧客データプラットフォーム製品の説明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [プロファイルとセグメント化のガイドライン](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [セグメントドキュメント](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinationsドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## 関連するビデオとTutorials

* [リアルタイム顧客データプラットフォームの概要](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [リアルタイム顧客データプラットフォームのデモ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [セグメントの作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)