---
title: Web およびモバイルPersonalization用のリアルタイム Edge プロファイルアクセス
description: '[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] エッジでアクセスして、リアルタイムの web およびモバイルパーソナライゼーションのコンテキストを提供します。'
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
exl-id: null
source-git-commit: 5530337ed9a9c67285db4abd0afba3809466e42c
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 6%

---

# Web およびモバイルPersonalization用のリアルタイム Edge プロファイルアクセス

Web およびモバイルEdgeのリアルタイム Personalization プロファイルアクセス ブループリントは、web およびモバイルアプリケーションがエッジでAdobe Experience Platform [!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] にアクセスして、高スループットで低遅延のパーソナライゼーションを行う方法を示します。

アプリケーションは、ミリ秒の待ち時間で、エッジのリアルタイムプロファイル属性およびオーディエンスにアクセスできます。 プロファイルに属性として保存されている属性、オーディエンスメンバーシップ、モデル駆動機能にリアルタイムでアクセスして、web チャネルやモバイルチャネルをまたいで同じページや次のページのパーソナライゼーションを行うことができます。

この機能を使用すると、リアルタイム顧客プロファイルに基づいて、高度にパーソナライズされたエクスペリエンスを web サイトやモバイルアプリケーションで提供できます。これには、リアルタイムの行動から得られたオーディエンス、リアルタイム顧客プロファイルに取り込まれた属性、計算されたインサイトなどが含まれます。

>[!NOTE]
>
>Edge プロファイルアクセスは、web/モバイルインバウンドパーソナライゼーション、リアルタイム offer decisioning など、高スループットで低遅延のユースケース向けに特別に設計されています。 エージェント支援サポートや営業インタラクションなど、スループットの低いシナリオには、ハブプロファイル参照 API の方が適しています。 ハブベースのプロファイルアクセスについては、[&#x200B; サポートおよび販売シナリオのリアルタイムプロファイルアクセスのブループリント &#x200B;](customer-activity.md) を参照してください。

## アプリケーション

* Real-time Customer Data Platform
* Adobe Experience Platform Data Collection （Web SDK/モバイルSDK）
* Edge Network Server API

## ユースケース

* 既知の顧客体験に対応する web およびモバイルチャネルでのリアルタイムパーソナライゼーション
* リアルタイムのプロファイル属性とオーディエンスに基づく、同じページおよび次のページのパーソナライゼーション
* リアルタイムの行動データ、属性、計算されたインサイトなど、顧客プロファイルに基づくコンテンツとオファーのパーソナライゼーション
* パーソナライゼーションエンジン、コンテンツ管理システム、外部アプリケーションとの統合により、リアルタイムの意思決定を実現
* リアルタイムプロファイルコンテキストを使用したテストとコンテンツの最適化

## 前提条件

プロファイルをストリーミングデータでリアルタイムに更新する場合、このブループリントでは次のいずれかのデータ収集方法を使用する必要があります。 Edge プロファイルに直接データを収集しなくても、Edge プロファイルにリアルタイムでアクセスできます。データをハブに収集して、Edge プロファイルにも投影できます。 ハブに収集されたデータがEdgeに投影されると、待ち時間が追加されます。

* Web サイトからデータを収集する場合は [&#128279;](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=ja)Adobe Experience Platform Web SDK&rbrace; を使用します。
* モバイルアプリケーションからデータを収集する場合は [&#128279;](https://developer.adobe.com/client-sdks/home/)Adobe Experience Platform Mobile SDK&rbrace; を使用します。
* Web SDKや Mobile SDKを使用していない場合 [&#x200B; またはサーバーからサーバーへの直接接続を実装している場合は、](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)Edge Network Server API を使用します。

>[!IMPORTANT]
>
>エッジパーソナライゼーションを実装する前に、[&#x200B; エッジパーソナライゼーションの宛先に対してオーディエンスデータをアクティブ化する &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations) 方法についてのガイドをお読みください。 このガイドでは、複数のExperience Platform コンポーネントをまたいで、同じページおよび次のページのパーソナライゼーションのユースケースに必要な設定手順を説明します。

## アーキテクチャ図

<img src="assets/real-time-edge-lookup.svg" alt="Web およびモバイル Personalization用のEdge プロファイルアクセスのリファレンスアーキテクチャ" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## ガードレール

* [[!UICONTROL リアルタイム顧客プロファイル]データのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [Edge Networkガードレール &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Edge プロファイルには、14 日間の有効期間（TTL）があります。 ユーザーがエッジでアクティブ化されていない期間が 14 日間ある場合は、エッジプロファイルの有効期限が切れ、ハブから取得する必要が生じる可能性があり、最初のページのパーソナライゼーションに影響を与える可能性があります。
* Edgeのパーソナライゼーションでは、エッジのセグメント化条件を満たすオーディエンスに対して、オーディエンスメンバーシップのリアルタイム評価をサポートしています。 ハブのバッチオーディエンスとストリーミングオーディエンスは、適切に設定されたエッジでも使用できます。

## 実装パターン

Edgeのパーソナライゼーションは、Real-time Customer Data Platform の [&#x200B; カスタム Personalization接続 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization) 宛先を使用して実装できます。 この宛先では、使用例に応じて複数のデータ収集方法をサポートしています。

### パターン 1:Web SDK/モバイル SDKを使用したオーディエンスメンバーシップベースのパーソナライゼーション

* オーディエンスメンバーシップベースのパーソナライゼーションには、Adobe Experience Platform Web SDKまたはモバイル SDKとEdge Networkを使用します。
* このアプローチは、オーディエンスのメンバーシップに基づいて、エッジのパーソナライゼーションに低遅延と最高のパフォーマンスを提供します。
* リアルタイムエッジのセグメント化には、web/モバイル SDKの実装が必要です。
* Web SDKと Mobile SDK **単独では、オーディエンスメンバーシップのみに基づくパーソナライゼーションをサポートします**。
* SDK ベースの実装については [Experience Platform Web およびモバイル SDK ブループリントのを参照 &#x200B;](../experience-platform/deployment/websdk.md) てください。
* Mobile SDKを実装する場合は、[Adobe Journey Optimizer - Decisioning 拡張機能 &#x200B;](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/) を Mobile SDKにインストールする必要があります。

### パターン 2:Edge Network Server API を使用した属性ベースのパーソナライゼーション（プロファイル属性に必要）

>[!IMPORTANT]
>
>**属性ベースのパーソナライゼーション要件：** （オーディエンスメンバーシップだけでなく）プロファイル属性に基づいてパーソナライズする場合は、データ収集に Web SDKまたは Mobile SDKも使用しているかどうかに関係なく、認証済みのサーバーサイド統合で **&#x200B;**&#x200B;4&rbrace;Edge Network Server API[&#x200B; を使用する必要があります。](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)

* サードパーティのパーソナライゼーションエンジンおよび CDN ベースのパーソナライゼーションとの統合を有効にします。
* パーソナライゼーションのプロファイル属性を安全に取得するには、Edge Network Server API が必要です **必須**。
* Web または Mobile SDKの実装に既に使用しているのと同じデータストリームを使用するサーバーサイド統合を追加することで、Edge Network Server API を介してプロファイル属性を取得できます。
* 機密データを保護するために、プロファイル属性に対するすべてのEdge Network Server API 呼び出しは、認証済みコンテキストで行う必要があります。
* このパターンにより、オーディエンスメンバーシップベースのパーソナライゼーションと属性ベースのパーソナライゼーションの両方が可能になります。
* サーバーサイドパーソナライゼーションのユースケース、API ベースの統合、プロファイル属性アクセスを必要とするシナリオに適しています。

## 実装手順

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=ja)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. スキーマで [&#x200B; 正しい ID と ID 名前空間を設定 &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja) して、取り込まれたデータが統合プロファイルにステッチできるようにします。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. Experience Platform に[データを取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=ja)。
1. [&#x200B; 結合ポリシーを設定 &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja) して、ID ステッチとプロファイル結合が正しいことを確認します。
1. 宛先設定を有効にして、Experience Platform Data Collection で [&#x200B; データストリームを設定 &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ja) します。 データストリームは、ページへの応答にオーディエンスを含めるデータ収集データストリームを決定します。
1. データ収集用の web およびモバイルプロパティに [0&rbrace;Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=ja) または [&#x200B; モバイル SDK&rbrace; を実装します。](https://developer.adobe.com/client-sdks/home/)
1. リアルタイム評価が必要なオーディエンスには、エッジのセグメント化を設定します。 [Edgeのセグメント化に関するドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ja)。
1. 宛先カタログで、[&#x200B; カスタム Personalization接続 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization) 宛先を設定します。
1. [&#x200B; エッジパーソナライゼーションの宛先に対するオーディエンスのアクティブ化 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations). 宛先に対してアクティブ化するオーディエンスを選択します。
1. （属性ベースのパーソナライゼーションではオプション）オーディエンスメンバーシップに加えて、プロファイル属性に基づいてパーソナライズする必要がある場合は、同じデータストリームを使用して認証済みのサーバーサイド統合で [0&rbrace;Edge Network Server API&rbrace; を実装します。 &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)これは、プロファイル属性へのアクセスに **必須** です。
1. 書き出されたオーディエンスデータとプロファイル属性を使用するように web/モバイルアプリケーションにパーソナライゼーションロジックを実装します。
   * Adobe Experience Platformのタグを使用している場合は、[event complete の送信機能 &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja) を使用して、書き出したデータ `event.destinations` 変数にアクセスします。
   * タグを使用しない場合は、[&#x200B; コマンド応答 &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html?lang=ja) を使用して、Adobe Experience Platformからの JSON 応答を解析し、オーディエンス ID とプロファイル属性を取得します。

## 実装に関する考慮事項

### ID に関する考慮事項

* Edge Networkで web SDKまたはモバイル SDKを使用する場合、任意のプライマリ ID をエッジのパーソナライゼーションに使用できます。
* 既知の顧客データを使用した最初のログインパーソナライゼーションの場合、パーソナライゼーションリクエストでは、Real-time Customer Data Platform の既知の顧客 ID に一致するプライマリ ID を使用する必要があります。 プライマリ ID が ECID に設定されている場合や、既知の顧客プロファイルにまだステッチされていない匿名 ID に設定されている場合、ID ステッチの実現に時間がかかり、パーソナライゼーションの過去のプロファイルデータの可用性に影響する可能性があります。
* Edge プロファイルは、パーソナライゼーションに使用する前に初期化する必要があります。 エッジプロファイルの有効期限（14 日 TTL）が切れた初回の訪問者または再訪問者は、エッジプロファイルが完全に入力されるまで、制限されたプロファイルデータに基づいた最初のパーソナライゼーションが発生する可能性があります。

### 属性ベースのパーソナライゼーション

>[!IMPORTANT]
>
>プロファイル属性には、機密データが含まれている場合があります。 このデータを保護するには、属性ベースのパーソナライゼーション用にカスタム Edge Networkの宛先を設定する際に **2&rbrace;Personalization Server API&rbrace; を使用する** 必要があります [。 &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)すべてのEdge Network Server API 呼び出しは、認証済みコンテキストで行う必要があります。

* プロファイル属性を使用した属性ベースのパーソナライゼーションの場合は、Web または Mobile SDKの実装に使用するのと同じデータストリームを使用する、Edge Network Server API とのサーバーサイド統合を追加する必要があります。
* カスタム Personalization Connection destination configuration を使用して、エッジ投影に含めるプロファイル属性を設定する必要があります。
* **Web SDKとモバイル SDKだけでは、オーディエンスメンバーシップに基づくパーソナライゼーションのみをサポートします**。 パーソナライゼーションのプロファイル属性を安全に取得するには、Edge Network Server API が必要です **必須**。
* 属性アクセス用にEdge Network Server API を実装しない場合、パーソナライゼーションはオーディエンスメンバーシップのみに基づきます。
* 属性を含むカスタム Personalizationの API 応答には、オーディエンスセグメントに加えて `attributes` セクションが含まれています。

### オーディエンスの考慮事項

* ハブ上のストリーミングまたはバッチセグメント化を通じて評価されたオーディエンスは、エッジに投影され、パーソナライゼーションに使用できます。
* エッジのセグメント化条件を満たすオーディエンスは、エッジ上でリアルタイムに評価され、同じページのパーソナライゼーションが可能になります。
* リアルタイムパーソナライゼーションのユースケースでの使用状況に基づいて、エッジ評価の適切なオーディエンスを設定します。

## 関連ドキュメント

### 宛先設定

* [&#x200B; カスタム Personalization接続 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - プライマリ実装ガイド
* [Personalizationの宛先の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/overview)
* [&#x200B; エッジパーソナライゼーションの宛先に対するオーディエンスのアクティブ化 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [&#x200B; エッジ上のプロファイル属性のリアルタイム検索 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### SDK ドキュメント

* [Experience Platform Web SDK ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=ja)
* [Experience Platform Mobile SDK ドキュメント](https://developer.adobe.com/client-sdks/home/)
* [Edge Network Server API ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)
* [Experience Platform タグドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Web SDKのコマンドの応答 &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html?lang=ja)

### プロファイルとセグメント化に関するドキュメント

* [[!UICONTROL リアルタイム顧客プロファイル]ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ja)
* [プロファイルのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

### チュートリアル

* [Real-Time CDP と Adobe Target を使用した、次のヒットのパーソナライズ機能](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ja)
* [&#x200B; データストリーム設定 &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ja)
