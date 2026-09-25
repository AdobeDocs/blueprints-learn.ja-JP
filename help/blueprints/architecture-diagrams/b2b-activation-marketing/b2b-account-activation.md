---
title: Advertisingおよびファイル宛先へのB2B アカウントアクティベーション
description: アカウントベースのエンゲージメントを使用してアカウントオーディエンスを作成し、広告配信先やクラウドストレージにアクティベートできます。
solution: Real-Time Customer Data Platform
exl-id: 578c0019-6133-4508-ae9d-8a8a463376f0
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%
---

# 広告宛先やファイル宛先へのB2B アカウントのアクティベーション

B2B マーケターは、アカウントベースのエンゲージメントにより、**Real-Time Customer Data Platform B2B edition**&#x200B;のアカウントのオーディエンス（企業一覧）を作成し、それらのアカウントオーディエンスをLinkedIn Matched Audiences、Bombora、Demandbaseなどの広告配信先やクラウドストレージの配信先にアクティベートできます。 こうしたアカウントオーディエンスは、ターゲティング、セールスアウトリーチ、ダウンストリームの分析に活用できます。

## ユースケース

アカウントベースのエンゲージメントを利用することで、マーケターは次の3つの重要なユースケースを実現できます。

- **購買グループのギャップを埋める：** マーケターは、CMOまたはCIOの役割の連絡先がまだ決まっていないアカウントに広告を表示できます。 「CMO」または「CIO」というタイトルを持たずにアカウントのオーディエンスを構築し、LinkedIn Matched Audiencesまたはその他のサポートされている広告配信先でオーディエンスをアクティブ化することができます。 そして、宛先内で、「CMO」または「CIO」の役職を持つオーディエンスや特定の人々をターゲットにしたキャンペーンを開始して、これらの新しい連絡先にリーチし、そのサービスのメリットを強調することができます。
- **既存顧客である会社の他の部門へのアップセルまたはクロスセル：** マーケターは、製品Xを3 ～ 9か月前に購入したが、製品Yを所有していないアカウントオーディエンスを作成できます。営業部門とマーケティング部門の連携を促進するために、LinkedIn Matched Audiences、その他の広告プラットフォーム、クラウドストレージの書き出しを通じて、製品Yをそのターゲットオーディエンスに配信する利点を強調しながら、このアカウントオーディエンスをアクティベートできます。
- **競合製品を使用している企業をターゲットにする：** マーケターは、アカウントに連絡先がなくても、競合他社の製品を置き換えるためにアカウントにマーケティングをおこなうことができます。 競合他社製品の所有権や使用状況を示すパートナーまたはインテントのデータにもとづいてアカウントオーディエンスを作成し、LinkedIn Matched Audiencesなどのサポートされている広告配信先を通じてアクティベートして、ターゲットアカウントのオーディエンスを獲得し、拡張することができます。

## アプリケーション

- Real-Time Customer Data Platform B2B edition
- （オプション）Customer Journey Analytics B2B edition

## 統合パターン

このブループリントの一般的な統合パターンは次のとおりです。

- **B2B エンゲージメントとCRM ソース → RTCDP B2B edition → アカウントオーディエンス→宛先**

  B2B エンゲージメントおよびCRM システム（Marketo Engage、Salesforce、Microsoft Dynamicsなど）は、標準のB2B スキーマとリレーションシップを使用して、リード/コンタクト、アカウント、商談を&#x200B;**Real-Time CDP B2B edition**&#x200B;に送信します。 アカウントオーディエンスは、統合されたB2B データモデルの上に構築され、広告やファイルの宛先に対してアクティブ化されます。

- **B2B インテントおよびイベントソース → RTCDP B2B edition → アカウントオーディエンス→宛先**

  B2Bのインテントおよびイベントソース（Bombora IntentやDemandbase Intentなど）は、Experience Platformにインテントおよびエンゲージメントイベントを送信します。 これらのデータセットは、標準的なB2B スキーマにマッピングされているため、マーケターはアカウントオーディエンス（競合他社のトピックで急増するアカウントなど）を構築し、広告やクラウドストレージの宛先に活用できます。 次に、アカウントオーディエンスを、BomboraやDemandbaseなどの広告パートナー（サポートされている場合）にアクティベートできます。

## アーキテクチャ

![B2B Account Activation ブループリントの参照アーキテクチャ ](assets/b2b-account-activation.png){width="1000" zoomable="yes"}

## アカウントオーディエンスの宛先

- **LinkedIn Matched Audiences**
- **ボンボラ**
- **Demandbase**
- **クラウドストレージの宛先**
  - Azure Data Lake Storage Gen2
  - データランディングゾーン
  - SFTP
  - Azure・ブロブ
  - AWS S3

アカウントオーディエンスをサポートする宛先の最新のリストについては、宛先ドキュメントを参照してください。

## ガードレール

アカウントオーディエンスの設計とアクティブ化については、次のガードレールを参照してください。

- [Real-Time Customer Data Platform B2B editionのガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [アカウントオーディエンス](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [アカウントオーディエンスのアクティベーション](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [プロファイルとセグメント化のガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ストリーミングセグメント化の適格基準の更新](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/eligibility-criteria-update)

## Real-Time Customer Data Platform B2B edition、アカウントオーディエンスの構築およびアクティベーションの実装ステップ

- Real-Time Customer Data Platform B2B editionの実装手順については、次のドキュメントを参照してください。[Real-Time Customer Data Platform B2B editionの概要](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en)。
- アカウントオーディエンスの作成手順については、[ アカウントオーディエンス ](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en)のドキュメントを参照してください。
- アカウントオーディエンスのアクティベーション手順については、[ アカウントオーディエンスのアクティベーション ](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)のドキュメントを参照してください。

  - [LinkedIn Matched Audiences destination](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en#required-mappings)に必要なマッピング。

## 実装に関する考慮事項

LinkedIn Matched Audiencesには、オーディエンスサイズの最小要件（300件のマッチング済みメンバーなど）があります。 LinkedIn Matched Audiencesに対してアクティブ化されたアカウントオーディエンスがこの要件を満たさない場合は、キャンペーンを開始する前に、オーディエンス定義を拡張して一致するオーディエンスサイズを増やす必要がある場合があります。

## 関連ドキュメント

- [B2B オーディエンスとプロファイル アクティベーションの設計図](b2b-audience-profile-activation.md) – 個人レベルとアカウント レベルの両方のB2B アクティベーションをカバーする親の設計図。
- [Real-Time Customer Data PlatformのB2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview?lang=en)
- [アカウントオーディエンスの作成とアクティブ化 – チュートリアルビデオ](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data?lang=en)
- [アカウントオーディエンスの構築](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [アカウントオーディエンスのアクティベーション](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [Adobe Experience Platform - LinkedIn Destination Connector](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin?lang=en)
- [Real-Time CDP B2B editionのスキーマ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Real-Time CDP B2B editionへのアーキテクチャのアップグレード](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [宛先ガードレール](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
