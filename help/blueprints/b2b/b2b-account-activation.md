---
title: Advertisingの宛先とファイルの宛先に対する B2B アカウントのアクティベーション
description: アカウントベースのエンゲージメントを使用して、オーディエンスを作成し、宛先を介してターゲットに設定します。
solution: Real-Time Customer Data Platform
exl-id: 578c0019-6133-4508-ae9d-8a8a463376f0
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 4%

---

# 広告の宛先とファイルの宛先に対する B2B アカウントのアクティベーション

アカウントベースのエンゲージメントにより、B2B マーケターは、アカウントのオーディエンス（会社のリスト）を作成し、LinkedIn のような、ターゲティングやセールスアウトリーチのためにクラウドストレージの宛先への入力または書き出しとして会社のリストを受け入れる宛先を介して、それらの会社をターゲットにすることができます。

## ユースケース

アカウントベースのエンゲージメントを使用すると、マーケターは次の 3 つの主要なユースケースを活用できます。

* **購入グループのギャップを埋める：** マーケターは、CMO または CIO の役割にまだ関する連絡先がないアカウントについて、広告を行うことができます。 最初に、「CMO」または「CIO」というタイトルの担当者なしで、アカウントのオーディエンスを作成し、次に LinkedIn でオーディエンスをアクティブ化できます。 LinkedIn は対象先に入り、「CMO」または「CIO」という役職のオーディエンスおよび特定の人物をターゲットにしたキャンペーンを開始し、これらの新しい連絡先にリーチして提供されるサービスのメリットを示すことができます。
* **既存の顧客である会社の他の部門に対するアップセルまたはクロスセル：** マーケターは、製品 X を 3 ～ 9 か月前に購入したが、製品 Y をまだ所有していないアカウントオーディエンスを作成できます。その後、オーディエンスをアクティブ化して、そのターゲットオーディエンスに対する製品 Y のメリットを強調します。
* **競合する製品を使用している企業をターゲットにする：** マーケターは、競合他社の製品を置き換えるために、これらのアカウントに連絡先がない場合でも、アカウントにマーケティングを行うことができます。 競合他社の製品の所有権や使用状況を示すパートナーデータに基づいてアカウントのオーディエンスを作成し、LinkedIn を通じてアクティブ化して、ターゲットアカウントのソース連絡先で拡張を行うことができます。

## アプリケーション

* Real-time Customer Data Platform B2B エディション

## 統合パターン

* B2B データソース（Marketo、Salesforceなど） -> Real-time Customer Data Platform B2B edition -> 宛先。
* 様々な B2B データソースを使用して、アカウント、リード、オポチュニティおよび人物のデータを Real-time Customer Data Platform のB2B editionにマッピングできます。

## アーキテクチャ

![B2B アカウントAudience Activation ブループリントのリファレンスアーキテクチャ &#x200B;](assets/b2b-blueprint-account-audience-activation.png)

## アカウントオーディエンスの宛先

* （会社）リンクインされたマッチしたオーディエンス
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
* [B2B プロファイルおよびセグメント化ガードレール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails).

## Real-time Customer Data Platform B2B edition、アカウントオーディエンスの作成、アクティベーションの実装手順

* Real-time Customer Data Platform B2B editionの実装手順については、[Real-Time Customer Data Platform B2B Editiond の使用の手引き &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial) ドキュメントを参照してください。
* アカウントオーディエンスの作成手順については、[&#x200B; アカウントオーディエンス &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/account-audiences) のドキュメントを参照してください。
* アカウントのAudience Activation手順については、[&#x200B; アカウントオーディエンスのアクティブ化 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-account-audiences) ドキュメントを参照してください。
   * [&#x200B; （会社） LinkedIn でマッチしたオーディエンスの宛先 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-account-audiences#required-mappings) に必須のマッピング。

## 実装に関する考慮事項

LinkedIn でマッチしたオーディエンスには、マッチしたメンバーの最小オーディエンスサイズ 300 人など、いくつかの要件があります。 会社のリンクされた一致したオーディエンスの宛先に対してアクティブ化されたアカウントオーディエンスが要件を満たさない場合は、LinkedIn キャンペーンを開始するオーディエンスサイズを増やすようにオーディエンス定義を変更する必要があります。

## 関連ドキュメント

* [Real-time Customer Data Platform のB2B edition](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [アカウントオーディエンスの作成と有効化チュートリアルビデオ](https://experienceleague.adobe.com/ja/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data)
* [アカウントオーディエンスの作成](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/account-audiences)
* [アカウントオーディエンスの有効化](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-account-audiences)
* [Adobe Experience Platform - LinkedIn 宛先コネクタ](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/social/linkedin)
