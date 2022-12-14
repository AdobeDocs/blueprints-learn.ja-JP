---
description: 概要 — MarketoとWorkfrontを使用した Campaign サプライチェーンの最適化
title: 概要
source-git-commit: ecdc672b7667ff6e40fa37fdde698fd66ecafac9
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 0%

---

# 概要 {#overview}

## 最適化されたキャンペーンサプライチェーンにより、市場投入までの時間を短縮 {#achieving-faster-time-to-market-with-optimized-campaign-supply-chain}

マーケティングの仕事は、新しいチャネルや、コミュニケーションを日々パーソナライズする方法で増え続けています。 マーケティングチームは、世界中のマーケティングニーズの変化をサポートするために、自動化を続け、発展させる方法が必要です。

**「ROI は常に真の目標でした。 収入は大きいが、今日は特にコストはかからない」と述べた。 - CMO、ビジネスサービス業界**

売上高の増加と共に ROI の向上を実現している組織は、キャンペーンの開発プロセスを合理化し、キャンペーンの実行速度を最適化し、マーケティング機能全体にわたって監視を向上させることで、売上高を増やしています。

以下に説明するような目標を達成したい場合は、このドキュメントが役立ちます。

* 部門をまたいだマーケティングチームをサポートするようにキャンペーン運営を拡大
* キャンペーンリクエストプロセスの合理化により、市場投入までの時間を短縮
* 記録システムを確立し、キャンペーンの関係者間での可視性を高めます
* キャンペーンアセット（画像、E メールコピー）の確認と承認

キャンペーンの運用チームには、マーケティングキャンペーンを効率的かつ効果的に計画および実行できるシステムが必要です。 E メール、ウェビナー、イベント、有料メディア、育成またはコンテンツシンジケーションのどちらであっても、マーケティングチームはキャンペーンの寄稿者、成果物、実行を整理するための一元化されたソリューションが必要です。

マルチチャネルマーケティング有効化システム (Marketo Engage) をマーケティング計画や記録システム (Workfront) と統合することで、キャンペーンの速度を上げ、関係者の可視性を高めることができます。

Workfront Fusion を使用すると、マーケティングオペレーションチームは、マーケティング概要をキャンペーンに翻訳する際に、手動で誤りが生じやすい手順を大幅に排除できます。 Workfront Fusion は、WorkfrontとMarketo Engageの間に既製の統合レイヤーを備えており、システム間でのワークフロー開発を柔軟かつ効率的におこなうことができます。 統合を設定する方法と、ワークフローを自動化するために実行できるアクションについて詳しく学ぶことができます [ここ](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/marketo-modules.html){target=&quot;_blank&quot;}。

## キャンペーンの実行計画 — 自動化の使用例 {#campaign-planning-to-execution-automation-use-cases}

* Workfrontでの取り込みリクエストを通じてMarketo Engageでのキャンペーン作成を自動化し、マーケティング運用チームをサポートします
* Marketo Engageで作成された E メールとランディングページのドラフトをWorkfrontに共有して、部門をまたぐ関係者から最終レビューと承認を得る
* キャンペーンの結果をMarketo EngageからWorkfrontに共有し、キャンペーン指標へのアクセスを民主化します

以下に、E メールブラストリクエストの場合の、キャンペーンの開発プロセスのワークフロー図を示します。 さらに、Workfront Fusion がWorkfrontとMarketo Engageの間でどのように役割を果たし、キャンペーン開発サイクルを通じてワークフローとプロセスの自動化を推進しているかを確認できます。

![](assets/overview-1.png)

キャンペーンの開発プロセスの様々なフェーズに注意します。

1. 取り込みと作成：キャンペーンのリクエストが作成され、キャンペーンアセットがプログラムによって組み立てられます。

1. 配達確認と承認：キャンペーンがまとまると、関係者は e メールやランディングページなどのキャンペーンアセットを確認し、サインオフする時が来ます。

1. レポートと監査：キャンペーンの結果をWorkfrontに共有して、部門をまたぐ関係者をより詳細に把握できるようにします。

>[!NOTE]
>
>上記の例では、Workfrontは、Marketo Engageプログラムのライフサイクルを通じて、作業を管理および計画しています。 ただし、Workfrontの柔軟性は、マーケティングチームのあらゆる取り組みの管理にまで拡大できます。 これには、アカウントベースのマーケティング、マーケティングコンテンツサプライチェーン、代理店管理、デジタル/ソーシャルキャンペーン管理、販売イネーブルメントプログラムが含まれます。

## Workfrontでのマーケティングイニシアチブの表れ方について {#understanding-how-marketing-initiatives-are-represented-in-workfront}

Adobe Workfrontを使用すると、組織が作業を管理して、より効率的な実行を実現できます。 Workfrontには、様々なチーム間での計画、リソース管理、コラボレーションのためのフレームワークを提供するオブジェクトの階層があります。

ビジネスプロセスをこれらのオブジェクトにマッピングする方法を理解することは、WorkfrontとMarketo Engageの関係を理解するうえで重要です。

![](assets/overview-2.png)

### Portfolio階層の定義 {#portfolio-hierarchy-defined}

<table> 
  <tr> 
   <td><b>オブジェクト</b></td>
   <td><b>定義</b></td>
  </tr>
  <tr> 
   <td>Portfolio</td>
   <td>WorkfrontのPortfolioとプログラムを使用して、プロジェクトを整理できます。 プロジェクトの整理を通じて、類似のプロジェクトを比較し、リソースの最適な使用場所を決定できます。<br /><br />
   ( 例：Portfolioは、サービスや製品の販売に重点を置いた、会社内のビジネスユニット用に作成されます )。</td>
  </tr>
  <tr>
   <td>プログラム</td>
   <td>Workfrontプログラムを使用して、プロジェクトを整理できます。 プロジェクトの整理を通じて、類似のプロジェクトを比較し、リソースの最適な使用場所を決定できます。<br /><br />
   （例えば、新製品の発売に対する意識向上や需要の促進など、高レベルの目標を持つマーケティング戦略）。</td>
  </tr>
  <tr>
   <td>プロジェクト</td>
   <td>Workfrontプロジェクトは、特定の目標、成果物、製品などを達成するために完了する必要がある作業項目の集まりです。<br /><br />
   ( 例：E メールの一斉送信、育成キャンペーン、ウェビナー、対面イベントなどのマーケティング戦術。 また、E メール、ディスプレイ広告、ランディングページ、ダウンロード可能なホワイトペーパーなど、同じ結果をもたらす複数の戦術を含めることで、1 つのプロジェクトをより複雑にすることもできます )。</td>
  </tr>
  <tr>
   <td>タスク</td>
   <td>Workfrontタスクは、プロジェクトまたはイニシアチブの一部となる予定作業項目です。 タスクは、完了するためにユーザーまたはチームに割り当てられます。<br /><br />
   ( 例えば、オーディエンスセグメントを作成したり電子メールドラフトを作成したりするタスクは、Marketo Engage電子メールプログラムを開発するためにプロジェクトに関連付けられたタスクです )。</td>
  </tr>
  <tr>
   <td>問題</td>
   <td>問題は、Workfrontの予期しない作業項目です。 これは、プロジェクト中に発生する問題か、要求キューを介して送信される要求の可能性があります。<br /><br />
   （例：E メールバナーの画像のサイズが正しくないので、問題が発生します）。</td>
  </tr>
  <tr>
   <td>文書</td>
   <td>Word ドキュメントやプレゼンテーションなど、従来のドキュメントを使用できます。 また、画像ファイルにすることもできます。 Workfrontでは、ドキュメントや画像に対するコメントや注釈を使用してアセットを校正し、チーム間での共同作業を可能にします。<br /><br />
   （確認が必要な E メールヘッダー画像など）。</td>
  </tr>
  <tr>
   <td>更新</td>
   <td>Workfrontでの作業を追跡し、共同作業を容易にするコメントと監査ログが含まれます。<br /><br />
   （例：新しいイメージバージョンの監査ログ）。</td>
  </tr>
  </tbody>
</table>

## マーケティングイニシアチブの作業管理の例 {#marketing-initiative-work-management-example}

Workfrontのポートフォリオ階層が実際の例でどのように機能しているかを見てみましょう。

Zeplin 社は、Z11 と呼ばれるコンパクトなユーティリティトラクターの付属品の更新版をリリースしています。Z11 は、耐久性とカスタマイズ性を高めることで、以前の Z10 モデルを上回る性能を発揮します。 これにより、トラクター事業部門からの新規リリースに対する需要を高め、意識を高めるために、マーケティング戦略の策定、策定、策定、実行が必要となります。 このマーケティング戦略には、新しい顧客意識と既存の Z10 の顧客意識の両方を高めるために、異なるマーケティング戦略を含める必要があります。

以下の階層は、このマーケティングキャンペーンの戦略、戦術、タスクおよびアセットをWorkfrontにマッピングする方法を示しています。

![](assets/overview-3.png)

## WorkfrontとMarketoのマッピング {#mapping-workfront-to-marketo}

Workfrontをマーケティング計画やプロジェクト組織のアップストリームシステムとして使用する場合、Marketo EngageとWorkfront間で情報を共有する方法を理解することが重要です。

新しいマーケティング戦略の開発に合わせてこれらのシステムを連携させるには、Workfrontの様々なレコードタイプがMarketo Engageのレコードタイプにどのようにマッピングされているかを理解することが重要です。

### WorkfrontプロジェクトのMarketo Engageプログラムへのマッピング {#mapping-workfront-projects-to-marketo-engage-programs}

Workfront Fusion を統合レイヤーとして使用すると、WorkfrontのプロジェクトをMarketo Engageのプログラムにマッピングできます。 例えば、上記の場合、Zeplin は新しい Zeplin モデルに対する意識を高めたいと考えています。 これにより、Workfrontで新しいプログラムを作成し、プロジェクトとして表される複数のマーケティング戦術を格納します。 1 つの戦術は、Z10 モデルの既存のお客様に新しい Z11 モデルについて知らせる必要がある認識メールです。 Workfrontには、オーディエンスの作成、E メール画像のクリエイティブの取得、E メールのMarketo Engage化のための一連のタスクを含む、この E メール戦術を表す E メール戦術を作成するプロジェクトがあります。 WorkfrontのプロジェクトをMarketo Engageの電子メールプログラムにマッピングして、システム間で情報を同期できます。

以下に、プログラムが複数のプロジェクトを含める方法と、それらのWorkfrontプロジェクトをMarketo Engageのプログラムにマッピングする方法の例を示します。

![](assets/overview-4.png)

複数のWorkfront Projects をWorkfrontプログラムに格納する必要がある大規模なマーケティングイニシアチブを開始したり、1 つのWorkfront Project を作成するだけの必要がある Web セミナーや電子メールを 1 回限りリクエストしたりできます。 Workfront、Workfront Fusion、Marketo Engageなど、あらゆるニーズに応えて、チームは、キャンペーン開発プロセスを計画から実行に至るまでシームレスに統合できる柔軟性を備えています。

### Workfront Tasks とMarketo EngageAssets のマッピング {#mapping-workfront-tasks-to-marketo-engage-assets}

WorkfrontでキャンペーンMarketo Engageプロセスをマッピングし始める際に、開発で実行すべきタスクと、Workfrontでの情報の取得方法を考え、キャンペーン開発サプライチェーンの一貫性、効率性、正確性を高めることもできます。

Workfrontプロジェクトをテンプレート化して、特定のマーケティング戦術を実行するたびにプロセスを明確に定義できます。 例えば、E メールキャンペーンを実行する際には、組織に応じて完了する必要のある標準のタスクセットが存在します。 これらのタスクには、関係者とのキックオフミーティング、クリエイティブアセットの取得、クリエイティブの承認、ターゲットオーディエンスの構築、E メールの構築、E メールの翻訳、E メールの承認、E メールキャンペーンの結果の関係者との共有が含まれます。

これらのタスクの一部は、作業に直接マッピングし、Marketo Engageで実行できます。 例えば、Workfrontの E メールの作成タスクをカスタマイズして、Marketo Engageに情報を渡すフィールドを含め、E メールの組み立てを自動化できます。 件名、コピー、E メール内の画像などが含まれます。

## 次の手順 {#next-steps}

WorkfrontとMarketo Engageがキャンペーン開発サプライチェーンの新しい効率性を解き放つ方法を理解できたので、Workfront Fusion を使用してMarketo EngageとWorkfront間のワークフローとプロセスを自動化する方法に関する次のドキュメントとリソースを確認します。

### Workfront Fusion、Workfront、Marketo Engage統合の概要 {#getting-started-with-workfront-fusion}

* [取り込みと作成](/help/blueprints/optimize-campaign-supply-chain-with-marketo-and-workfront/intake-and-create.md){target=&quot;_blank&quot;} -Marketo EngageとWorkfrontを使用したキャンペーン開発の自動化

* 配達確認と承認（近日公開）

* レポートと監査（近日公開）

### Marketo Engageキャンペーン名と関連 URL の管理 {#managing-marketo-engage-campaign-names}

キャンペーンと URL の命名規則を標準化することは、Marketo Engageでの正確なプログラム管理の重要な基盤であり、キャンペーンサプライチェーン全体でより一貫したプロセスを推進するのに役立ちます。 これを支援するツールをお探しの場合は、以下の無料のオープンソースツールをご利用ください。 [Adobe成功サービス](https://main--marketo-campaign-tools--dr-adobe.hlx.live/){target=&quot;_blank&quot;}。Marketo Engageキャンペーンとそれに関連する URL を作成および管理するための一貫した手法を作成できます。

### リソース {#resources}

* [Workfront Fusion forMarketo Engage](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/marketo-modules.html){target=&quot;_blank&quot;}

* [Workfront Fusion for Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/workfront-modules.html){target=&quot;_blank&quot;}
