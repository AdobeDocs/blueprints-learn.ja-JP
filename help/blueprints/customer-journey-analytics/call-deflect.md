---
title: 呼び出し偏向分析シナリオ
description: コールセンターに連絡する前に、顧客の行動を分析します。
solution: Experience Platform, Customer Journey Analytics
kt: 7209
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---


# 呼び出し偏向ジャーニー分析のシナリオ

コールセンターに連絡する前に、デスクトップとモバイルでの顧客の行動を分析します。 顧客が行おうとしている行動、表示したコンテンツ、カスタマーサポートに連絡する前に検索した用語を把握することで、顧客のジャーニーを改善する機会を特定します。 顧客が電話をかけなくても問題を解決できるように改善できるコンテンツおよびセルフサービスツールを決定します。

## 使用例

* 顧客がサポートに連絡する前に顧客行動を分析する
* セルフサービス機能を改善する機会を見つけ出す

## アプリ

* Adobe Experience Platform
* Customer Journey Analytics

## 統合パターン

* Adobe Experience Platform→Customer Journey Analytics

## 建築

<img src="assets/CJA.svg" alt="Customer Journey Analyticsのブループリントのリファレンスアーキテクチャ" style="border:1px solid #4a4a4a" />

## ガードレール

Customer Journey Analyticsへのデータ取り込み：

* 湖へのデータ取り込み：API ～ 7 GB/時、ソースコネクタ～ 200 GB/時、15分間のレークにストリーミング、Analyticsソースコネクタ～ 45分のレークにストリーミング。
* データがデータレークに発行された後、Customer Journey Analyticsが処理されるまでに最大90分かかる場合があります。

## 導入手順

1. データセットとスキーマを設定します。
1. データをプラットフォームに取り込みます。
データは、Customer Journey Analyticsに取り込む前にプラットフォームに取り込む必要があります。
1. チャネル間のイベントデータセットを分析します。
和集合で分析されるデータセットは、共通の名前空間IDを持つか、Customer Journey Analyticsのフィールドベースのステッチ機能を使用して再キー設定する必要があります。 

   >[!NOTE]
   >
   >Customer Journey Analyticsは現在、ステッチにExperience PlatformプロファイルまたはIDサービスを使用していません。

1. データに対するフィールドベースのIDステッチのカスタムデータ準備または使用を実行し、時系列データセット間の共通キーをCustomer Journey Analyticsに取り込むようにします。
1. 参照データのプライマリIDを指定します。このIDをイベントデータ内のフィールドに結合できます。 ライセンスの行としてカウントします。
1. プロファイルデータには、イベントデータのプライマリIDと同じプライマリIDを設定します。
1. データをExperience PlatformからCustomer Journey Analyticsに取り込むためのデータ接続を設定します。 データがデータレークに到着した後、90分以内にCustomer Journey Analyticsに処理されます。
1. 表示に含める特定のディメンションおよび指標を選択するには、接続でデータ表示を設定します。 アトリビューションと配分の設定は、データ表示でも設定されます。 これらの設定は、レポート時に計算されます。
1. プロジェクトを作成して、Analysis Workspace内でダッシュボードとレポートを設定します。

## 実装に関する考慮事項

### IDのステッチの考慮事項

* 結合する時系列データは、すべてのレコードで同じID名前空間を持つ必要があります。 コールセンターデータを匿名デバイスデータに接続するには、デジタルIDを呼び出し元IDに関連付ける必要があります。 この結び付きは、次のいくつかの考えられるメカニズムを通して発生します。
   * ダイヤル番号は、その時点でのその訪問者の一意のダイヤル番号で、関係を追跡するための参照テーブルと共に使用されます。
   * サポートをリクエストする前にユーザーの認証を要求し、この認証をコールエージェントが決定する識別子（電話番号、電子メールなど）に関連付けます。
   * オンボーディングパートナーを使用して、サポート要求に関連付けられた既知の識別子を持つオンラインデバイス識別子を入力します。
* 個別のデータセットを統合する和集合プロセスでは、データセット全体で共通の主要な人/エンティティキーが必要です。
* 現在、セカンダリキーベースの和集合はサポートされていません。
* フィールドベースのIDの切り替えプロセスでは、認証IDなど、後続の一時的なIDレコードに基づいて、行のIDを再入力できます。 このプロセスにより、個別のレコードを、デバイスやcookieレベルではなく、個人レベルでの分析用に1つのIDに解決できます。
* ステッチは週に1回行われ、ステッチの後に再生が行われます。

## FAQ

* Customer Journey Analyticsにおけるデータモデルのダウンストリームの影響は何ですか。

   同じXDMフィールドのオブジェクトと属性は、Customer Journey Analytics内の1つのディメンションに結合されます。 様々なデータセットの複数の属性を同じCJAディメンションにマージするには、データセットは同じXDMフィールドまたはスキーマを参照する必要があります。

## 関連ドキュメント

* [Customer Journey Analytics製品の説明](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analyticsドキュメント](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Customer Journey Analyticsチュートリアル](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
