---
title: データアクセスと書き出しブループリント
description: このブループリントは、Adobe Experience Platform およびアプリケーションからデータにアクセスしてエクスポートするためのすべての方法の概要を提供します。
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-Time Customer Data Platform, Tags
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 94%

---

# データアクセスと書き出しブループリント

データアクセスおよびブループリント書き出しは、Adobe Experience Platform およびアプリケーションからデータにアクセスまたはエクスポートできるすべての可能な方法の概要を示しています。

ブループリントは、Experience Platform とアプリケーションからのデータアクセス用に、2 つのカテゴリに分類されます。第 1 に、Experience Platform やアプリケーションからデータを送り出すためのアプローチ。これは、プッシュ型のデータ送り出し方法と見なされます。第 2 に、Experience Platform とアプリケーションからデータにアクセスするためのアプローチ。 これは、プル型のデータアクセス方法と見なされます。

データアクセスのアプローチ：

* [リアルタイム顧客プロファイルアクセス API](#rtcp-profile-access-api)
* [データアクセス API](#data-access-api)
* [クエリサービス](#query-service)

データエクスポートのアプローチ：

* [クライアント側タグ](#client-side-tags-extensions)
* [イベント転送](#event-forwarding)
* [Real-time Customer Data Platform Destinations](#RTCDP-destinations)
* [Journey Optimizer カスタムアクション](#jo-custom-actions)

## データのアクセスと書き出しの概要アーキテクチャ

<img src="../experience-platform/assets/aep_data_flow.svg" alt="データ準備と取り込みブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" />

## データアクセスのためのアプローチ

### リアルタイム顧客プロファイルアクセス API {#rtcp-profile-access-api}

顧客は、リアルタイム顧客プロファイルアクセス API を使用して、すべてのプロファイル ID、オーディエンスメンバーシップ、属性、エクスペリエンスイベントを含む、リアルタイム顧客プロファイル格納から単一の統合プロファイルにアクセスすることができます。

詳しくは、 [リアルタイム顧客プロファイルアクセス API](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=ja) ドキュメントを参照してください。

#### 使用例

* 単一のプロファイルを検索して、チャットやコールセンターを通じたサポートインタラクション、店頭でのセールスインタラクションなど、エージェントの顧客インタラクションにコンテキストを追加します。
* 外部システム（Web パーソナライゼーションシステムやオファー決定支援システムなど）によっておこなわれるパーソナライゼーションの決定に、コンテキストの追加を許可します。

#### 注意点

* リアルタイム顧客プロファイル[ガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)が適用されます。
* 一度に 1 つのプロファイル参照用に設計されています。一括プロファイルアクセスや、分析やデータ サイエンスに使用するプロファイル母集団全体のダウンロードには使用されません。
* プロファイル参照の応答時間は、プロファイルガードレールに従います。リアルタイムの低遅延要件（同じページのパーソナライゼーション要件の場合など）は、[Adobe Target 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja) または [カスタムパーソナライゼーション接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=ja)から Edge プロファイルを利用して、ブラウザー内およびアプリ内パーソナライゼーションのリアルタイムプロファイルアクセスを行う必要があります。

### データアクセス API {#data-access-api}

データアクセス API を使用すると、顧客が Experience Platform データレイクに保存されている生データのセットファイルに直接アクセスすることができます。

* データアクセス API の使用に関する詳細は、[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=ja)を参照してください。

#### 使用例

* エンタープライズ環境での保存と評価のために、生データファイルと処理済みデータファイルを Experience Platform からプルします。

#### 注意点

* データにバッチ非同期でアクセスすると、タグの活用、イベント転送、RTCDP 宛先などのストリーミングデータ送り出しのアプローチと比較して、データへのアクセスは潜在的に遅延します。
* データファイルが Experience Platform に取り入れられて処理されると、ファイルのコレクションとしてバッチで保存され、圧縮されて Parquet 形式で保存されます。したがって、ファイルにアクセスして別の環境にダウンロードする場合は、データセット全体ではなく、バッチとファイルによって体系的にアクセスする必要があり、データに対する操作では、parquet 形式で圧縮されているファイルを考慮する必要があります。

### クエリサービス {#query-service}

Experience Platform クエリサービスを使用すると、顧客は Experience Platform 内でデータセットに対してクエリを実行し、クエリの結果を保持することができます。SQL クライアントを使用してクエリを実行し、SQL クライアントがサポート可能な目的の保存先に、クエリのレスポンスを保持することができます。クエリサービス UI を使用して、SQL 結果を Experience Platform 内のターゲットデータセットに保存したり、結果をローカルマシンに保存したりすることができます。

* Experience Platform クエリサービスからの SQL 結果を保持するための SQL クライアントへの接続の詳細については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=ja)を参照してください。

#### 使用例

* Experience Platform データセットから生データをクエリし、クエリ結果を保持します。
* プロファイルスナップショットデータセットをクエリして、リアルタイム顧客プロファイルのインサイトを抽出します。[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=ja#profile-attribute-datasets)。
* クエリ結果を、アクセス用に別のデータセットに保存するか、RTCDP やリアルタイム顧客プロファイルにアクセスするその他の Experience Cloud アプリケーションを介して後で出力できるプロファイル対応のデータセットに保存します。

#### 注意点

* データがバッチ非同期的にクエリされるため、タグの活用、イベント転送、RTCDP 宛先などのストリーミングデータ送り出しのアプローチと比較して、データへのアクセスは潜在的に遅延します。
* Experience Platform データレイクで使用可能なデータのみが、クエリサービスを使用してクエリすることができます。リアルタイム顧客プロファイル格納、ID グラフ、Customer Journey Analytics は、クエリサービスを使用して直接クエリすることができません。プロファイルスナップショットデータセットの例に示すように、データセットがデータレイクにエクスポートされている場合にのみ、これらのデータセットをクエリすることができます。
* クエリ結果の数とクエリタイムアウトのガードレールは、[クエリサービスガードレール](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ja)ドキュメントで概説されているように適用されることご注意ください。

## データエクスポートのためのアプローチ

### クライアント側タグ拡張 {#client-side-tags-extensions}

拡張機能は、アドビのタグソリューションを使用してデプロイすることができます。拡張機能がデプロイされると、データリクエストがクライアントブラウザーまたはアプリケーションに直接デプロイされ、リクエストを呼び出して、目的の宛先にデータとリクエストを送信することができます。

詳しくは、[タグの概要](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)ドキュメントを参照してください。

#### 使用例

* タグ付けを使用して、クライアント側の環境から直接生のストリーミング情報を収集します。

#### 注意点

* Experience Platform のリアルタイム顧客プロファイルやオーディエンスメンバーシップなど、サーバー側の情報に直接アクセスすることはできません。
* ページにデータ収集タグを追加すると、ページの読み込み時間が長くなる場合があります。
* 特定の条件が満たされた場合にのみデータをリクエストするルールを設定する機能。
* データはクライアントから直接収集され、データ収集の前に実行することができる変換とエンリッチメントのタイプを制限します。

### イベント転送 {#event-forwarding}

データ収集リクエストは、アドビの Edge ネットワークに直接収集されます。Edge ネットワークリクエストから外部 RESTful エンドポイントに対して、これらのリクエストを外部の宛先に転送するように設定することができます。

詳しくは、以下の[イベント転送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja)ドキュメントを参照してください。

#### 使用例

* アドビのサーバー側イベント転送を使用して、生のストリーミング情報をクライアント側環境からエンタープライズエンドポイントに直接収集します。

#### 注意点

* イベント転送を使用するには、Web SDK または MobileSDK を使用して Edge ネットワークにデータを送信する必要があります。
* イベント転送のアプローチでは、ページにタグが追加されるので、ページの読み込み時間と重み付けが軽減されます。
* エッジプロファイルまたは他のデータソースからのエンリッチメントは、現在サポートされていません。
* 限定的なデータフィルタリングと単純なマッピング変換がサポートされています。

### Real-time Customer Data Platformの宛先 {#RTCDP-destinations}

プロファイル属性データとオーディエンスメンバーシップデータを、企業や広告の宛先に対してアクティブ化することができます。これは、送信されたデータを Experience Platform のリアルタイム顧客プロファイルに取り込む必要があることを意味します。

詳しくは、 [Real-time Customer Data Platform Destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=ja) ドキュメントを参照してください。

#### 使用例

* 内部エンタープライズデータ格納、分析ツール、電子メールシステムやサポートシステムへのオーディエンスメンバーシップを含む、プロファイル属性情報をアクティブ化します。
* 外部の広告ベンダーに対してプロファイルオーディエンスのメンバーシップをアクティブ化し、プロファイルに対するコンテンツのターゲティングとパーソナライズを行います。

#### 注意点

* プロファイル属性とオーディエンスメンバーシップをアクティブ化することができます。生のエクスペリエンスイベントは現在、RTCDP の宛先の一部としては、アクティブ化することができません。
* セグメント評価の特性と、宛先が受け入れる取り込みプロトコルの特性に応じて、ストリーミングまたはバッチで、アクティブ化が発生します。

### Journey Optimizerのカスタムアクション {#jo-custom-actions}

Journey Optimizer を使用すると、顧客はジャーニーキャンバスからカスタムアクションを呼び出して、設定された外部 API エンドポイントにペイロードまたはメッセージを送信することができます。アクションは、JSON 形式のペイロードを使用して REST API を介して呼び出すことができる任意のプロバイダーの任意のサービスに対して設定することができます。このペイロードには、イベント情報、プロファイル属性と以前のイベントデータ、ジャーニーで設定された変換とエンリッチメントを含めることができます。

詳しくは、 [Journey Optimizer のカスタムアクション](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=ja)ドキュメントを参照してください。

#### 使用例

* リアルタイム顧客プロファイルからの追加情報を含む Experience Platform および Journey Optimizer からのアクティベーションイベント。
* 顧客がジャーニーの特定のポイントに到達したときに、外部システムに通知します。

#### 注意点

* [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=ja)によってサポートされるスループットのガードレール、および[リアルタイム顧客プロファイル](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)によってサポートされるエンリッチメントのガードレールに適用されます。
* カスタムアクションは、ジャーニーのイベントまたはプロファイルごとに 1 つずつストリーミングで実行することができます。ファイルまたはカスタマージャーニー全体の集約されたリクエストの形式での一括操作または一括データ送信は、実行することができません。
* アクティベーションペイロードに含めることができる、リアルタイム顧客プロファイル属性とエクスペリエンスイベントへのストリーミングアクセス。
* イベントを外部の宛先に送信する前に、イベントデータをフィルタリングし、単純なマッピング変換を適用することができます。
