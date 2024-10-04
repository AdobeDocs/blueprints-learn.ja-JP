---
title: 購買グループベースのマーケティングおよびジャーニー管理のブループリント
description: Adobe Journey Optimizer B2B editionで、リードを購入グループに選定するジャーニーを作成、デザイン、構築する方法を説明します。
solution: Journey Optimizer B2B Edition
source-git-commit: 5035c869aa5181fff66cbc20b03922f82832f126
workflow-type: tm+mt
source-wordcount: '2129'
ht-degree: 0%

---

# 購買グループベースのマーケティングおよびジャーニー管理のブループリント

現在、マーケティングチームは、セールス部門に適格なリードを提供する際に、多くの課題に直面しています。 これらの課題の 1 つは、組織内の適切な人材と協力することです。通常、労力と精度の点で明らかです。 _リードスコアリング_ では、グループが狭すぎて、チームが適切な人物を逃す可能性があります。 _アカウントのスコアリング_ を使用すると、アカウントの全体像を持つ適切な人物を識別するために必要な労力が増します。

この課題に対して、「購買グループ **_の概念_** を導入します。 購入グループを使用すると、マーケターは、アカウント内の適切なユーザーグループを見つけ、リードを絞り込み、グループ内での自分の役割を特定するというレンズを通じてこれらの個人と協力できます。

## 購入グループを使用してリードとアカウントを選定する方法

購買グループを作成し、それを達成するために努力することで、セールス・オポチュニティの見極めにおけるマーケティング活動の有効性が向上します。 購入グループは、合致するリードと、ソリューションの意図にリンクされた役割テンプレートを結び付けることに依存します。

購入グループの例としては、_AI Driven Seeds_ のソリューション関心を持つ _Acme Corp Seeds Buying Group_ があります。

購入グループは、ソリューションのインテントを通じてソリューションに関心を持つ企業の人物のグループを表します。 また、1 つの購入グループが複数のソリューションの関心について識別され、個人が複数の購入グループに表示される場合もあります。

Journey Optimizer B2B editionが提供する強化された B2B 機能により、次の課題に対処できるようになりました。

* _顧客第一_ のマーケティングキャンペーンがない。
* マーケティング認定リード（MQL）からセールス認定リード（SQL）へのコンバージョンが一貫していない。MQL を育成するには、イニシアチブとセールスを連携させる必要がある
* _競合_ アカウントを特定してターゲットを設定するための拡張性の高いメカニズムがない
* 収益とパイプラインにおける集中リスク。

次の KPI は、ユースケースの成功を測定することと適切に一致しています。

* **認識**：ターゲット顧客はあなたの広告を見ていますか、そしてそれは以前よりも高い割合であなたのウェブサイトにそれらを駆動しますか？
* **エンゲージメント**：ターゲット顧客が web サイトを閲覧してコンテンツに関与しているか。
* **時間**：セールスチームが様々なツールから連絡先を見つけてオポチュニティに追加するのにかかる時間はどれくらいですか？
* **コスト**：各プラットフォームのリードコストはどれくらいですか？

## アカウントベースドマーケティング

一般的なユースケースであり、このブループリントで重点的に取り組んでいるのは、アカウントベースのマーケティングイニシアチブです。作成した購入グループが役割とソリューションの関心に関連付けられている場合に、そのグループにリードが割り当てられるポイントを調査します。

個人をジャーニーに導くと、フォーム、CRM 同期、LinkedInのアクティベーションを通じて、リード（購入グループワークフロー）に関する詳細が収集されます。

リードがソリューションの関心を明確に示す場合は、ビジネスレンズによって定義されたビジネスイベントを示します。 この時点で、このリードは商品に本当に興味を持っており、Journey Optimizer B2B editionでは、ロールテンプレート内のそのソリューションの購入グループ（インフルエンサー、意思決定者、チャンピオン、スポンサーなど）に関連付けられているとビジネスは確信しています。

次の図に示すように、フォームまたはLinkedInのアクティベーションを通じて詳細を収集し、チャットボットとのインタラクションが発生した場合のソリューションインテントを確認できます。

![ 購入グループジャーニー ](./assets/buying-group-journey-diagram.svg){zoomable="yes"}

購入グループの完了率が十分に高い場合は、SQL または SOL を使用してグループを営業チームに共有し、アカウント内のリードを完了済みの販売に変換します。

## アカウント中心のソリューション

B2B のリード管理の焦点は、アカウントとそのリードにあります。 技術レイヤーは、これらの特性を表すデータをサポートするように設定されています。これは、アカウントのセグメント化とジャーニーの管理を成功させるための要件です。

### 要件

アカウント中心のソリューションには、次のアプリケーションとサービスが必要です。

* Adobe Journey OptimizerB2B edition
* Adobe Real-time Customer Data Platform（RTCDP）B2B edition
* Adobe Marketo Engage

>[!NOTE]
>
>Journey Optimizer B2B editionのライセンスには、次の項目を含める必要があります。
><ul><li>Experience Platform B2B に接続されたJourney Optimizer B2B edition インスタンス</li><li>RTCDP に同期されたMarketo Engageインスタンス</li></ul>
&gt;<br/>
&gt; 既存のMarketo Engageユーザーの場合は、既存のインスタンスへの接続を使用することをお勧めします。
&gt;<br/><br/>
&gt; プロファイルの豊富さを強化するために、ソリューションで使用できる追加の拡張機能があります。
&gt;<ul><li>プロファイルを強化するための RTCDP への追加のソース</li><li>RTCDP 宛先からMarketo Engageへ</li></ul>

_このソリューションを導入するには、「アカウント_ および _購入グループ_ の概念を明確に理解し、それらがセールス・リードの認定をどのように強化および促進するかについての理解も必要です。 この理解により、必要な購入グループの完全性スコアも特定する必要があります。

### アーキテクチャ

![ 購入グループベースのマーケティングおよびジャーニー管理のためのソリューションアーキテクチャ ](./assets/ajo-b2b-architecture.png){zoomable="yes"}

### データスキーマ

データ駆動型マーケティング自動化の実装では、スキーマの設計は実装を成功させるために重要です。 スキーマを設計する前に、[B2B 名前空間とスキーマを確認し ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo-namespaces) 新しい実装シナリオで新しいスキーマを生成するために使用できる自動生成ユーティリティについて理解していることを確認してください。

プロファイルの豊富な関係をサポートし、イベントとプロファイルをアカウントスキーマに結び付ける `sourceKey` ールを通じてアカウントの観点を含むために、スキーマには B2B データ要素が具体的に使用されます。 スキーマは、組織の要件、および収集されプロファイルされたデータを表すものです。 これらのニーズを満たすために、B2B スキーマは柔軟で、必要な B2B 要素の拡張機能です。

組織のデータスキーマを設計する際には、[RTCDP B2B スキーマのドキュメント ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-b2b) の最初の図で、ERD のメインエンティティを表し、高レベルのエンティティにラベルを付けるのがベストプラクティスです。 このプロセスは、各スキーマで定義する必要がある必須のデータ要素を理解するのに非常に役立ちます。

この段階では、エクスペリエンスイベントはまだジャーニーに影響を与えることができません。 エクスペリエンスイベントスキーマに加えて、ユーザーアクティビティに基づく主要な決定を表すプロパティをアカウントに追加することをお勧めします。 これらのプロパティは、ジャーニーデザイナーの分割パス要素に使用されます。

>[!NOTE]
>
>現在、Journey Optimizer B2B editionでサポートされている唯一の関係は、`Person` エンティティの `personComponents[0].sourceAccountKey.sourceKey` 属性を介した直接の関係です。 今後、B2b スキーマのアカウントと人物の関係オブジェクトに対応する拡張が予定されています。

### Marketo Engageソースコネクタ

アカウントデータ要素を強化するには、Marketo Engageとその B2B データを使用して、RTCDP とJourney Optimizer B2B editionのアカウントビューを強化します。 Marketo Engage Source コネクタを設定し、Marketo Engageデータを RTCDP スキーマ属性にマッピングすると、データがMarketo Engageから RTCDP に送られ、指定されている場合はプロファイルに送られます。

コネクタ設定および前の手順で定義したスキーマへの必須フィールド マッピングについて詳しくは ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)[Marketo Engageコネクタのドキュメント } を参照してください。

### ガードレール

Journey Optimizer B2B editionのガードレールについて詳しくは、[ 製品説明ページ ](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer-b2b.html) を参照してください。

実装に関連するガードレール

* すべての B2B オーディエンスガードレールは、[B2B オーディエンスとプロファイルアクティベーションのブループリントに記載されており ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails)Journey Optimizer B2B editionの成功に直接転置されます。
* アカウントジャーニーのMarketo Engageチャネルを通じてアクティベーションが必要な場合、または CRM Sync を使用してアカウントをエンリッチメントする場合は、[Marketo Engage関連のガードレール ](https://helpx.adobe.com/legal/product-descriptions/adobe-marketo-engage---product-description.html#performance-guardrails) が関連します。

RTCDP ガードレールについて詳しくは ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview)[Real-Time CDP ガードレールのドキュメントを参照してください。

### プロビジョニング

* すべてのインスタンスは、同じ IMS 組織にある必要があります。
* 1 つのExperience PlatformサンドボックスにリンクできるJourney Optimizer B2B edition インスタンスは 1 つだけです。
* [Real-time Customer Data PlatformへのMarketo Source コネクタ ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) を実装することを強くお勧めします。

## 実装

次の手順では、Journey Optimizer B2B edition インスタンスで購入グループ機能を有効にする際のガイダンスを示します。また、ロールテンプレートがない購入グループに重点を置き、アカウントベースの拡張をサポートするためにアクティベーションを追加します。

### 前提条件となる手順

1. アカウントとリードのビジネスビューを表す XDM スキーマを定義します。

   最初の手順として、B2B のユースケースのニーズに合わせて設計され、データソースをバッチおよびリアルタイムの両方でカバーするエクスペリエンススキーマを定義し作成します。 このデザインは、アカウントや人物のエンティティに関するビジネスの考え方や、サポートするユースケースを表している必要があります。 スキーマを B2B スキーマにするには、[RTCDP B2B スキーマのドキュメント ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-b2b) に記載されている構造に従う必要があります。

   便利な方法は、図からエンティティ名を取得し、同じ方法でラベルを付けてスキーマ内のそれらのエンティティを識別することです。 一部のスキーマでは、RTCDP B2B で機能するために `sourceKey` などの特定のキーが必要です。 短期的に言えば、Journey Optimizer B2B では、アカウント人物関係を通じたアカウントと人物の間の _多対多_ 関係はサポートされていません。 最適な出発点として、アクセラレータスクリプトを使用します。

   * [RTCDP B2B スキーマ作成スクリプト ](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) を使用して、初期スキーマを生成します
   * 組織のニーズに合わせてスキーマを完成させるために生成されたスキーマに、ユースケース固有のフィールドを追加します。

   この段階では、Marketo Engageと RTCDP 間の接続が設定され、アカウントセグメントのデータセットに入力するアカウントおよび人物データを受け入れるスキーマ構造が定義されています。 次の手順では、RTCDP をMarketo EngageおよびJourney Optimizer B2B editionと接続します。

1. Marketo Engageの XDM 構造へのマッピングを含む、Marketo Engageコネクタを設定します。

   XDM 構造とフィールドを配置したら、コネクタを使用してMarketo Engageを RTCDP に接続します。コネクタは、Marketo EngageとJourney Optimizer B2B のデータをデータセットにフィードします。 まず、Marketo Engageから RTCDP クラスへのフィールドのマッピングを構成します。 [ コネクタドキュメント ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo#field-mapping-from-marketo-engage-to-xdm) の情報を使用して、Marketo Engage実装から含めるフィールドを特定します。

### 購買グループ構成

1. Journey Optimizer B2B editionまたは RTCDP でアカウントオーディエンスを作成します。

   Customer → Audiences →の参照ページで「すべてのオーディエンスをスケジュールする」オプションを有効にして、アカウントオーディエンスを有効にします。 （これが機能しない場合は、アカウントオーディエンスを作成できるように、顧客プロファイルセグメントを作成する必要があります）

   セグメントを作成するには、[ アカウントオーディエンスドキュメント ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-audiences/account-audience-overview) の手順に従います。 アカウントオーディエンスのキーとして特定したデータフィールドでのセグメントビルダーの使用は、オーディエンスを定義する際の主要なアクティビティになります。

   この段階では、アカウントが RTCDP を通じてに焦点を当て、購入グループの構成要素にを使用することを知っています。

1. 役割テンプレートを定義します。

   各購入グループで、対処するグループにおける個人の役割を表す役割を特定します。 例えば、_decision maker_、_influencer_、および _champion_ を使用できます。 また、この役割の重み付けと条件を購入グループで定義します。

   このプロセスと特別な条件の定義方法については、[ 役割テンプレートのドキュメント ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates) を参照してください。

1. ソリューションの関心を定義します。

   ソリューションへの関心は、マーケティング活動や戦略に対する購買グループのフォーカスを示す方法です。

   ソリューションの関心を定義するには、[ ソリューションの関心に関するドキュメント ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests) の手順に従ってください。 購買グループを組織内の営業構想に照合するために使用します。

1. 購入グループを設定します。

   購入グループの構成要素の準備が整ったら、ソリューションの興味とアカウントオーディエンスの購入グループをターゲットで設定し、アカウントの適切なメンバーで役割テンプレートを完了させます。 この設定では、特定した役割テンプレートにソリューションの関心を割り当て、その特定の製品のセールス成功に各役割に重みを付けます。

   購入グループを作成するには、[ 購入グループのドキュメント ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create) の手順に従います。

   この段階では、[ ジャーニーを作成 ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview#get-started-with-a-journey) して、アカウントオーディエンスとの連携を開始し、購入グループを構築してソリューションの利益に適合させる準備が整います。

### Audience activation

オーディエンスアクティベーションにより、購入グループの完全性を高めます。

1. linkedIn広告に一致したアカウントオーディエンスを定義します。

   Journey Optimizer B2B editionは、メールやフォームの入力アクティビティに加えて、LinkedIn広告機能を提供して、アカウントの幅を広げ、アカウントリードの範囲を拡大しマーケティングアクティビティのリーチを上げることで、購入グループの締結をサポートします。

   購入グループの完了や関与が十分でないアカウントとのコミュニケーションにLinkedIn ペイドメディアを使用する場合、アカウントオーディエンスを拡張または関与させるには、[LinkedIn アカウントマッチドオーディエンス機能 ](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-audiences/linkedin-account-matched-audiences) を使用して、アカウントマッチドオーディエンスを通じてLinkedIn広告オーディエンスを生成します。

1. 購入グループのオーディエンスを有効化します。

>[!TIP]
>
>キャンペーンを成功させるためのヒント：
>
>* キャンペーンには、ROI を向上させるために、役割が欠落している購入グループに適合する役割フィルターを含める必要があります。
>* リードをキャプチャするには、ダイレクトリードを使用してフォーム（LinkedInまたはMarketo Engageフォーム）に入力し、フォームミスをリターゲティングします。
