---
title: Marketo データブループリントを使用した B2Bジャーニー
description: Marketo Engage Data を使用したJourney Optimizer B2B editionの迅速なデプロイメントのブループリント。
solution: Journey Optimizer B2B Edition
exl-id: d7bd0bd3-0f61-4e59-855f-27afc147c9aa
source-git-commit: c8ea7b87270a25420ad43dae4384d70603f00dcd
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 2%

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
| [Marketo Engage コネクタ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) | Adobe Experience Platformは、Marketoからのデータの取り込みを容易にし、そのサービスを使用してデータの構造化、ラベル付け、拡張を行う機能を提供します。 |
| [Journey Optimizer B2B edition - Marketo Engageのアクション &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes/action-nodes#marketo-engage-actions) | 人物ベースのアクションを使用してリストメンバーシップを管理し、キャンペーンをリクエストすることで、Journey Optimizer B2B editionのAccount-Based MarketingをMarketo Engageのリードベースの取り組みと同期させます。 |

## アーキテクチャ

![Marketo data を使用したJourney Optimizer B2B editionのソリューションアーキテクチャ &#x200B;](./assets/ajo-b2b-architecture-simplified.png){zoomable="yes"}

## 実装手順

1. 次のいずれかのオプションを使用して、B2B スキーマと名前空間をインストールします。
   * [Postman コレクション &#x200B;](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility){target="_blank"} を使用
   * Platform UI での [templates](https://experienceleague.adobe.com/en/docs/experience-platform/sources/ui-tutorials/templates) の使用
1. ジャーニー決定とメールのパーソナライゼーションのための購入、ライセンス、イベント登録など、ビジネスエンティティを表すために必要に応じて、リレーショナルスキーマを作成します。
1. [XDM 設定 &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/admin/xdm-field-management/xdm-field-management){target="_blank"} を完了します。
   * Journey Optimizer B2B editionでデフォルトで選択される一連の標準 XDM フィールド（「管理フィールド _も呼ばれます_ を確認します。 **[!UICONTROL 管理]**/**[!UICONTROL 設定]** の XDM 設定に移動して、管理フィールドセットを確認します。
      * **[!UICONTROL 標準]** タブを選択し、XDM 個人プロファイルと XDM ビジネスアカウントの両方で **[!UICONTROL 管理フィールドを編集]** をクリックします。
      * 「**[!UICONTROL 選択したフィールドのみを表示]**」オプションを選択して、選択したフィールドの現在のリストを表示します。
      * 必要に応じてフィールドを追加または削除します。
         * 人物データセットには `workEmail.address` が必要です。
         * アカウントデータセットには `accountName` が必要です。
   * ジャーニーの _人物プロファイルを更新_ および _アカウントプロファイルを更新_ アクションに使用する XDM フィールドのセットを設定します。 これらのフィールドは、_更新可能フィールド_ とも呼ばれます。
      * 「_[!UICONTROL 標準]_」タブで、XDM 個人プロファイルと XDM ビジネスアカウントの両方に対して「**[!UICONTROL 更新可能なフィールドを編集]**」をクリックします。
      * 更新するスキーマ、データセット、フィールドを選択します。
   * ジャーニーで使用するリレーショナルスキーマとフィールドを設定します。
      * 「**[!UICONTROL リレーショナル]**」タブを選択し、「**[!UICONTROL リレーショナル XDM スキーマを選択]**」をクリックします。
      * 使用するスキーマ、名前空間およびフィールドを選択します。
   * ジャーニーで使用するエクスペリエンスイベントを設定します。
      * 「**[!UICONTROL イベント]**」タブを選択し、「**[!UICONTROL エクスペリエンスイベントを選択]** をクリックします。
      * 使用するエクスペリエンスイベントとフィールドを選択します。
1. [Marketo Engage ソースコネクタ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) を設定します。
   * データディクショナリを使用して、ソースコネクタの [&#x200B; マッピングをインポート &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/data-prep/ui/mapping#import-mapping) を定義します。
   * [&#x200B; 実装に関する考慮事項 &#x200B;](#implementation-considerations) を考慮する前に、プロファイルを有効にしないことをお勧めします。
   * また、人物、会社、機会およびアクティビティは、アカウントオーディエンスを作成する際に最も役立つので、少なくとも取り込むことをお勧めします。
1. 人物に対して [ID グラフリンクルール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) を実装します。
   * ID 名前空間を使用して、人物レコードのリンク方法を定義します。
   * Experience Platformで ID 名前空間と ID ステッチルールを設定します。
   * サンプルの人物データとプレビューツールを使用してリンクを検証します。
1. [&#x200B; プロファイル &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#enable-profile) のユーザー、会社、機会、およびアクティビティ データセットを有効にします
1. 最初の [&#x200B; アカウントオーディエンス &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/audiences/account-audience-overview) を定義
1. アカウントオーディエンスを使用して、[&#x200B; 購入グループ &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/accounts/buying-groups/buying-groups-overview) または [&#x200B; アカウントジャーニー &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview) を定義します。
   * アカウントがアカウントオーディエンスの資格を得ると、購入グループジョブが毎日実行され、オーディエンスが更新されるとすぐに、購入グループが作成され、関連するユーザーに役割が割り当てられます。
   * さらに、購買グループのメンテナンスは毎週金曜日の午前 0 時（CT）に実行されます。 この毎週のプロセスでは、資格を喪失したメンバーの削除や、最初のオーディエンスの更新時にキャプチャされなかった新しく資格を取得したメンバーの追加などの更新を処理します。

## 推奨設定

実装を効率化しAdobe Journey Optimizer B2B editionとの互換性を確保するには、次の設定をお勧めします。

* **デフォルトの ID フィールドを使用：**
   * _email_ および _b2b_person_ は、ID スティッチングとオーディエンスアクティベーションをサポートするために、人物スキーマの ID フィールドとして保持する必要があります。
* **Marketo Source Connector のデフォルトのマッピングを使用する：**
   * Adobeが提供する標準のフィールドマッピングを活用して、データ取り込みを簡素化し、設定のオーバーヘッドを削減します。
* **AJO B2B にデフォルトのマッピングを使用：**
   * Journey Optimizer B2B editionの [&#x200B; 標準フィールドマッピング &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/admin/xdm-field-management/field-mapping) を採用して、購買グループロジックおよび journey orchestration との互換性を確保します。
* **メールを除くすべてのフィールドでフィールドの更新をブロック：**
   * Marketo Engageで、「電子メール [&#x200B; を除くすべてのフィールドについて、Adobe Experience Platformからの &#x200B;](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) 更新をブロック _するようにフィールド管理を設定し_ す。 これにより、ID 解決を可能にしながら、データの整合性を維持できます。
* **メールを一意の ID 名前空間として使用して ID リンクルールを実装する**
   * [&#x200B; メール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-graph-linking-rules/overview) を一意の ID 名前空間として明示的に使用するように、Adobe Experience Platformで _ID グラフリンクルール_ を設定します。 これらのルールにより、_メール_ が存在するデータソース間でプロファイルが正確に結び付けられ、堅牢な ID 解決が可能になります。 Adobeのベストプラクティスに従って、一貫性がありプライバシーに準拠した ID グラフを維持するために、メールを安定したグローバルに一意の ID として優先付けするリンクルールを定義します。
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

このクエリは、プラットフォームの ID ステッチの一部として結合される人物レコードの数を返します。

>[!NOTE]
>
>データセットテーブル marketo_person_ajo_b2b を使用して、Marketo ユーザーデータセットの操作方法の完全な例を示します。
>サンドボックスのデータセットは、[&#x200B; データセット &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide) ワークスペースにあります。

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

このクエリを実行すると、データセット内の重複レコードが最も多いメールが返されます。  このリストを使用すると、これらのレコードの一部をチェックして、ID のリンクがMarketoと CRM に与える影響をより深く理解できます。  ID リンクの仕組みについて詳しくは、[ID サービスの概要 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) を参照してください。

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

分析後、メールが ID フィールドとして使用できる有効なフィールドではないと判断した場合、人物スキーマを変更して [ID フィールドとしてメールを削除 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/fields/identity) することができます。

#### Adobe Experience Platformからの更新をブロック

メールを ID フィールドとして保持することがユースケースに最適な場合は、AJO B2B からの [&#x200B; フィールドの更新をブロック &#x200B;](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field) するオプションがあり、AJO B2B を主にMarketo データに対して実行できます。

## ガードレール

Marketo Engageとの B2B ジャーニーに適用されるガードレールの包括的な理解については、次の公式ドキュメントを参照してください。

* [Adobe Journey Optimizer B2B edition – 製品説明 &#x200B;](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer-b2b.html)
Journey Optimizer B2B edition固有のガードレールと使用パラメーターが含まれます。
* [Adobe Experience Platform デプロイメントガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/guardrails?lang=en)
Adobe Experience Platform ソリューション全体の一般的なアーキテクチャおよびデプロイメントガードレールについて説明します。
* [Adobe Marketo Engage – 製品の説明 &#x200B;](https://helpx.adobe.com/legal/product-descriptions/adobe-marketo-engage---product-description.html#performance-guardrails)
アクティベーションや CRM 同期に関する考慮事項など、Marketo Engageのパフォーマンスと使用に関するガードレールについて詳しく説明します。
* [Real-Time CDPガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview?lang=en)
Real-Time Customer Data Platform内でのデータ取得、セグメント化、アクティブ化の制限に関するガイダンスを提供します。

## 関連ドキュメント

* [Real-time Customer Data Platform B2B エディション](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [Real-time Customer Data Platform B2B editionの概要 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Real-time Customer Data Platform B2B editionのガードレール &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform)
* [Adobe Experience Platform ID サービス &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
* [Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)
* [Adobe Experience Platform - Marketo ソースコネクタ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
* [Adobe Journey Optimizer B2B edition ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
* [XDM フィールド管理（Journey Optimizer B2B edition） &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/admin/xdm-field-management/xdm-field-management)
