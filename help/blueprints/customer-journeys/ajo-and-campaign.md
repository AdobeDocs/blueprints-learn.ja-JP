---
title: Journey Optimizer と Adobe Campaign ブループリント
description: Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
source-git-commit: 6901596cbb661ffa8cf57c6ae958db1978bf1520
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 92%

---

# Journey Optimizer と Adobe Campaign

Adobe Journey Optimizer を Adobe Campaign と併用し、Campaign のリアルタイムメッセージングサーバーを利用してネイティブでメッセージを送信する方法を示します。

<br>

## アーキテクチャ

<img src="assets/ajo-campaign-architecture.svg" alt="参照アーキテクチャ Journey Optimizer ブループリント" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>Journey Optimizer と Campaign の両方を使用して、互いに独立してメッセージを送信することは可能ですが、技術的な考慮事項を熟慮する必要があります。このルートを進める場合は、Pre-Sales Enterprise Architect と協力し、実装をサポートするために必要な事項を理解する必要があります。

<br>

## 前提条件

### Adobe Experience Platform

* Journey Optimizer のデータソースを設定する前に、スキーマとデータセットをシステムに設定する必要があります。
* エクスペリエンスイベントクラスベースのスキーマの場合、ルールベースのイベントではないイベントをトリガーする場合に、を追加します エクスペリエンスイベントクラスベースのスキーマでは、ルールベースのイベントではないイベントをトリガーさせたい場合は「オーケストレーション eventID」フィールドグループを追加します。
* 個別のプロファイルクラスベースのスキーマの場合、「Profile test details」フィールドグループを追加して、Journey Optimizer で使用するテストプロファイルを読み込めるようにします
* Journey Optimizer と Campaign が同じ IMS 組織内でプロビジョニングされています

### Campaign v7/v8 または Campaign Standard

* リアルタイムメッセージングサービス (Message Center) の実行インスタンスは、アドビが管理する Cloud Services がホストする必要があります
* すべてのメッセージの作成は、Campaign インスタンス自体内でおこなわれます

<br>

## ガードレール

[Journey Optimizer ガードレール製品リンク](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ja)

### その他の Journey Optimizer ガードレール

* キャッピングは、宛先システムが障害点で飽和しないようにするために、今日では API を通じて利用できます。これは、キャップを超過したメッセージが完全にドロップされ、まったく送信されないことを意味します。スロットリングは、サポートされていません。
   * 最大接続数：宛先が処理できる http/s 接続の最大数
   * 最大呼び出し数：periodInMs パラメーターで行われる呼び出しの最大数
   * periodInMs：ミリ秒単位の時間
* セグメントメンバーシップで開始されるジャーニーは、2 つのモードで操作できます。
   * バッチセグメント（24 時間ごとに更新）
   * ストリーミングセグメント（5 分未満での認定）
* バッチセグメント - 認定ユーザーの毎日のボリュームを確実に把握し、宛先システムがジャーニーごと、およびすべてのジャーニーのバーストスループットを処理するために必要です
* ストリーミングセグメント - ジャーニーごと、およびすべてのジャーニーの毎日のストリーミング認定ボリュームと共に、プロファイル認定の最初のバーストを処理するために必要です
* 意思決定管理はサポートされていません
* ビジネスイベントはサポートされていません
* サードパーティシステムへのアウトバウンド統合
   * インフラはマルチテナントであるため、単一の静的 IP をサポートしていません（すべてのデータセンター IP を許可リストに含める必要があります）
   * カスタムアクションは POST メソッドと PUT メソッドのみ対応
   * 認証のサポート：トークン｜パスワード｜OAuth2
* Adobe Experience Platform や Journey Optimizer の個々のコンポーネントをパッケージ化して、様々なサンドボックス間で移動させることはできません。新しい環境に再実装する必要があります

<br>

### Campaign 統合

Adobe CampaignおよびAdobe Journey Optimizerの特定のバージョンとの統合に関するガイダンスについては、各Adobe Campaignバージョンに対応するガイドを参照してください。

* [Adobe Journey Optimizer &amp; Campaign v7](ajo-and-campaign-v7.md)
* [Adobe Journey Optimizer &amp; Campaign v8](ajo-and-campaign-v8.md)