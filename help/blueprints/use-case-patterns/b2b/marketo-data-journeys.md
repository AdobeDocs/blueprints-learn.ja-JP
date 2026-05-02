---
title: Adobe Marketo Data Blueprintを活用したB2Bジャーニー
description: Marketo Engage データを使用したJourney Optimizer B2B editionの迅速なデプロイメントの設計図。
solution: Journey Optimizer B2B Edition
source-git-commit: 8284380fb9202991f3da7d755225da2e38a50cac
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 2%

---

# Adobe Marketo Data Blueprintを活用したB2Bジャーニー

この包括的なガイドでは、Marketo EngageとAdobe Journey Optimizer B2B editionを統合するプロセスの概要を説明します。 カスタムスキーマの設定、プロファイルとアカウントの取り込み、購買グループに対するパーソナライズされたジャーニーのオーケストレーションについて説明します。 この設計図は、Marketo Engageのデータを活用することで、複数のチャネルをまたいで正確なターゲティングとエンゲージメントを実現し、より質の高い需要を促進して、顧客体験を向上させるのに役立ちます。

## ユースケース

* **購買グループの作成と管理**：生成AIを使用して、ターゲットアカウント内の購買グループを作成および管理し、主要な関係者を包括的にカバーします
* **メンバー割り当ての自動化**: コンテンツの利用やCRM データなど、定義された条件に基づいて、購買グループの役割にメンバーを自動的に割り当てます
* **パーソナライズされたジャーニー**：役割、アカウント、製品への興味、ライフサイクルステージに基づいて、各購買グループやメンバーに合わせたマルチステップのジャーニーを設計して可視化します
* **リアルタイム自動化**：リアルタイムのエンゲージメントトリガーと適格性スコアリングにより、ジャーニーを通じたアカウントと購買グループの進行を自動化します
* **Cross-Channel Engagement**：電子メール、SMS、広告、チャット、イベント、ウェビナーなど、複数のチャネルをまたいで購買グループをエンゲージし、需要創出と選定を合理化します
* **AIを活用したインサイト**: AIを活用したインサイトを使用して、購入者および購買グループ全体に対してコンテンツ配信とエンゲージメント戦略を最適化します
* **統合データアクティベーション**：購買グループを作成および管理するための最新かつ包括的なデータを提供するために、Adobe Real-Time Customer Data Platformから統合アカウントリストをアクティベートします
* **強化されたCollaboration**: マーケティング活動と営業活動を調整して、より正確な販売機会を生み出し、パイプラインの構築を加速させます

## アプリケーション

* Journey Optimizer B2B Edition
* Real-time Customer Data Platform B2B エディション
* Marketo Engage

## 統合パターン

| 統合 | 説明 |
| :-- | :--- |
| [Marketo Engage コネクタ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) | Adobe Experience Platformは、Marketoからのデータの取り込みを促進し、サービスを使用してデータを構造化、ラベル付け、強化する機能を提供します。 |
| [Journey Optimizer B2B edition - Marketo Engageのアクション &#x200B;](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes/action-nodes#marketo-engage-actions) | 人物ベースのアクションを使用して、Journey Optimizer B2B editionのAccount-Based MarketingをMarketo Engageのリードベースの取り組みと同期させ、リストメンバーシップの管理やキャンペーンのリクエストを行うことができます。 |

## アーキテクチャ

![Marketo データを使用したJourney Optimizer B2B editionのソリューションアーキテクチャ &#x200B;](/help/blueprints/b2b/assets/ajo-b2b-architecture-simplified.png){zoomable="yes"}

## 実装手順

1. 次のいずれかのオプションを使用して、B2B スキーマと名前空間をインストールします。
   * [Postman コレクション &#x200B;](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility){target="_blank"}を使用
   * Platform UIで[&#x200B; テンプレート &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/ui-tutorials/templates)を使用
1. ジャーニーの決定とメールのパーソナライズのための購入、ライセンス、イベント登録など、ビジネスエンティティを表すために、必要に応じて関連スキーマを作成します。
1. [XDM設定](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/admin/xdm-field-management/xdm-field-management){target="_blank"}を完了します。
   * Journey Optimizer B2B editionでデフォルトで選択されている標準XDM フィールドのセット（_管理フィールド_&#x200B;とも呼ばれます）を確認します。 **[!UICONTROL 管理]**/**[!UICONTROL 設定]**&#x200B;のXDM設定に移動して、管理フィールドのセットを確認します。
      * 「**[!UICONTROL 標準]**」タブを選択し、XDM個人プロファイルとXDM ビジネスアカウントの両方の&#x200B;**[!UICONTROL 管理フィールドを編集]**&#x200B;をクリックします。
      * 「**[!UICONTROL 選択したフィールドのみを表示]**」オプションを選択すると、選択したフィールドの現在のリストが表示されます。
      * 必要に応じてフィールドを追加または削除します。
         * `workEmail.address`は人物データセットに必要です。
         * `accountName`はアカウント データセットに必要です。
   * ジャーニーの&#x200B;_個人プロファイルの更新_&#x200B;および&#x200B;_アカウントプロファイルの更新_ アクションに使用するXDM フィールドのセットを設定します。 これらのフィールドは&#x200B;_更新可能フィールド_&#x200B;とも呼ばれます。
      * 「_[!UICONTROL 標準]_」タブで、「**[!UICONTROL 更新可能なフィールドを編集]**」をクリックして、XDM個人プロファイルとXDM ビジネスアカウントの両方を編集します。
      * 更新するスキーマ、データセット、フィールドを選択します。
   * ジャーニーで使用するリレーショナルスキーマとフィールドを設定します。
      * 「**[!UICONTROL リレーショナル]**」タブを選択し、「**[!UICONTROL リレーショナル XDM スキーマを選択]**」をクリックします。
      * 使用するスキーマ、名前空間およびフィールドを選択します。
   * ジャーニーで使用するエクスペリエンスイベントを設定します。
      * 「**[!UICONTROL イベント]**」タブを選択し、**[!UICONTROL エクスペリエンスイベントを選択]**&#x200B;をクリックします。
      * 使用するエクスペリエンスイベントとフィールドを選択します。
1. [Marketo Engage ソースコネクタ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)を設定します。
   * データディクショナリを使用して、ソースコネクタの[&#x200B; インポートマッピング &#x200B;](https://experienceleague.adobe.com/jp/docs/experience-platform/data-prep/ui/mapping#import-mapping)を定義します。
   * [実装に関する考慮事項](#implementation-considerations)を考慮する前に、プロファイルを有効にしないことをお勧めします。
   * また、アカウントのオーディエンスを作成する際に、これらのオブジェクトが最も有用であるため、最低でも人物、会社、機会、アクティビティを取り込むことをお勧めします。
1. [ID グラフ リンク ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/identity-graph-linking-rules/overview)をユーザーに対して実装します：
   * ID名前空間を使用して、個人レコードをリンクする方法を定義します。
   * Experience PlatformでID名前空間とID ステッチルールを設定します。
   * サンプルの人物データとプレビューツールを使用して、リンクを検証します。
1. [&#x200B; プロファイル &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/catalog/datasets/user-guide#enable-profile)の個人、企業、商談、アクティビティのデータセットを有効にする
1. 最初の[&#x200B; アカウントオーディエンス &#x200B;](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/audiences/account-audience-overview)を定義
1. アカウントオーディエンスを使用して、[購買グループ &#x200B;](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/accounts/buying-groups/buying-groups-overview)または[&#x200B; アカウントジャーニー](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)を定義します。
   * アカウントがアカウントオーディエンスに適格であると、購買グループのジョブが毎日実行され、オーディエンスが更新されるとすぐに、購買グループを作成し、関連する人々に役割を割り当てます。
   * さらに、購買グループのメンテナンスは毎週金曜日の深夜CTで実行されます。 この週次プロセスでは、資格を失ったメンバーの削除や、最初のオーディエンス更新中に取得されなかった新しい資格を持つメンバーの追加などの更新を処理します。

## 推奨される設定

実装を合理化し、Adobe Journey Optimizer B2B editionとの互換性を確保するには、次の設定をお勧めします。

* **既定のID フィールドを使用：**
   * IDの結合とオーディエンスのアクティブ化をサポートするために、_電子メール_&#x200B;と&#x200B;_b2b_ person_を個人スキーマのID フィールドとして保持する必要があります。
* **Marketo Source コネクタのデフォルトマッピングを使用：**
   * Adobeが提供する、すぐに利用できるフィールドマッピング機能を利用すれば、データの取り込みを簡素化し、設定のオーバーヘッドを削減できます。
* **AJO B2B:**&#x200B;のデフォルトマッピングを使用
   * 購買グループのロジックとジャーニーオーケストレーションとの互換性を確保するために、Journey Optimizer B2B editionの[標準フィールドマッピング &#x200B;](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/admin/xdm-field-management/field-mapping)を導入します。
* **電子メール：**&#x200B;を除くすべてのフィールドのフィールド更新をブロック
   * Marketo Engageでは、_電子メール_&#x200B;を除くすべてのフィールドについて、Adobe Experience Platformから[&#x200B; ブロック更新](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field)するようにフィールド管理を設定します。 これにより、ID解決を可能にしながら、データの整合性を維持できます。
* **電子メールを一意のID名前空間として使用してID リンクルールを実装**
   * _電子メール_&#x200B;を一意のID名前空間として明示的に使用するように、Adobe Experience Platformの[ID グラフ リンク ルール &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/identity-graph-linking-rules/overview)を設定します。 これらのルールにより、_email_が存在するデータソースをまたいでプロファイルが正確に結合され、堅牢なID解決が可能になります。 Adobeのベストプラクティスに従って、一貫性のあるプライバシーに準拠したID グラフを維持するために、グローバルで一意の安定したIDとしてメールを優先するリンクルールを定義します。
この設定は、容易な導入とデータガバナンスのバランスを取り、B2B ジャーニーを調整するための信頼性の高い基盤を提供します。

## 実装に関する考慮事項

Adobe Journey Optimizer B2B editionを導入する際は、Adobe Real-Time CDPのID照合機能を理解することが重要です。 このプラットフォームは、個人レベルとアカウントレベルの両方でIDをつなぎ合わせ、顧客データの統一されたビューを保証します。

### キーポイント

* **IDの結合**: プラットフォームは、Marketo ID、CRM ID、電子メールなどのデフォルトのIDを使用してIDを結合します。 これにより、さまざまなソースからデータを統合して、包括的なプロファイルを作成できます。
* **潜在的なリスク**：電子メールをステッチの識別子として使用すると、意図しないIDの折りたたみが発生する可能性があります。 つまり、同じメールアドレスを共有する複数の個人が、誤って単一のプロファイルに統合される可能性があります。 このIDの統合は、CRM データの精度に悪影響を与え、その整合性を損なう可能性があります。
* **結合戦略**: B2B CDPは時間ベースの結合戦略を採用しています。この戦略では、特定のプロファイル属性に対する最新のlastUpdatedDateが使用されます。 この戦略により、最新のデータがプロファイルに反映されます。
* **電子メールに関する考慮事項**: プロファイルフラグメントを結合するための識別子として電子メールを使用する方法を徹底的に評価することが重要です。 それは有益である可能性がありますが、IDの崩壊のリスクは、利点に対して慎重に検討する必要があります。 ただし、欠点がひとつあります。識別子として電子メールを使用しない場合、AJO B2Bによって作成された外部オーディエンスメンバーシップが、既存のプロファイルに統合されません。
* **Marketo人物の統合**：複数のAJO レコードが1つのプロファイルに結合される場合、Marketo B2Bは最も低いリード IDのMarketo人物を使用します。

これらの点を念頭に置くことで、Adobe Journey Optimizer B2B editionでID合成を設定する方法について、情報に基づいた意思決定を行うことができ、正確で信頼性の高い顧客プロファイルを実現できます。

### Id照合の結果の評価

クエリサービスを使用すると、プロファイルが有効になっていないデータセットでID ステッチの影響を確認できます。 次のクエリを使用して、評価を行うことができます

#### 取り込まれたレコード数

このクエリは、人物プロファイルデータセットに取り込まれたレコードの合計数を返します

```sql
select
    count(distinct b2b.personKey.sourceKey)
from
    marketo_person_ajo_b2b
```

#### メールの重複

このクエリは、プラットフォームのID ステッチの一部として結合される人物レコードの数を返します。

>[!NOTE]
>
>データセットテーブル marketo_person_ajo_b2bを使用して、Marketo Person データセットの操作方法の完全な例を示します。
>サンドボックスのデータセットは、[&#x200B; データセット &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/catalog/datasets/user-guide) ワークスペースで見つけることができます。

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

#### 重複したレコードを持つメールアドレス

このクエリは、データセット内で最も重複したレコードを含むメールを返します。  このリストを使用すると、これらのレコードの一部を確認して、IDのリンクがMarketoとCRMに与える影響をより詳細に把握できます。  ID リンクの仕組みについて詳しくは、[ID サービスの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)を参照してください。

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

#### 電子メールをIDとして削除

分析後、電子メールがID フィールドとして使用する有効なフィールドではないと判断した場合、人物スキーマを[ID フィールドとして電子メールを削除](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/ui/fields/identity)に変更できます

#### Adobe Experience Platformから更新をブロック

電子メールをID フィールドとして保持することがユースケースに最適な場合は、AJO B2Bから送信されるフィールド更新を[&#x200B; ブロック &#x200B;](https://experienceleague.adobe.com/ja/docs/marketo/using/product-docs/administration/field-management/block-updates-to-a-field)し、AJO B2Bを主にMarketo データで実行できるようにするオプションがあります。

## ガードレール

Marketo Engageを使用したB2B ジャーニーに適用されるガードレールについて詳しくは、次の公式ドキュメントを参照してください。

* [Adobe Journey Optimizer B2B edition – 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-journey-optimizer-b2b.html)
Journey Optimizer B2B editionの特定のガードレールと使用パラメーターが含まれています。
* [Adobe Experience Platformのデプロイメントガードレール](https://experienceleague.adobe.com/ja/docs/blueprints-learn/architecture/architecture-overview/guardrails?lang=en)
Adobe Experience Platform ソリューション全体の一般的なアーキテクチャおよびデプロイメントのガードレールについて説明します。
* [Adobe Marketo Engage – 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-marketo-engage---product-description.html#performance-guardrails)
アクティベーションやCRM同期に関する考慮事項など、Marketo Engageのパフォーマンスと使用ガードレールを詳しく説明します。
* [Real-Time CDP ガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/guardrails/overview?lang=en)
Real-Time Customer Data Platform内でのデータの取り込み、セグメンテーション、アクティベーションの制限に関するガイダンスを提供します。

## 関連ドキュメント

* [Adobe Real-Time CDPのB2B editionは](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
* [Adobe Real-Time CDP B2B editionの導入方法](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [Adobe Real-Time CDP B2B editionのガードレール](https://experienceleague.adobe.com/ja/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/ja/docs/experience-platform)
* [Adobe Experience Platform ID サービス](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/home)
* [Marketo Engage](https://experienceleague.adobe.com/ja/docs/marketo/using/home)
* [Adobe Experience Platform - Marketo Source Connector](https://experienceleague.adobe.com/ja/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
* [Adobe Journey Optimizer B2B edition ドキュメント](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/guide-overview)
* [XDM フィールド管理（Journey Optimizer B2B edition）](https://experienceleague.adobe.com/ja/docs/journey-optimizer-b2b/user/admin/xdm-field-management/xdm-field-management)
