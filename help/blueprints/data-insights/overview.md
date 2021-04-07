---
title: データ分析、インテリジェンス、AI/ML
description: この設計図は、Adobe Experience Platform内で、データレーク内に存在するデータの調査クエリと分析を実行する機能を示しています。
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039
translation-type: tm+mt
source-git-commit: f5d8b3fea11df0ffaeb59f0b53e93d76426ef252
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# データ分析、インテリジェンス、AI/ML

企業データの調査とレポートは、Adobe Experience Platform内でデータレーク内に存在するデータの調査クエリと分析を実行する機能を備えています。

Experience Platformのクエリサービスを使用すると、SQLクエリをデータに対して実行できます。 Data Science Workspaceを使用すると、データ調査、データ科学、および機械学習のワークロードをデータに対して実行できます。

さらに、Experience Platformは、サードパーティのSQLクライアント、インタフェース、およびBusiness Intelligence(BI)ツールとの接続を、PostgreSQLプロトコルを使用して、Experience Platform内のデータに直接接続し、アクセスし、クエリすることを可能にします。

シナリオの詳細に示すように、クエリのタイムアウトと、クエリ結果に含まれるデータ量に適用されるガードレールもあります。

## ブループリント

| Blueprint | 説明 | Experience Cloudアプリ |
|---|---|---|
| **[データ分析とインテリジェンス](analysis.md)** | <ul><li>データの準備と取り込みのブループリントには、データを準備し、Adobe Experience Platformに取り込むためのすべての方法が含まれます。</ul></li> | <ul><li> Adobe Experience Platform </ul></li> |
| **[プロファイルエンリッチメント設計図のカスタムデータサイエンス](data-science.md)** | <ul><li>電子メールプロバイダー、ソーシャルネットワーク、広告先など、既知のプロファイルベースの送信先に対してアクティブ化します。 </li><li>オフライン注文、トランザクション、CRM、忠誠度データなどのオフライン属性やイベントを、オンラインでのターゲティングとパーソナライゼーションのためのオンライン行動と共に使用します。</li></ul> | <ul><li>Adobe Experience Platform</li><li> リアルタイム顧客データプラットフォーム</li><li>Adobe Audience Manager（オプション）</li></ul> |
