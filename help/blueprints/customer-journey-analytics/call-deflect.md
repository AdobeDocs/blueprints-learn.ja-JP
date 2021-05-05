---
title: 呼び出し偏向分析ブループリント
description: コールセンターに問い合わせる前の顧客行動を分析します。
solution: Experience Platform, Customer Journey Analytics
kt: 7209
exl-id: 13593c1c-4c58-4b8a-aa6c-7530fd679a14
translation-type: tm+mt
source-git-commit: 6365fa00a77ba22774b2d6de3e882a3e09dcae0f
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 92%

---

# 呼び出し偏向ジャーニー分析ブループリント

コールセンターに問い合わせる前の顧客の行動をデスクトップとモバイルをまたいで分析します。カスタマーサポートに問い合わせる前に顧客が取った行動、表示したコンテンツ、検索したフレーズを把握することで、カスタマージャーニーを向上させる機会を特定します。顧客が電話することなく問題を解決できるように、改善できるコンテンツおよびセルフサービスツールを判別します。

## ユースケース

* 顧客がサポートに問い合わせる前の顧客行動を分析
* セルフサービス機能を改善する機会を見つける

## アプリケーション

* Adobe Experience Platform
* Customer Journey Analytics

## 統合パターン

* Adobe Experience Platform → Customer Journey Analytics

## 構造

<img src="assets/CJA.svg" alt="Customer Journey Analytics ブループリントの参照アーキテクチャ" style="border:1px solid #4a4a4a" />

## 実装手順

1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) スキーマを作成します。
1. [取り込むデータの](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) データセットを作成します。
1. [データをプラットフォームに取り込みます](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)。データは、Customer Journey Analytics に取り込まれる前に、Platform に取り込まれる必要があります。
1. クロスチャネルイベントデータセットを分析します。
結合で分析されたデータセットは、共通の名前空間 ID を持つか、Customer Journey Analytics のフィールドベースのステッチ機能でキー更新されている必要があります。 

   >[!NOTE]
   >
   >Customer Journey Analytics は、現在、Experience Platform プロファイルや ID サービスをステッチに使用していません。

1. 時系列のデータセットをまたいで共通キーを Customer Journey Analytics に取り込むために、カスタムデータ準備を実行するか、データに対するフィールドベースの ID ステッチを使用します。
1. イベントデータのフィールドに結合できる、ルックアップデータ用のプライマリ ID を提供します。ライセンスの行としてカウントされます。
1. イベントデータのプライマリ ID と同じプライマリ ID をプロファイルデータに設定します。
1. Experience Platform から Customer Journey Analytics への取り込みデータに対するデータ接続を設定します。データがデータレイクに入ったら、90 分以内に Customer Journey Analytics で処理されます。
1. 接続のデータビューを設定して、ビューに含める特定のディメンションおよび指標を選択します。また、属性および配分設定も、データビューで設定されます。これらの設定は、レポート時に計算されます。
1. Analysis Workspace 内でダッシュボードおよびレポートを設定するためのプロジェクトを作成します。

## 実装のための考慮事項

### ID ステッチの考慮事項

* 結合される時系列データは、レコードごとに同じ ID 名前空間を持っている必要があります。コールセンターデータを匿名デバイスデータに接続するには、デジタル ID が呼び出し ID に結びつけられている必要があります。この結びつきは、以下のようなメカニズムで発生します。
   * 関係をトラッキングするためのルックアップテーブルと共に、ダイヤル番号が、その時間、その訪問者の一意のダイヤル番号である。
   * サポートをリクエストする前にユーザーを認証する必要があり、この認証をコールセンター担当者が決定する識別子（例えば、電話番号や電子メール）に結びつける。
   * オンボーディングパートナーを使用して、サポートリクエストに結びつけられる既知の識別子と共にオンラインデバイス識別子を入力する。
* 異なるデータセットを統合する結合プロセスでは、データセット間で共通のプライマリユーザー／エンティティキーが必要です。
* セカンダリキーベースの結合は、現在、サポートされていません。
* フィールドベースの ID ステッチプロセスを使用すると、以降の一時的な ID レコード（認証 ID など）に基づいて、行の ID をキー更新できます。このプロセスを使用すると、デバイスまたは cookie レベルではなくユーザーレベルで分析するために、異なるレコードを単一の ID に解決できます。
* ステッチは 1 週間に 1 回行われ、ステッチの後に繰り返されます。

## よくある質問

* Customer Journey Analytics のデータモデルは、ダウンストリームにどのような影響がありますか？

   同じ XDM フィールドのオブジェクトおよび属性は、Customer Journey Analytics の 1 つのディメンションに結合されます。様々なデータセットから同じ CJA ディメンションに複数の属性を結合するために、データセットは、同じ XDM フィールドまたはスキーマを参照している必要があります。

## 関連ドキュメント

* [Customer Journey Analytics 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics ドキュメント](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=ja)
* [Customer Journey Analytics チュートリアル](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html?lang=ja)
