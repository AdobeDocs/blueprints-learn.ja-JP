---
title: Marketo データブループリントを使用した B2Bジャーニー
description: Marketo Engage Data を使用したJourney Optimizer B2B editionの迅速なデプロイメントのブループリント。
solution: Journey Optimizer B2B Edition
exl-id: d7bd0bd3-0f61-4e59-855f-27afc147c9aa
source-git-commit: cf5cc31e3ef96c2bf1748cb8d1afacdc2f45c156
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 3%

---

# Marketo データブループリントを使用した B2Bジャーニー

この包括的なガイドでは、Marketo EngageとAdobe Journey Optimizer B2B editionの統合プロセスについて説明します。 カスタムスキーマの設定、プロファイルとアカウントの取り込み、購入グループ向けにパーソナライズされたジャーニーのオーケストレーションについて説明します。 このブループリントはMarketo Engage データを使用することで、複数のチャネルにわたる正確なターゲティングとエンゲージメントを保証し、より適格性の高い需要を促し、カスタマーエクスペリエンス（顧客体験）を強化します。

## ユースケース

* **購入グループの作成と管理**：生成 AI を使用して、ターゲットアカウント内の購入グループを組み立てて管理し、主要な関係者を包括的にカバーします
* **メンバーの自動割り当て**：定義された基準（コンテンツ消費や CRM データなど）に基づいて、メンバーを購買グループの役割に自動的に割り当てます
* **ジャーニーのパーソナライズ**：役割、アカウント、商品の興味、ライフサイクルステージに基づいて、各購入グループとメンバーに合わせてカスタマイズされた複数手順のジャーニーを設計および視覚化します
* **リアルタイム自動化**：リアルタイムエンゲージメントトリガーと選定スコアリングを使用して、ジャーニーを通じてアカウントと購入グループの進行を自動化します
* **Cross-Channel Engagement**: メール、SMS、広告、チャット、イベント、ウェビナーなど、複数のチャネルをまたいで購入グループを参加させ、需要の創出と選定を合理化します
* **AI 駆動型インサイト**:AI 駆動型インサイトを使用して、個々の購入者と購入グループ全体のコンテンツ配信とエンゲージメント戦略を最適化します
* **統合データアクティベーション**:Adobe Real-Time Customer Data Platformの統合アカウントリストをアクティブ化して、購入グループの作成と管理のための最新かつ完全なデータを提供します
* **Collaborationの強化機能**：マーケティングと販売の取り組みを調整して、より正確な販売チャンスを生み出し、パイプラインの作成を迅速化します

## アプリケーション

* Journey Optimizer B2B Edition
* Real-time Customer Data Platform B2B エディション
* Marketo Engage

## 統合パターン

| 統合 | 説明 |
| :-- | :--- |
| [Marketo Engage コネクタ ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) | Adobe Experience Platformは、Marketoからのデータの取り込みを容易にし、そのサービスを使用してデータの構造化、ラベル付け、拡張を行う機能を提供します。 |
| [Journey Optimizer B2B edition - Marketo Engageのアクション ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes/action-nodes#marketo-engage-actions) | 人物ベースのアクションを使用してリストのメンバーシップ、人物のパーティション、リクエストキャンペーンを管理することで、Journey Optimizer B2B editionのAccount-Based MarketingをMarketo Engageのリードベースの取り組みと同期させます。 |
| [Journey Optimizer B2B edition - Marketo Engage assets](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content-management/assets/marketo-engage-dam/marketo-engage-design-studio) | Marketo Engage Design Studio は、Journey Optimizer B2B editionのデフォルトのアセットソースで、アカウントジャーニーのアセット管理を容易にします。 |

## アーキテクチャ

![Marketoのみのデータを含むAJO B2B のソリューションアーキテクチャ ](./assets/ajo-b2b-marketo-only.png){zoomable="yes"}

## 実装手順

* 以下のいずれかのオプションを使用して、B2B スキーマと名前空間をインストールします
   * [Postman コレクション ](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) の使用
   * Platform UI での [ テンプレート ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/ui-tutorials/templates) の使用
* Marketo フィールドとExperience Platform XDM スキーマ間のマッピングを定義するデータディクショナリを作成します
   * [Marketo オブジェクトメタデータ ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/export-all-object-metadata) を開始点として使用
   * [XDM スキーマをカスタマイズ ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/overview) して、カスタムフィールドを含める
   * Journey Optimizer B2B editionでサポートされている標準 [XDM フィールド ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/accounts/field-mapping) を確認します。 追加のフィールドが必要な場合は、サポートチケットを開いて設定してください
      * **workEmail.address** は人物データセットに必須です
      * **accountName** はアカウント データ セットに必要です
   * 書き出されたMarketo メタデータのスプレッドシートに新しい XDM フィールド列を追加し、目的のマッピングを記録します
* [Marketo Engage ソースコネクタを設定 ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
   * 上記で定義したデータディクショナリを使用して、ソースコネクタの [ マッピングをインポート ](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/ui/mapping#import-mapping) を定義します
   * [ 実装に関する考慮事項 ](#implementation-considerations) を考慮に入れる前に、プロファイルを有効にしないことをお勧めします
   * アカウントオーディエンスを作成する際には、これらのオブジェクトが最も役に立つので、少なくとも人物、会社、機会およびアクティビティを取り込むことをお勧めします
* 人物に対して [ID グラフリンクルール ](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) を実装します。
   * ID 名前空間（例：電子メール、b2b_person）を使用して人物レコードをリンクする方法を定義します。
   * AEPで ID 名前空間と ID ステッチルールを設定します。
   * サンプルの人物データとプレビューツールを使用してリンクを検証します。
* [ プロファイル ](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#enable-profile) の個人、会社、機会、および活動データセットを有効にします
* 最初の [ アカウントオーディエンス ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/accounts/account-audience-overview) を定義
* アカウントオーディエンスを使用した [ 購入グループ ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/accounts/buying-groups/buying-groups-overview) または [ アカウントジャーニー ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview) の定義
   * 購入グループジョブは毎日実行され、アカウントオーディエンスまたは新しく関連付けられた人物として認定される新しいアカウントを処理します
   * 購買グループの保守は毎週金曜日の午前 0 時（CT）に実行されるため、メンバーの削除や新しく認定されたメンバーの追加は金曜日にのみ行われます

## 推奨設定

実装を効率化しAdobe Journey Optimizer B2B editionとの互換性を確保するには、次の設定をお勧めします。

* **デフォルトの ID フィールドを使用：**
   * _email_ および _b2b_person_ は、ID スティッチングとオーディエンスアクティベーションをサポートするために、人物スキーマの ID フィールドとして保持する必要があります。
* **Marketo Source Connector のデフォルトのマッピングを使用する：**
   * Adobeが提供する標準のフィールドマッピングを活用して、データ取り込みを簡素化し、設定のオーバーヘッドを削減します。
* **AJO B2B にデフォルトのマッピングを使用：**
   * Journey Optimizer B2B editionの [ 標準フィールドマッピング ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/accounts/field-mapping) を採用して、購買グループロジックおよび journey orchestration との互換性を確保します。
* **メールを除くすべてのフィールドでフィールドの更新をブロック：**
   * Marketo Engageで、「電子メール [ を除くすべてのフィールドについて、Adobe Experience Platformからの ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) 更新をブロック _するようにフィールド管理を設定し_ す。 これにより、ID 解決を可能にしながら、データの整合性を維持できます。
* **メールを一意の ID 名前空間として使用して ID リンクルールを実装する**
   * [ メール ](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) を一意の ID 名前空間として明示的に使用するように、Adobe Experience Platformで _ID グラフリンクルール_ を設定します。 これらのルールにより、_メール_ が存在するデータソース間でプロファイルが正確に結び付けられ、堅牢な ID 解決が可能になります。 Adobeのベストプラクティスに従って、一貫性がありプライバシーに準拠した ID グラフを維持するために、メールを安定したグローバルに一意の ID として優先付けするリンクルールを定義します。
この設定により、デプロイメントの容易さとデータガバナンスのバランスが取れるので、B2B ジャーニーを調整するための信頼性の高い基盤が確保されます。

## 実装に関する考慮事項

Adobe Journey Optimizer B2B editionを実装する場合、Real-time Customer Data Platform が提供する ID ステッチ機能を理解することが重要です。 このプラットフォームは、人物レベルとアカウントレベルの両方で ID ステッチを実行し、顧客データの統一されたビューを確保します。

### キーポイント

* **ID ステッチ**:Platform は、Marketo ID、CRM ID、メールなどのデフォルトの識別子を使用して ID をステッチします。 これは、様々なソースからのデータを結合して、包括的なプロファイルを作成する際に役立ちます。
* **潜在的なリスク**：メールをステッチの識別子として使用すると、意図しない ID の崩壊につながる可能性があります。 つまり、同じメールアドレスを共有する複数の個人が、誤って 1 つのプロファイルに結合される可能性があります。 この ID の崩壊は、CRM データの精度に悪影響を与え、整合性を損なう可能性があります。
* **結合戦略**:B2B CDP は、特定のプロファイル属性の最新の lastUpdatedDate を使用する、時間ベースの結合戦略を採用しています。 この方法を使用すると、最新のデータがプロファイルに反映されます。
* **メールに関する考慮事項**：プロファイルフラグメントを結合するための識別子として、メールの使用について十分に評価する必要があります。 有益な場合もありますが、ID の崩壊のリスクは、利点に対して慎重に考慮する必要があります。 1 つの欠点は、ID としてメールがない場合、AJO B2B で作成された外部オーディエンスメンバーシップは既存のプロファイルに統合されないことです。
* **Marketo ユーザー統合**:AJO B2B は、複数のMarketo レコードが 1 つのプロファイルに結合される場合に、最もリード ID が低いMarketo ユーザーを使用します。

これらの点を念頭に置くことで、Adobe Journey Optimizer B2B editionでの ID ステッチの設定方法について十分な情報に基づいた意思決定を行い、正確で信頼性の高い顧客プロファイルを確保できます。

### Id ステッチの結果の評価

クエリサービスを使用して、プロファイルが有効になっていないデータセットで ID ステッチの影響を確認できます。 次のクエリを使用して、評価を実行できます

#### 取り込まれたレコード数

このクエリは、人物プロファイルデータセットに取り込まれたレコードの合計数を返します

```sql
select
    count(distinct b2b.personKey.sourceKey)
from
    marketo_person_ajo_b2b
```

#### メールを複製

このクエリは、プラットフォームの ID ステッチの一部として結合される人物レコードの数を返します

```sql
select
    SUM(personCount)
from
    (
        select
            emailAddress,
            count(*) as personCount
        from
            (
                select
                    MAX(workemail.address) as emailAddress
                from
                    marketo_person_ajo_b2b
                where
                    workemail.address IS NOT NULL
                group by
                    b2b.personKey.sourceKey
            )
        group by
            emailAddress
        having
            count(*) > 1
    )
```

#### レコードが重複しているメールアドレス

このクエリを実行すると、データセット内の重複レコードが最も多いメールが返されます。  このリストを使用すると、これらのレコードの一部をチェックして、ID のリンクがMarketoと CRM に与える影響をより深く理解できます。  ID リンクの仕組みについて詳しくは、[ID サービスの概要 ](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) を参照してください。

```sql
select
    *
from
    (
        select
            emailAddress,
            MAX(personId) as personId,
            count(*) as personCount
        from
            (
                select
                    b2b.personKey.sourceKey,
                    MAX(workemail.address) as emailAddress,
                    MAX(b2b.personKey.sourceId) as personId
                from
                    marketo_person_ajo_b2b
                where
                    workemail.address IS NOT NULL
                group by
                    b2b.personKey.sourceKey
            )
        group by
            emailAddress
        having
            count(*) > 1
    )
order by
    personCount desc
```

### オプション

#### Id としての電子メールの削除

分析後、メールが ID フィールドとして使用できる有効なフィールドではないと判断した場合、人物スキーマを変更して [ID フィールドとしてメールを削除 ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/identity) することができます。

#### Adobe Experience Platformからの更新をブロック

メールを ID フィールドとして保持することがユースケースに最適な場合は、AJO B2B からの [ フィールドの更新をブロック ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) するオプションがあり、AJO B2B を主にMarketo データに対して実行できます。

## ガードレール

Marketo Engageとの B2B ジャーニーに適用されるガードレールの包括的な理解については、次の公式ドキュメントを参照してください。

* [Adobe Journey Optimizer B2B edition – 製品説明 ](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer-b2b.html)
Journey Optimizer B2B edition固有のガードレールと使用パラメーターが含まれます。
* [Adobe Experience Platform デプロイメントガードレール ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails?lang=en)
Adobe Experience Platform ソリューション全体の一般的なアーキテクチャおよびデプロイメントガードレールについて説明します。
* [Adobe Marketo Engage – 製品の説明 ](https://helpx.adobe.com/legal/product-descriptions/adobe-marketo-engage---product-description.html#performance-guardrails)
アクティベーションや CRM 同期に関する考慮事項など、Marketo Engageのパフォーマンスと使用に関するガードレールについて詳しく説明します。
* [Real-Time CDPガードレール ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview?lang=en)
Real-Time Customer Data Platform内でのデータ取得、セグメント化、アクティブ化の制限に関するガイダンスを提供します。

## 関連ドキュメント

* [Real-time Customer Data Platform B2B エディション](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [Real-time Customer Data Platform B2B editionの概要 ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Real-time Customer Data Platform B2B editionのガードレール ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform)
* [Adobe Experience Platform ID サービス ](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
* [Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)
* [Adobe Experience Platform - Marketo ソースコネクタ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
* [Adobe Journey Optimizer B2B edition ドキュメント ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
