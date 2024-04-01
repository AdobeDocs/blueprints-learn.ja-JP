---
title: データ収集と準備
description: Adobe Experience Platformでデータを取り込み、準備する方法について説明します。
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 80%

---

# データ収集と準備のブループリント

データ収集と準備は、データを準備して Adobe Experience Platform に取り込むためのすべての方法を網羅しています。さらに、Adobeに対してデータを収集する機能 [!DNL Experience Platform Edge Network] およびを使用したエンタープライズ宛先へのサイド転送の後続のデータ転送。

データ準備には、エクスペリエンスデータモデル（XDM）スキーマへのソースデータのマッピングが含まれます。また、データ変換（日付形式、フィールドの分割／連結／コンバージョン、レコードの結合／キー更新など）の実行も含まれます。データ準備は、顧客データを統合して、集計／フィルタリングされた分析を提供するのに役立ちます。これには、レポート作成や顧客プロファイルの組み立て／データサイエンス／アクティベーションのためのデータ準備が含まれます。

| ブループリント | 説明 | Experience Cloud アプリケーション |
|---|---|---|
| **[データ準備と取り込み](ingestion.md)** | <ul><li>データ準備と取り込みブループリントは、データを準備して Adobe Experience Platform に取り込むためのすべての方法を網羅しています。</ul></li> | <ul><li> Adobe Experience Platform </ul></li> |
| **[サーバーサイドエンタープライズデータ収集](server-side-collection.md)** | <ul><li>既知のプロファイルベースの宛先（電子メールプロバイダー、ソーシャルネットワーク、広告など）に対してアクティブ化します。 </li><li>オンラインビヘイビアーと共に、オフライン属性およびイベント（オフラインの注文、トランザクション、CRM またはロイヤリティデータなど）を、オンラインターゲティングとパーソナライズ機能に使用します。</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager（オプション）</li></ul> |
