---
title: サポートとセールスのシナリオのためのリアルタイムのプロファイルアクセス
description: '[!UICONTROL リアルタイム顧客プロファイル]を検索し、担当者がサポートおよび販売を支援する際のコンテキストを提供します。'
solution: Data Collection
kt: 7195
source-git-commit: 8284380fb9202991f3da7d755225da2e38a50cac
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 66%

---

# サポートとセールスのシナリオのためのリアルタイムのプロファイルアクセス

サポートおよびセールス シナリオのリアルタイム プロファイル アクセス ブループリントでは、外部アプリケーションが[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;]を使用してAdobe Experience Platformにアクセスする方法を示します。

外部アプリケーションは、API GET リクエストを使用して、プロファイルにアクセスできます。 これにより、プロファイルに格納された属性、イベント、セグメントメンバーシップおよびモデル主導の機能を、外部のアドビ以外のアプリケーションで使用できます。

この機能によって、顧客がコールセンターに問い合わせる際にリッチコンテキストを表示できます。 サポート担当者は、例えば、顧客のライフタイムバリュー、チャーン傾向またはマーケティングキャンペーンのエクスポージャーなどを表示できます。 また、販売担当者は、より多くのコンテキストや顧客へのインサイトというメリットを得られます。

>[!NOTE]
>
>ハブでのプロファイル検索は、web/モバイルのインバウンドパーソナライゼーションなど、スループットが高く、低遅延のユースケースを対象としたものではありません。 ハブでのプロファイル検索は、エージェントによるサポートやセールスインタラクションなど、低遅延のシナリオを目的としています。 web/モバイルのパーソナライゼーションやリアルタイムのオファー決定など、低遅延で高スループットのシナリオの場合は、Edge プロファイルを活用する必要があります。 Edge プロファイルは、Real-time Customer Data Platformの[&#x200B; カスタム Personalization Connection](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization)を通じてリアルタイム アクセスを有効にします。

## ユースケース

* 担当者がサポートするインタラクションに、詳細な消費者コンテキスト（サポートおよび販売エクスペリエンスなど）を提供します。 Experience Platform のプロファイルルックアップを使用して、担当者は、最近の購入、キャンペーンインタラクション、傾向、オーディエンスメンバーシップ、リアルタイム顧客プロファイルに格納されたその他の属性およびインサイトなど、消費者に対するより詳細なコンテキストを受け取ることができます。

## アーキテクチャ

<img src="/help/blueprints/audience-activation/assets/customer_activity_hub.svg" alt="顧客アクティビティハブブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## ガードレール

* [[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] データのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

## 実装手順

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=ja)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. 取り込まれたデータが統合プロファイルに確実にステッチできるようにするために、スキーマに[正しい ID および ID 名前空間を設定します](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. Experience Platform に[データを取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=ja)。
1. [結合ポリシーを設定](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)します。
1. [&#x200B; エンティティ APIを使用して、プロファイル属性](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=ja)を検索します。

## 関連ドキュメント

* [Adobe Experience Platform アクティベーション製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ja)
* [プロファイルガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [プロファイル検索API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
