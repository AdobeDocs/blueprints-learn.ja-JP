---
title: イベント転送
description: Edge Networkを通じて収集したリアルタイムのイベントデータを、分析、保存、広告のためにAdobe以外の宛先に転送する方法について説明します。
solution: Experience Platform
exl-id: 24964d27-db56-4fa4-a79f-1b6750564b34
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# イベント転送

このガイドでは、[!DNL Adobe Experience Platform] Edge Networkでのサーバーサイド処理を使用して、リアルタイムのイベントデータをAdobe以外の宛先（サードパーティのAnalytics プラットフォーム、クラウドストレージエンドポイント、広告ネットワーク、カスタム webhookなど）に配信するイベント転送ユースケースパターンについて説明します。 このパターンの仕組み、ビジネス目標、戦術的なユースケース、関連するAdobe アプリケーションについて理解する必要があるソリューションアーキテクト、マーケティングテクノロジスト、実装エンジニア向けに設計されています。

## ユースケースパターン

この節では、イベント転送の実装に使用されるパターンと実行プランについて説明します。

**イベント転送** — Edge Networkを介して収集したリアルタイムのイベントデータを、分析、保存、広告のためにAdobe以外の宛先に転送します。

**実行プラン：** データストリーム設定/ イベントルール定義/宛先マッピング / 転送実行> モニタリング

## ユースケースの概要

[!DNL Adobe Experience Platform] Web SDK、モバイル SDK、またはServer APIを通じて行動データを収集する企業は、多くの場合、[!DNL Google Analytics]や[!DNL Snowflake]などの分析プラットフォーム、コンバージョン トラッキング用の広告ネットワーク、長期保存のためのデータウェアハウス、カスタム内部サービスなど、Adobe以外のシステムと同じイベントストリームを共有する必要があります。 従来、この必要なクライアントサイドのタグの急増は、ページの重みを増やし、遅延を引き起こし、プライバシーとガバナンスのリスクを生じさせていました。

イベント転送は、Edge Networkでサーバーサイドを操作することで、これを解決します。 訪問者インタラクションがWeb SDKまたはServer APIを介してイベントをトリガーすると、そのイベントはデータストリームを介してEdge Networkにルーティングされます。 イベント転送ルール – 専用のイベント転送プロパティで設定 – 受信イベントデータを評価し、1つ以上の設定された宛先に選択的に転送します。 このサーバーサイドのアプローチにより、クライアント側のタグの肥大化を減らし、ページパフォーマンスを向上させ、データガバナンスを一元化し、Adobeのエコシステムに残るデータを正確に制御することができます。

このパターンのターゲットオーディエンスには、データ収集用の[!DNL Adobe Experience Platform] Web SDKまたはServer APIを既にデプロイした（またはデプロイする予定の）組織が含まれ、クライアントサイドのJavaScript タグを追加せずにAdobe以外のエンドポイントにイベントデータを配布することで、その投資を拡張する組織が含まれます。

## 主なビジネス目標

このユースケースパターンでは、次のビジネス目標をサポートしています。

### データ品質とガバナンスを改善する

クリーンで完全なコンプライアンスのデータを確保し、正確なターゲティング、無駄の削減、信頼性の高い分析を実現します。 イベント転送は、サーバー側でデータ配信を一元化し、外部システムと共有するデータの制御ポイントを組織に提供します。これにより、データ漏洩のリスクを軽減し、データが[!DNL Adobe] Edge Networkを離れる前にガバナンスポリシーが適用されます。

**KPI:**&#x200B;効率、コスト削減

詳しくは、[ データ品質とガバナンスの改善](../../business-objectives/cost-efficiency/improve-data-quality-governance.md)を参照してください。

### マーケティングテクノロジーの統合と近代化

統合されたスケーラブルなプラットフォームに移行することで、ツールの断片化と技術的負債を低減します。 イベント転送により、複数のクライアントサイドのベンダータグを単一のサーバーサイドのデータ配信メカニズムに置き換えることができるため、ページ読み込みのオーバーヘッドを減らし、テクノロジースタックを簡素化できます。

**KPI:** コスト削減、効率性、市場投入までの時間

詳しくは、[ マーケティングテクノロジーの統合と近代化](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)を参照してください。

## 戦術的なユースケース

このユースケースパターンが当てはまる一般的な戦術的シナリオは次のとおりです。

- **サードパーティの分析エンリッチメント** — クライアントサイドのタグを追加することなく、ページビュー、クリック、コンバージョンイベントを[!DNL Google Analytics]、[!DNL Snowflake]またはその他の分析プラットフォームにリアルタイムで転送します
- **Advertising コンバージョン トラッキング** — サーバーサイドのコンバージョンの測定と最適化のために、購入イベントとリードジェネレーションイベントを[!DNL Meta] コンバージョン API、[!DNL Google Ads]、[!DNL TikTok]または[!DNL Snap]に送信します
- **データウェアハウスのストリーミング** – 生のイベントデータをクラウドデータウェアハウス （[!DNL Google BigQuery]、[!DNL Amazon S3]、[!DNL Azure Event Hubs]）にルーティングして、長期的な保存とオフライン分析を行います
- **カスタム Webhook統合** — フィルタリングまたは変換されたイベントデータを、HTTP エンドポイントを介して内部マイクロサービス、CRM システム、またはパートナープラットフォームに転送します
- **タグの削減とページのパフォーマンス向上** – 複数のクライアントサイドベンダーのJavaScript タグを、単一のWeb SDK実装に加え、サーバーサイドイベント転送ルールに置き換えることで、ページの重みを軽減し、Core Web Vitalsを改善します
- **プライバシーに準拠したデータ共有** — イベントデータをサードパーティと共有する前に、データフィルタリングとフィールドレベルの墨消しルールをサーバーサイドで適用し、PIIが外部システムに到達する前に確実に削除またはハッシュ化されます
- **マルチクラウドイベント配信** – 単一のサーバーサイドのルールセットから、同じイベントストリームを複数の宛先（分析、広告、データウェアハウスなど）に同時に転送します
- **リアルタイムの不正信号の転送** – 価値の高いトランザクションイベントを不正検出システムに転送し、リアルタイムのリスクスコアリングとアラートを実現します

## 主要業績評価指標

次のKPIは、このユースケースパターンの成功を測定するのに役立ちます。

- **ページ読み込み時間の短縮** — クライアントサイドのタグをサーバーサイドのイベント転送に移行した後、ページの読み込み速度とCore Web Vitalsの改善を測定
- **データ配信の成功率** — エラーまたはタイムアウトなしで宛先エンドポイントに正常に転送されたイベントの割合
- **タグ数の削減** — サーバーサイドの同等な機能を実装した後に削除されたクライアントサイドのベンダータグの数
- **データの鮮度/待ち時間** — クライアントでのイベントの発生から宛先エンドポイントでのイベントの到着までの時間（目標：秒単位から秒単位）
- **ガバナンスコンプライアンス率** — サーバーサイドのフィルタリングルールを通過するアウトバウンドデータ共有の割合。PIIまたは制限されたデータが不正な宛先に到達しないようにします
- **運用効率** — クライアントサイドのタグのデプロイメントの管理とタグ競合のトラブルシューティングに費やす開発者時間の削減

## アプリケーション

このユースケースパターンでは、次のアプリケーションを使用します。

- **[!DNL Adobe Experience Platform]（Edge Network）** – 設定されたデータストリームを通じて、Web SDK、モバイル SDK、またはServer APIからリアルタイムのイベントデータを受け取り、ルーティングします
- **[!DNL Adobe Experience Platform]（イベント転送）** — イベントデータを評価、フィルタリング、変換、および外部宛先に転送するためのサーバーサイドのルールエンジンを提供します
- **[!DNL Adobe Experience Platform]（タグ / データ収集）** — イベント転送プロパティのライフサイクル、拡張機能、ルール、公開ワークフローを管理します

## 関連ドキュメント

次のリソースでは、このガイドで取り上げるトピックに関する追加の詳細を提供します。

**イベント転送**

- [イベント転送の概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [イベント転送の概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [イベント転送モニタリング](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [イベント転送シークレット](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

**イベント転送拡張機能**

- [サーバーサイド拡張機能カタログ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Adobe Cloud Connector拡張機能](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Meta Conversions API拡張機能](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Google Cloud Platform拡張機能](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [AWS拡張機能](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Snowflake拡張機能](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Google Ads Enhanced Conversions拡張機能](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Mailchimp拡張機能](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**データ収集とEdge Network**

- [データストリームの設定](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [データストリーム概要](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [Web SDKの概要](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Edge Network Server APIの概要](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [タグの概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
