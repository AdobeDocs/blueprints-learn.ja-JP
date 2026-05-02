---
title: webおよびモバイルPersonalizationのリアルタイムEdgeプロファイルアクセス
description: '[!UICONTROL &#x200B; リアルタイムの顧客プロファイル &#x200B;]がエッジでアクセスし、リアルタイムのwebおよびモバイルのパーソナライゼーションのコンテキストを提供します。'
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
source-git-commit: 8284380fb9202991f3da7d755225da2e38a50cac
workflow-type: tm+mt
source-wordcount: '1936'
ht-degree: 11%

---

# webおよびモバイルPersonalizationのリアルタイムEdgeプロファイルアクセス

Webおよびモバイル向けのリアルタイムのEdge プロファイルへのアクセス Personalization ブループリントでは、Webおよびモバイルアプリケーションがエッジの[!UICONTROL Real-time Customer Profile]を使用してAdobe Experience Platformにアクセスし、高スループットで低遅延のパーソナライズを実現する方法を示しています。

アプリケーションは、ミリ秒単位の遅延で、エッジにあるリアルタイムのプロファイル属性およびオーディエンスにアクセスできます。 プロファイルに属性、オーディエンスメンバーシップ、モデル駆動機能を属性として保存し、webとモバイルのチャネル全体で同じページと次のページのパーソナライゼーションをリアルタイムで実行できます。

この機能を利用すれば、リアルタイムの行動から得られるオーディエンス、リアルタイムの顧客プロファイルに取り込まれた属性、計算されたインサイトなど、リアルタイムの顧客プロファイルにもとづいて、web サイトやモバイルアプリケーションで、高度にパーソナライズされた体験を提供できます。

>[!NOTE]
>
>Edgeのプロファイルアクセスは、webやモバイルのインバウンドパーソナライゼーション、リアルタイムのオファー決定など、スループットが高く低遅延のユースケース向けに設計されています。 エージェントによるサポートやセールスインタラクションなど、スループットが低いシナリオの場合は、Hub プロファイル参照APIの方が適切です。 ハブベースのプロファイルアクセスについては、[&#x200B; サポートおよびセールスシナリオのリアルタイムプロファイルアクセスの設計図](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md)を参照してください。

## アプリケーション

* Real-time Customer Data Platform
* Adobe Experience Platform Data Collection （Web SDK / モバイルSDK）
* Edge Network Server API

## ユースケース

* webとモバイルのチャネルでリアルタイムにパーソナライズされ、既知の顧客体験を提供
* リアルタイムのプロファイル属性とオーディエンスにもとづく、同一ページと次のページのパーソナライゼーション
* リアルタイムの行動データ、属性、計算されたインサイトなど、顧客プロファイルにもとづくコンテンツとオファーのパーソナライゼーションを実現します
* パーソナライゼーションエンジン、コンテンツ管理システム、外部アプリケーションとの統合によるリアルタイムの意思決定
* リアルタイムのプロファイルコンテキストによるテストとコンテンツ最適化

## 前提条件

このブループリントでは、ストリーミングデータを使用してプロファイルをリアルタイムで更新する場合は、次のいずれかのデータ収集方法を使用する必要があります。 Edge プロファイルに直接データを収集することなく、Edge プロファイルにリアルタイムにアクセスできます。データはハブに収集され、Edge プロファイルにも投影できます。 Hubに収集されたデータに対して、Edgeに投影される遅延が追加されることに注意してください。

* Web サイトからデータを収集する場合は、[Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=ja)を使用します。
* モバイルアプリケーションからデータを収集する場合は、[Adobe Experience Platform モバイルSDK](https://developer.adobe.com/client-sdks/home/)を使用します。
* Web SDKまたはモバイル SDKを使用していない場合、またはサーバー間のより直接的な接続を実装している場合は、[Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)を使用します。

>[!IMPORTANT]
>
>エッジパーソナライゼーションを実装する前に、オーディエンスデータをエッジパーソナライゼーション宛先に[&#x200B; アクティベートする方法](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)に関するガイドを参照してください。 このガイドでは、複数のExperience Platform コンポーネントをまたいで、同じページと次のページのパーソナライゼーションのユースケースに必要な設定手順について説明します。

## アーキテクチャ図

<img src="/help/blueprints/audience-activation/assets/real-time-edge-lookup.svg" alt="WebおよびモバイルPersonalization用Edge プロファイルアクセスのリファレンスアーキテクチャ" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## ガードレール

* [[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] データのガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)
* [Edge Network ガードレール](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Edge プロファイルには、14日間の有効期間（TTL）があります。 ユーザーが14日間エッジでアクティブでなかった場合、エッジプロファイルは期限切れになり、ハブから取得する必要が生じる可能性があり、最初のページのパーソナライゼーションに影響を与える可能性があります。
* Edge personalizationは、エッジセグメント化の条件を満たすオーディエンスに対して、リアルタイムのオーディエンスメンバーシップの評価をサポートします。 ハブからのバッチオーディエンスとストリーミングオーディエンスも、適切な設定でエッジで利用できます。

## 実装パターン

Edgeのパーソナライゼーションは、Real-time Customer Data Platformの[&#x200B; カスタム Personalization Connection](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization)宛先を使用して実装できます。 この宛先では、ユースケースに応じて複数のデータ収集方法をサポートしています。

### パターン 1:Web SDKとモバイルSDKを利用した、オーディエンスメンバーシップベースのパーソナライゼーション

* Adobe Experience Platform Web SDKまたはモバイルSDKとEdge Networkを併用すると、オーディエンスメンバーシップにもとづいたパーソナライゼーションが可能です。
* このアプローチは、オーディエンスメンバーシップにもとづくエッジパーソナライゼーションに低遅延で最高のパフォーマンスをもたらします。
* リアルタイムのエッジセグメント化には、Web/Mobile SDKを導入する必要があります。
* Web SDKとモバイル SDK **だけでも、オーディエンスメンバーシップに基づくパーソナライゼーションをサポートします**。
* [SDK ベースの実装については、Experience Platform Webおよびモバイル SDK ブループリント &#x200B;](/help/blueprints/experience-platform/deployment/websdk.md)を参照してください。
* Mobile SDKを実装する場合、[Adobe Journey Optimizer - Decisioning拡張機能](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/)をMobile SDKにインストールする必要があります。

### パターン 2:Edge Network Server APIを使用した属性ベースのパーソナライゼーション（プロファイル属性に必要）

>[!IMPORTANT]
>
>**属性ベースのパーソナライゼーション要件：** プロファイル属性（オーディエンスメンバーシップだけでなく）に基づいてパーソナライズする場合、**は、Web SDKまたはMobile SDKをデータ収集に使用しているかどうかに関係なく、認証済みのサーバーサイド統合で[Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)を**&#x200B;使用する必要があります。

* サードパーティのパーソナライゼーションエンジンやCDN ベースのパーソナライゼーションとの統合が可能です。
* パーソナライゼーション用のプロファイル属性を安全に取得するには、Edge Network Server APIが&#x200B;**必要です**。
* Edge Network Server APIを使用して、WebまたはMobile SDKの実装に既に使用しているのと同じデータストリームを使用するサーバーサイド統合を追加することで、プロファイル属性を取得できます。
* プロファイル属性に対するすべてのEdge Network Server API呼び出しは、機密データを保護するために、認証済みコンテキストで行う必要があります。
* このパターンにより、オーディエンスメンバーシップベースのパーソナライゼーションと属性ベースのパーソナライゼーションの両方が可能になります。
* サーバーサイドのパーソナライゼーションのユースケース、API ベースの統合、プロファイル属性へのアクセスを必要とするシナリオに適しています。

## 実装手順

1. データを取り込むために[スキーマを作成](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&lang=ja)します。
1. データを取り込むために[データセットを作成](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ja)します。
1. [取り込んだデータを統合プロファイルに結合できるように、スキーマ上で正しいIDとID名前空間](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ja)を設定します。
1. [プロファイル用のスキーマおよびデータセットを有効にします](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ja)。
1. Experience Platform に[データを取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&lang=ja)。
1. [結合ポリシー](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ja)を設定して、正しいID ステッチとプロファイルの結合を確実に行います。
1. 宛先設定を有効にして、Experience Platform Data Collectionで[&#x200B; データストリーム &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ja)を設定します。 データストリームは、ページへの応答にオーディエンスを含めるデータ収集データストリームを決定します。
1. Webおよびモバイルのプロパティに[Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=ja)または[&#x200B; モバイル SDK](https://developer.adobe.com/client-sdks/home/)を実装してデータ収集を行います。
1. リアルタイムの評価が必要なオーディエンスに対して、エッジセグメント化を設定します。 [Edge セグメント化ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ja)。
1. 宛先カタログで、[&#x200B; カスタム Personalization Connection](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization)の宛先を設定します。
1. [&#x200B; エッジ パーソナライゼーションの宛先に対してオーディエンスをアクティブ化](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)。 宛先に対してアクティブ化するオーディエンスを選択します。
1. （属性ベースのパーソナライゼーションの場合はオプション）オーディエンスメンバーシップに加えてプロファイル属性に基づいてパーソナライズする必要がある場合は、同じデータストリームを使用して、認証済みのサーバーサイド統合を使用して[Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)を実装します。 プロファイル属性にアクセスするには&#x200B;**必須**&#x200B;です。
1. web/モバイルアプリケーションにパーソナライゼーションロジックを実装して、書き出されたオーディエンスデータとプロファイル属性を使用します。
   * Adobe Experience PlatformでTagsを使用する場合は、[send event complete機能](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja)を使用して、書き出されたデータを含む`event.destinations`変数にアクセスします。
   * タグを使用しない場合は、[&#x200B; コマンド応答](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html?lang=ja)を使用して、Adobe Experience PlatformからJSON応答を解析し、オーディエンス IDとプロファイル属性を取得します。

## 実装に関する考慮事項

### IDに関する検討事項

* Web SDKまたはモバイル SDKとEdge Networkを使用する場合は、任意のプライマリ IDをエッジパーソナライゼーションに使用できます。
* 既知の顧客データを使用した最初のログインのパーソナライゼーションを行うには、パーソナライゼーションリクエストで、Real-time Customer Data Platformの既知の顧客IDと一致するプライマリ IDを使用する必要があります。 プライマリ IDがECIDまたは既知の顧客プロファイルにまだステッチされていない匿名IDに設定されている場合、ID ステッチが実現されるまでに時間がかかり、パーソナライゼーションの過去のプロファイルデータの可用性に影響を与える可能性があります。
* Edge プロファイルは、パーソナライゼーションに使用する前に初期化する必要があります。 エッジプロファイルの有効期限（14日間TTL）が切れた初回訪問者または再訪問者は、エッジプロファイルが完全に入力されるまで、限られたプロファイルデータに基づいて初期パーソナライゼーションを受ける場合があります。

### 属性ベースのパーソナライゼーション

>[!IMPORTANT]
>
>プロファイル属性には、機密データが含まれる場合があります。 このデータを保護するには、**属性ベースのパーソナライゼーション用にカスタム Edge Networkの宛先を設定する際に、[Personalization Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)を使用する必要があります**。 すべてのEdge Network Server API呼び出しは、認証済みコンテキストで行う必要があります。

* プロファイル属性を使用した属性ベースのパーソナライゼーションの場合は、WebまたはMobile SDKの実装に使用するのと同じデータストリームを使用するEdge Network Server APIとサーバーサイド統合を追加する必要があります。
* エッジ投影に含めるプロファイル属性は、カスタム Personalization Connectionの宛先設定を使用して設定する必要があります。
* **Web SDKとモバイル SDKだけでも、オーディエンスメンバーシップに基づくパーソナライゼーションのみがサポートされます**。 パーソナライゼーション用のプロファイル属性を安全に取得するには、Edge Network Server APIが&#x200B;**必要です**。
* 属性アクセス用にEdge Network Server APIを実装しない場合、パーソナライゼーションはオーディエンスメンバーシップのみに基づきます。
* カスタム Personalizationの属性を含むAPI応答には、オーディエンスセグメントに加えて`attributes` セクションが含まれます。

### オーディエンスの考慮事項

* ストリーミングまたはハブでのバッチセグメント化によって評価されたオーディエンスは、エッジに投影され、パーソナライゼーションに使用できます。
* エッジのセグメント化基準を満たすオーディエンスは、エッジ上でリアルタイムに評価され、同じページでパーソナライズされます。
* リアルタイムのパーソナライゼーションのユースケースでの使用に基づいて、エッジ評価に適切なオーディエンスを設定します。

## 関連ドキュメント

### 配信先設定

* [&#x200B; カスタム Personalization Connection](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - プライマリ実装ガイド
* [Personalizationの宛先の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/overview)
* [エッジのパーソナライゼーション宛先に対するオーディエンスのアクティブ化](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [エッジ上のプロファイル属性をリアルタイムで検索し](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### SDK ドキュメント

* [Experience Platform Web SDKのドキュメント](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html?lang=ja)
* [Experience Platform Mobile SDKのドキュメント](https://developer.adobe.com/client-sdks/home/)
* [Edge Network Server API ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ja)
* [Experience Platform Tags ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)
* [Web SDKでのコマンド応答](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html?lang=ja)

### プロファイルとセグメント化に関するドキュメント

* [[!UICONTROL &#x200B; リアルタイム顧客プロファイル &#x200B;] ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ja)
* [プロファイルガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)

### チュートリアル

* [Real-Time CDPとAdobe Targetによる次のヒットのパーソナライゼーション](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ja)
* [データストリーム設定](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ja)
