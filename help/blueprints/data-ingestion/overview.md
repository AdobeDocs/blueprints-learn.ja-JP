---
title: データ収集と準備
description: Adobe [!DNL Experience Platform] でデータを取得し、準備する方法を説明します。
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 61%

---

# データ収集と準備のブループリント

データの収集と準備には、データを準備してAdobe[!DNL Experience Platform] に取り込めるすべての方法が含まれます。 データをAdobe[!DNL Experience Platform Edge Network] に収集する機能と、その後のエンタープライズ宛先へのサイド転送を介したデータの転送。

データ準備には、エクスペリエンスデータモデル（XDM）スキーマへのソースデータのマッピングが含まれます。また、データ変換（日付形式、フィールドの分割／連結／コンバージョン、レコードの結合／キー更新など）の実行も含まれます。データ準備は、顧客データを統合して、集計／フィルタリングされた分析を提供するのに役立ちます。これには、レポート作成や顧客プロファイルの組み立て／データサイエンス／アクティベーションのためのデータ準備が含まれます。

| ブループリント | 説明 | Experience Cloud アプリケーション |
|---|---|---|
| **[データ準備と取り込み](ingestion.md)** | <ul><li>データの準備と取り込みのブループリントには、データを準備してAdobe[!DNL Experience Platform] に取り込むことができるすべての方法が含まれています。</ul></li> | <ul><li> アドビ [!DNL Experience Platform] </ul></li> |
| **[サーバーサイドエンタープライズデータ収集](server-side-collection.md)** | <ul><li>既知のプロファイルベースの宛先（電子メールプロバイダー、ソーシャルネットワーク、広告など）に対してアクティブ化します。 </li><li>オンラインビヘイビアーと共に、オフライン属性およびイベント（オフラインの注文、トランザクション、CRM またはロイヤリティデータなど）を、オンラインターゲティングとパーソナライズ機能に使用します。</li></ul> | <ul><li>アドビ [!DNL Experience Platform]</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager（オプション）</li></ul> |
