---
title: データアクセスと書き出しブループリント
description: このブループリントは、Adobe Experience Platformおよびアプリケーションからデータにアクセスし、書き出す方法の概要と概要を提供します。
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-time Customer Data Platform, Tags
source-git-commit: 67e66068bb8a2106dd8aa9784b5a39377225c045
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 4%

---

# データアクセスと書き出しブループリント

データアクセスおよび書き出しブループリントでは、Adobe Experience Platformおよびアプリケーションからデータにアクセスまたは書き出しできる、すべての方法の概要を説明しています。

ブループリントは、Experience Platformとアプリケーションからのデータアクセス用に、2 つのカテゴリに分類されます。 第 1 に、Experience Platformやアプリケーションからデータを取り出す方法これは、データエグレスのプッシュタイプの方法と見なされます。 第 2 に、Experience Platformやアプリケーションからのデータへのアクセスのアプローチこれは、データアクセスのプルタイプの方法と考えられます。

データアクセスのアプローチ

* [リアルタイム顧客プロファイルアクセス API](#rtcp-profile-access-api)
* [データアクセス API](#data-access-api)
* [クエリサービス](#query-service)

データ書き出し方法

* [クライアント側タグ](#client-side-tags-extensions)
* [イベント転送](#event-forwarding)
* [Real-time Customer Data Platform Destinations](#RTCDP-destinations)
* [Journey Optimizer Custom Actions](#jo-custom-actions)

## データのアクセスと書き出しの概要アーキテクチャ

<img src="../experience-platform/assets/aep_data_flow.svg" alt="データ準備と取り込みブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a" />

## データアクセスのアプローチ

### リアルタイム顧客プロファイルアクセス API {#rtcp-profile-access-api}

顧客は、リアルタイム顧客プロファイルアクセス API を使用して、すべてのプロファイル ID、オーディエンスメンバーシップ、属性、エクスペリエンスイベントを含む、リアルタイム顧客プロファイルストアから単一の統合プロファイルにアクセスできます。

詳しくは、 [リアルタイム顧客プロファイルアクセス API](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en) ドキュメントを参照してください。

#### ユースケース

* 単一のプロファイルを参照して、チャットやコールセンターを通じたサポートインタラクション、販売時点でのセールスインタラクションなど、エージェントの顧客インタラクションにコンテキストを追加します。
* 外部システム（Web パーソナライゼーションシステムやオファー決定システムなど）によっておこなわれるパーソナライゼーションの定義に、追加されたコンテキストを許可します。

#### 注意点

* リアルタイム顧客プロファイル [guardrail](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) 適用されます。
* 一度に 1 つのプロファイル参照用に設計されています。 分析やデータサイエンスを使用するために、プロファイル母集団全体の一括プロファイルアクセスやダウンロードには使用されません。
* プロファイル参照の応答時間は、プロファイルガードレールに従います。 待ち時間が短い要件 — 同じページのパーソナライゼーション要件の場合は、Edge プロファイルや顧客のパーソナライゼーションの宛先を利用して、待ち時間が短いプロファイルにアクセスする必要があります。 [ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en).

### データアクセス API {#data-access-api}

データアクセス API を使用すると、ユーザーはデータレイクに保存されている生のデータセットファイルに直接Experience Platformできます。

* データアクセス API の使用に関する詳細は、 [ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=en).

#### ユースケース

* エンタープライズ環境での保存と評価のために、生データファイルと処理済みデータファイルをExperience Platformから抽出します。

#### 注意点

* データにバッチ非同期的にアクセスすると、タグの活用、イベント転送、RTCDP 宛先などのストリーミングデータエグレスアプローチと比較して、データへのアクセスは本質的に遅延します。
* データファイルをExperience Platformに処理する際は、ファイルのコレクションとしてバッチで保存され、圧縮されて Parquet 形式で保存されます。 したがって、異なる環境にファイルにアクセスしてダウンロードする場合は、バッチとファイルでデータセット全体に対応するように体系的にアクセスし、データに対する操作には、Parquet 形式で圧縮されるファイルを考慮する必要があります。

### クエリサービス {#query-service}

Experience Platform クエリサービスを使用すると、顧客はExperience Platform内でデータセットに対してクエリを実行し、クエリの結果を保持できます。 SQL Client は、SQL クライアントを使用してクエリを実行し、SQL クライアントがサポートできる目的のストレージ宛先にクエリ応答を保持できます。 クエリサービス UI を使用して、SQL 結果をExperience Platform内のターゲットデータセットに保存したり、結果をローカルマシンに保存したりできます。

* Experience Platformクエリサービスから SQL 結果を保持するための SQL クライアントへの接続の詳細については、次を参照してください [ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=en).

#### ユースケース

* Experience Platformデータセットから生データをクエリし、クエリ結果を保持します。
* プロファイルスナップショットデータセットをクエリして、リアルタイム顧客プロファイルのインサイトを抽出します。 [ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets).
* クエリの結果を別個のデータセットに格納してアクセスするか、プロファイル対応データセットに格納します。このデータセットは、後で RTCDP や、リアルタイム顧客プロファイルにアクセスする他のExperience Cloudアプリケーションを通じて登録できます。

#### 注意点

* データがバッチ非同期方式で照会されると、タグの活用、イベント転送、RTCDP 宛先などのストリーミングデータエグレスアプローチと比較して、データへのアクセスは本質的に遅延します。
* クエリサービスを使用してクエリできるのは、Experience Platformデータレイクで使用可能なデータのみです。 リアルタイム顧客プロファイルストア（ID グラフ）Customer Journey Analyticsをクエリサービスを使用して直接クエリすることはできません。 プロファイルスナップショットデータセットの例に示すように、データセットがデータレイクに書き出された場合にのみ、これらのデータセットをクエリできます。
* クエリ結果の数とクエリタイムアウトのガードレールは、「 [クエリサービスガードレール](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en) ドキュメント。

## データエクスポートのアプローチ

### クライアントサイドタグ拡張 {#client-side-tags-extensions}

拡張機能は、Adobeのタグソリューションを使用してデプロイできます。 拡張機能がデプロイされると、データリクエストがクライアントブラウザーまたはアプリケーションに直接デプロイされ、リクエストを呼び出して、目的の宛先にデータとリクエストを送信できます。

詳しくは、 [タグの概要](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en) ドキュメントを参照してください。

#### ユースケース

* タグ付けを使用して、クライアント側の環境から直接生のストリーミング情報を収集します。

#### 注意点

* Experience Platformのリアルタイム顧客プロファイルやオーディエンスメンバーシップなど、サーバー側の情報に直接アクセスすることはできません。
* ページにデータ収集タグを追加すると、ページの読み込み時間が長くなる場合があります。
* 特定の条件が満たされた場合にのみデータをリクエストするルールを設定できる。
* データはクライアントから直接収集され、データ収集の前に実行できる変換とエンリッチメントのタイプを制限します。

### イベント転送 {#event-forwarding}

データ収集リクエストは、Adobeの Edge ネットワークに直接収集されます。 Edge ネットワークリクエストから外部 RESTful エンドポイントに対して、これらのリクエストを外部の宛先に転送するように設定できます。

次を参照してください。 [イベント転送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en) ドキュメントを参照してください。

#### ユースカジア

* Adobeのサーバー側イベント転送を使用して、クライアント側の環境からエンタープライズエンドポイントに生のストリーミング情報を直接収集します。

#### 注意点

* イベント転送を使用するには、WebSDK または MobileSDK を使用して Edge ネットワークにデータを送信する必要があります。
* イベント転送のアプローチは、ページにタグが追加されるので、ページの読み込み時間と重み付けを軽減します。
* 現在、エッジプロファイルまたは他のデータソースからのエンリッチメントはサポートされていません。
* 制限付きのデータフィルタリングと単純なマッピング変換がサポートされます。

### Real-time Customer Data Platform Destinations {#RTCDP-destinations}

プロファイル属性データとオーディエンスメンバーシップデータを、企業や広告の宛先に対してアクティブ化できます。 つまり、送信されたデータは、Experience Platformのリアルタイム顧客プロファイルに取り込む必要があります。

詳しくは、 [Real-time Customer Data Platform Destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=ja) ドキュメントを参照してください。

#### ユースケース

* プロファイル属性情報（社内データストア、分析ツール、電子メールシステム、サポートシステムへのオーディエンスメンバーシップを含む）をアクティブ化します。
* 外部の広告ベンダーに対してプロファイルオーディエンスのメンバーシップをアクティブ化し、プロファイルに対するコンテンツのターゲティングとパーソナライズをおこないます。

#### 注意点

* プロファイル属性とオーディエンスメンバーシップをアクティブ化できます。 生のエクスペリエンスイベントは、現在、RTCDP の宛先の一部としてアクティブ化できません。
* セグメント評価の特性と、宛先が受け入れる取り込みプロトコルの特性に応じて、ストリーミングまたはバッチでアクティベーションが発生します。

### Journey Optimizer Custom Actions {#jo-custom-actions}

Journey Optimizerのお客様は、ジャーニーキャンバスからカスタムアクションを呼び出し、設定された外部 API エンドポイントにペイロードまたはメッセージを送信できます。 アクションは、JSON 形式のペイロードを持つ REST API を介して呼び出すことのできる任意のプロバイダーから任意のサービスに設定できます。 このペイロードには、イベント情報、プロファイル属性、以前のイベントデータ、変換、ジャーニーで設定されたエンリッチメントを含めることができます。

詳しくは、 [Journey Optimizerのカスタムアクション](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en) ドキュメントを参照してください。

#### ユースケース

* Experience PlatformおよびJourney Optimizerのアクティベーションイベント（リアルタイム顧客プロファイルからの追加情報を含む）。
* 顧客がジャーニーの特定のポイントに到達したら、外部システムに通知します。

#### 注意点

* でサポートされるスループットのガードレール [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en) そして、 [リアルタイム顧客プロファイル](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) 適用されます。
* カスタムアクションは、ジャーニーのイベントまたはプロファイルごとに 1 つずつストリーミングで実行できます。 カスタマージャーニーをまたいだファイルの形式での一括操作または一括データ出力は実行できません。
* アクティベーションペイロードに含めることができる、リアルタイム顧客プロファイル属性とエクスペリエンスイベントへのストリーミングアクセス。
* イベントを外部の宛先に送信する前に、イベントデータをフィルタリングし、単純なマッピング変換を適用することができます。










