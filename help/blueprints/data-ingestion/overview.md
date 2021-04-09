---
title: データ収集と準備
description: この設計図は、Adobe Experience Platformでデータを取り込み、調製する方法をすべて示しています。
solution: Experience Platform, Data Collection
kt: 7204
thumbnail: null
exl-id: 5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
translation-type: tm+mt
source-git-commit: ee1d97af9bf58076fbce24fbc8a3f0d50a4b52a0
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# データの収集と準備

データ収集と準備には、データを作成し、Adobe Experience Platformに取り込むためのすべての方法が含まれます。 また、Adobe Experience Platformのエッジネットワークにデータを収集する機能、および側面転送を介した企業の宛先へのデータの転送機能。

データの準備には、ソースデータとエクスペリエンスデータモデル(XDM)スキーマとのマッピングが含まれます。 また、日付形式、フィールド分割/連結/変換、レコードの結合/結合/再入力など、データに対する変換も実行されます。 データの準備は、顧客データの統合を支援し、レポートや顧客プロファイルの分析/データ科学/アクティベーションのためのデータを含む、集計/フィルタリングされたを提供します。

| Blueprint | 説明 | Experience Cloudアプリ |
|---|---|---|
| **[データの準備とExperience Platformへの取り込み](ingestion.md)** | <ul><li>データの準備と取り込みのブループリントには、データを準備し、Adobe Experience Platformに取り込むためのすべての方法が含まれます。</ul></li> | <ul><li> Adobe Experience Platform </ul></li> |
| **[サーバー側転送 — エンタープライズコレクション](server-side-collection.md)** | <ul><li>電子メールプロバイダー、ソーシャルネットワーク、広告先など、既知のプロファイルベースの送信先に対してアクティブ化します。 </li><li>オフライン注文、トランザクション、CRM、忠誠度データなどのオフライン属性やイベントを、オンラインでのターゲティングとパーソナライゼーションのためのオンライン行動と共に使用します。</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL リアルタイム顧客データプラットフォーム]</li><li>Adobe Audience Manager（オプション）</li></ul> |
