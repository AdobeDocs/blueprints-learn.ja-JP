---
title: Advertisingの宛先とファイルの宛先に対するB2B アカウントのアクティベーション
description: アカウントベースのエンゲージメントを使用してオーディエンスを作成し、配信先を通じてターゲティングできます。
solution: Real-Time Customer Data Platform
exl-id: 578c0019-6133-4508-ae9d-8a8a463376f0
source-git-commit: b8b25146021472c6f513435df8e3be88254d9c3f
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 4%

---

# 広告宛先やファイル宛先へのB2B アカウントのアクティベーション

B2B マーケターは、アカウントベースドエンゲージメントにより、アカウントのオーディエンス（企業リスト）を作成し、LinkedInなどの配信先を通じてターゲティングできます。この配信先では、企業リストの入力やエクスポートをクラウドストレージの宛先に送信し、ターゲティングやセールス活動に活用できます。

## ユースケース

アカウントベースのエンゲージメントを利用することで、マーケターは次の3つの重要なユースケースを実現できます。

* **購買グループのギャップを埋める：** マーケターは、CMOまたはCIOの役割の連絡先がまだ決まっていないアカウントに広告を表示できます。 「CMO」や「CIO」という肩書きを持たずにアカウントのオーディエンスを構築し、そのオーディエンスをLinkedInで活用することができます。 LinkedInでは、新しい連絡先にリーチし、そのサービスのメリットを強調するために、「CMO」または「CIO」の役職を持つオーディエンスや特定の個人をターゲットにしたキャンペーンを展開することができます。
* **既存顧客である会社の他の部門へのアップセルまたはクロスセル：** マーケターは、製品Xを3 ～ 9か月前に購入したが、製品Yを所有していないアカウントオーディエンスを作成できます。営業担当者は、ターゲットオーディエンスに対する製品Yのメリットを強調しながら、アクティブ化することができます。
* **競合製品を使用している企業をターゲットにする：** マーケターは、アカウントに連絡先がなくても、競合他社の製品を置き換えるためにアカウントにマーケティングをおこなうことができます。 競合他社製品の所有権や利用状況を示すパートナーデータにもとづいてアカウントのオーディエンスを作成し、LinkedInを通じてアクティベートして、ターゲットアカウントの連絡先を獲得し、拡張することができます。

## アプリケーション

* Real-time Customer Data Platform B2B エディション

## 統合パターン

* B2B データソース（Marketo、Salesforceなど） -> Real-time Customer Data Platform B2B edition -> Destinations.
* さまざまなB2B データソースを使用して、アカウント、リード、商談、人物データをAdobe Real-Time CDPのB2B editionにマッピングできます。

## アーキテクチャ

![B2B アカウント Audience Activation ブループリントの参照アーキテクチャ &#x200B;](assets/b2b-blueprint-account-audience-activation.png)

## アカウントオーディエンスの宛先

* （企業） LinkedIn Matched Audiences
* クラウドストレージの宛先
   * Azure Data Lake
   * データランディングゾーン
   * SFTP
   * Azure・ブロブ
   * AWS S3

## ガードレール

* 1 サンドボックスにつき50 アカウントセグメントを上限とします。
* バッチセグメント化の評価：
   * バッチオーディエンスの実行とプロファイルの書き出しジョブの完了後、24時間ごとに自動的に評価されます。
   * エッジ、ストリーミング、アドホックの評価はサポートしていません。
* アカウント属性は書き出しに使用できます。
* 人のイベント。
   * 最大30日間のイベントルックバック、イベント述語の順序なし。
   * AND / ORはサポートされています（そのため、「AとBは発生する必要があります」と言えますが、「AはBの3日前に発生する必要があります」とは言えません）。
* クラウドストレージの宛先の場合、書き出しスケジュールは「セグメント評価後」オプションをサポートしています。
* [B2B プロファイルとセグメント化ガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)。

## Adobe Real-Time CDP B2B edition、アカウントオーディエンスの構築、アクティベーションの導入手順

* Real-time Customer Data Platform B2B editionの実装手順については、[Real-Time Customer Data Platform B2B Editionの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial) ドキュメントを参照してください。
* アカウントオーディエンスの作成手順については、[&#x200B; アカウントオーディエンス &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences)のドキュメントを参照してください。
* アカウント Audience Activationの手順については、[&#x200B; アカウントオーディエンスの有効化](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences)のドキュメントを参照してください。
   * [&#x200B; （企業） LinkedIn Matched Audiencesの宛先](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences#required-mappings)に必要なマッピング。

## 実装に関する考慮事項

LinkedInに一致するオーディエンスには、300人の一致したメンバーの最小オーディエンスサイズなど、いくつかの要件があります。 会社のリンクされたマッチング済みオーディエンス宛先に対してアクティブ化されたアカウントオーディエンスが要件を満たさない場合は、LinkedIn キャンペーンを起動するためにオーディエンスのサイズを増やすようにオーディエンス定義を変更する必要があります。

## 関連ドキュメント

* [B2B オーディエンスとプロファイル アクティベーションの設計図](b2bactivation.md) – 個人レベルとアカウント レベルの両方のB2B アクティベーションをカバーする親の設計図。
* [Adobe Real-Time CDPのB2B editionは](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [アカウントオーディエンスの作成とアクティブ化のチュートリアルビデオ](https://experienceleague.adobe.com/ja/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data)
* [アカウントオーディエンスの構築](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences)
* [アカウントオーディエンスのアクティベーション](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences)
* [Adobe Experience Platform - LinkedIn Destination Connector](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
