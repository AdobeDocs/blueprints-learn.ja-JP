---
title: Advertisingの宛先とファイルの宛先に対する B2B アカウントのアクティベーション
description: アカウントベースのエンゲージメントを使用して、オーディエンスを作成し、宛先を介してターゲットに設定します。
solution: Real-Time Customer Data Platform
source-git-commit: 074edca2f061459935d5f8b5e59e8cbd69b0fe4f
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 5%

---

# 広告の宛先とファイルの宛先に対する B2B アカウントのアクティベーション

アカウントベースのエンゲージメントにより、B2B マーケターは、アカウントのオーディエンス（会社のリスト）を作成し、ターゲティングやセールスアウトリーチのためにクラウドストレージの宛先への入力または書き出しとして会社のリストを受け入れるLinkedInのような宛先を介して、それらの会社をターゲットにすることができます。

## ユースケース

アカウントベースのエンゲージメントを使用すると、マーケターは次の 3 つの主要なユースケースを活用できます。

* **購入グループのギャップを埋める：** マーケターは、CMO または CIO の役割にまだ関する連絡先がないアカウントについて、広告を行うことができます。 最初に「CMO」や「CIO」という肩書を持つ担当者なしで、アカウントのオーディエンスを作成し、次にLinkedInでオーディエンスをアクティブ化できます。 その後、宛先のLinkedIn内で、「CMO」または「CIO」という役職のオーディエンスおよび特定の人物をターゲットにしたキャンペーンを開始し、これらの新しい連絡先にリーチして提供されるサービスのメリットを強調できます。
* **既存の顧客である会社の他の部門に対するアップセルまたはクロスセル：** マーケターは、製品 X を 3 ～ 9 か月前に購入したが、製品 Y をまだ所有していないアカウントオーディエンスを作成できます。その後、オーディエンスをアクティブ化して、そのターゲットオーディエンスに対する製品 Y のメリットを強調します。
* **競合する製品を使用している企業をターゲットにする：** マーケターは、競合他社の製品を置き換えるために、これらのアカウントに連絡先がない場合でも、アカウントにマーケティングを行うことができます。 競合他社の製品の所有権や使用状況を示すパートナーデータに基づいてアカウントのオーディエンスを作成し、LinkedInを通じてアクティブ化して、ターゲットアカウントの連絡先を追加できます。

## アプリケーション

* Real-time Customer Data Platform B2B エディション

## 統合パターン

* B2B データソース (Marketo、Salesforce など)-> Real-time Customer Data Platform B2B Edition -> 宛先。
* 様々な B2B データソースを使用して、アカウント、リード、オポチュニティおよび人物のデータをReal-time Customer Data Platformの B2B Edition にマッピングできます。

## アーキテクチャ

![B2B アカウントAudience Activationブループリントのリファレンスアーキテクチャ ](assets/b2b-blueprint-account-audience-activation.png)

## アカウントオーディエンスの宛先

* （会社）LinkedInでマッチしたオーディエンス
* クラウドストレージの宛先
   * Azure データレイク
   * データランディングゾーン
   * SFTP
   * Azure Blob
   * AWS S3

## ガードレール

* サンドボックスあたり 50 個のアカウントセグメントが上限です。
* バッチセグメント化の評価。
   * バッチオーディエンス実行ジョブとプロファイル書き出しジョブの完了後、評価は 24 時間ごとに自動的に行われます。
   * エッジ、ストリーミングまたはアドホック評価はサポートされていません。
* アカウント属性は書き出し可能です。
* 人々のイベント。
   * 最大 30 日間のイベントルックバック。イベントの述語の順序は指定されません。
   * AND/OR がサポートされています（つまり、「A と B が発生する必要があります」）。  しかし、「A は B の 3 日前に起こらなければならない」とは言えません）。
* クラウドストレージの宛先の場合、書き出しスケジュールでは、「セグメントの評価後」オプションがサポートされます。
* [B2B プロファイルおよびセグメント化ガードレール ](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails).

## Real-time Customer Data Platform B2B Edition、アカウントオーディエンスの作成およびアクティベーションの実装手順

* Real-time Customer Data Platform B2B Edition の実装手順については、[Real-time Customer Data Platform B2B Edition の概要 ](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial) ドキュメントを参照してください。
* アカウントオーディエンスの作成手順については、[ アカウントオーディエンス ](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/account-audiences) のドキュメントを参照してください。
* アカウントAudience Activationの手順については、[ アカウントオーディエンスのアクティブ化 ](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-account-audiences) ドキュメントを参照してください。
   * [ （会社）LinkedInでマッチしたオーディエンスの宛先 ](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-account-audiences#required-mappings) に必須のマッピング。

## 実装に関する考慮事項

LinkedInでマッチしたオーディエンスには、マッチしたメンバーの最小オーディエンスサイズ 300 人など、いくつかの要件があります。 会社のリンクされた一致したオーディエンスの宛先に対してアクティブ化されたアカウントオーディエンスが要件を満たさない場合は、LinkedIn キャンペーンを開始するためにオーディエンスのサイズを大きくするようにオーディエンス定義を変更する必要があります。

## 関連ドキュメント

* [Real-time Customer Data Platform B2B エディション](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [ アカウントオーディエンスの作成と有効化チュートリアルビデオ ](https://experienceleague.adobe.com/ja/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data)
* [ アカウントオーディエンスの作成 ](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/account-audiences)
* [ アカウントオーディエンスの有効化 ](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-account-audiences)
* [Adobe Experience Platform - LinkedIn宛先コネクタ ](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/social/linkedin)
