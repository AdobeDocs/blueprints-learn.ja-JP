---
title: Digital Behavioral Data Consolidation Blueprint
description: カスタマージャーニーをまたいで顧客インタラクションからのインサイトを分析および抽出します。
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
exl-id: b042909c-d323-40d5-8b35-f3e5e3e26694
translation-type: tm+mt
source-git-commit: 844fff1cefe367575beb5c03aa0f0d026eb9f39b
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 2%

---

# Digital Behavioral Data Consolidation Blueprint

様々なWeb、モバイル、オフラインのプロパティからデータを統合することにより、様々なチャネルにわたる顧客の行動を1つの統合表示にします。

## 使用例

* デスクトップとモバイルで顧客のインタラクションを分析し、顧客の行動を把握し、インサイトを抽出してデジタル顧客体験を最適化します。
* サポートインタラクションや店頭購入など、デジタルやオフラインのチャネルを含むチャネル間での顧客のインタラクションを分析し、顧客のジャーニーをより深く理解し最適化する。 

## アプリ

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics（オプション）

## 統合パターン

* Adobe Experience Platform→Customer Journey Analytics
* Adobe Analytics→Adobe Experience Platform→Customer Journey Analytics

## 建築

<img src="assets/CJA.svg" alt="Customer Journey Analyticsのブループリントのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

Customer Journey Analyticsへのデータ取り込み：

* 湖へのデータ取り込み：API ～ 7 GB/時、ソースコネクタ～ 200 GB/時、レークへ15分、Adobe Analyticsソースコネクタ～ 45分
* データがデータレークに発行された後、Customer Journey Analyticsが処理されるまでに最大90分かかる場合があります。

## 導入手順

1. データセットとスキーマを設定します。
1. データをプラットフォームに取り込みます。
データは、Customer Journey Analyticsに処理する前にプラットフォームに取り込む必要があります。
1. チャネル間のイベントデータセットを分析し、和集合で分析対象の名前空間IDが共通であるか、Customer Journey Analyticsのフィールドベースのステッチ機能を使用して再キーされているかを確認します。 

   >[!NOTE]
   >
   >Customer Journey Analyticsは現在、ステッチにExperience PlatformプロファイルまたはIDサービスを使用していません。

1. データに対するフィールドベースのIDステッチのカスタムデータ準備または使用を実行し、時系列データセット間の共通キーをCustomer Journey Analyticsに取り込むようにします。
1. 参照データに、イベントデータのフィールドに結合できるプライマリIDを指定します。 ライセンスの行としてカウントします。
1. プロファイルデータには、イベントデータのプライマリIDと同じプライマリIDを設定します。
1. データをExperience PlatformからCustomer Journey Analyticsに取り込むためのデータ接続を設定します。 データがデータレークに到着した後、90分以内にCustomer Journey Analyticsに処理されます。
1. 表示に含める特定のディメンションおよび指標を選択するには、接続でデータ表示を設定します。 アトリビューションと配分の設定は、データ表示でも設定されます。 これらの設定は、レポート時に計算されます。
1. プロジェクトを作成して、Analysis Workspace内でダッシュボードとレポートを設定します。

## 実装に関する考慮事項

### IDのステッチの考慮事項

* 結合する時系列データは、すべてのレコードで同じID名前空間を持つ必要があります。
* 個別のデータセットを統合する和集合プロセスでは、データセット全体で共通の主要な人/エンティティキーが必要です。
* 現在、セカンダリキーベースの和集合はサポートされていません。
* フィールドベースのIDの切り替えプロセスでは、認証IDなど、後続の一時的なIDレコードに基づいて、行のIDを再入力できます。 これにより、個別のレコードを、デバイスやcookieレベルではなく、個人レベルでの分析用に単一のIDに解決できます。
* ステッチは週に1回行われ、ステッチの後に再生が行われます。

## FAQ

* Customer Journey Analyticsにおけるデータモデルのダウンストリームの影響は何ですか。

   同じXDMフィールドのオブジェクトと属性は、Customer Journey Analytics内の1つのディメンションに結合されます。 宛先  様々なデータセットの複数の属性を同じCustomer Journey Analyticsディメンションにマージする場合、データセットは同じXDMフィールドまたはスキーマを参照する必要があります。

## 関連ドキュメント

* [Customer Journey Analytics製品の説明](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analyticsドキュメント](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Customer Journey Analyticsチュートリアル](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
