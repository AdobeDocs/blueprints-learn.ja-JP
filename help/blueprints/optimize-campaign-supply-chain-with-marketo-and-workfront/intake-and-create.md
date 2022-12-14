---
description: 取り込みと作成 — MarketoとWorkfrontを使用した Campaign サプライチェーンの最適化
title: 取り込みと作成
source-git-commit: fd8dd3caee5cbf450c5f00266c74ccdef7cd1de9
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# 取り込みと作成 {#intake-and-create}

マーケティングオペレーションチームに新しいキャンペーンを立ち上げるマーケティングリクエストの数は、高機能なチームを繰り返しタスクの根本的な扉に変え、燃え尽き、イノベーションを停滞させることができます。

キャンペーンリクエストを送信するプロセスを確立し、一般にリクエストされるマーケティングキャンペーンの作成を自動化することで、次のことが可能になります。キャンペーンの速度を上げ、エラーを減らし、リクエストをマーケティング操作の適切なメンバーにルーティングし、リソース使用率を調整して改善し、マーケティング操作のより多くをより戦略的なタスクに集中させます。

WorkfrontとMarketo Engageを使用すると、システム間接続で [Workfrontリクエストフォーム](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/customize/custom-forms/create-or-edit-a-custom-form.html){target=&quot;_blank&quot;}:Marketo Engageプログラムを作成し、次のようなキー変数を入力します。件名、E メールコピー、画像、日付、時間、イベント情報など。

この統合を実現するには、Workfront Fusion を使用します。これは、Workfrontと他のシステムとの間のワークフローを自動化できる作業自動化レイヤーです。

以下のワークフローは、キャンペーンマネージャーがWorkfrontリクエストフォームを使用して行う、ウェビナーに対するリクエストを示しています。 リクエストで送信された詳細は、その後、ウェビナーのMarketo Engageで作成されるプログラムと電子メールをトリガーします。 さらに、電子メールのコンテンツを入力するための詳細がリクエストフォームから取得されます。

![](assets/intake-and-create-1.png)

>[!TIP]
>
>マーケティングキャンペーンの作業の整理に使用されるWorkfrontの様々なタイプのオブジェクトと、Marketo Engageプログラムへのマッピング方法について詳しくは、 [MarketoとWorkfrontの概要](/help/blueprints/optimize-campaign-supply-chain-with-marketo-and-workfront/overview.md){target=&quot;_blank&quot;}。

## 自動化のためのキャンペーン開発プロセスの準備 {#prepare-your-campaign-development-process-for-automation}

すべての優れたワークフロー自動化の背後には、チームや関係者が自動化から最大限の価値を引き出していることを保証する、定義済みのプロセスがあります。

**受け取るマーケティングリクエストのタイプは何ですか？**

E メール、育成、ファーストパーティのウェビナー、イベントなど、実行するマーケティング戦術のタイプについて考えてみましょう。 また、サードパーティのウェビナーやディスプレイ広告も実行していますか。 これらのリクエストは、リクエストフォームに特定の入力フィールドが必要な場合があるので、各リクエストを考慮する必要があります。また、複製されるMarketo Engage内の異なるプログラムテンプレートにマッピングされます。

また、複数の地域でキャンペーンを実行している場合も把握したいと思います。 その場合は、Workfrontで 1 つのプロジェクトを使用し、Marketo Engageで複数のプログラムを作成し、各プログラムが異なる言語サポートを表すようにします。

リクエストを自動化して容易におこなうために、どのようなマーケティングリクエストを受け取るのかを事前に知っておくことが重要です。

**キャンペーンリクエストで取り込む必要がある情報は何ですか？**

実行する様々な戦術ごとに、リクエストフォームに取り込む必要がある主要な情報について考えてみましょう。 以下に、Workfrontフォームに取り込んで、キャンペーンの開発を自動化する方法を示します。

<table> 
  <tr> 
   <td><b>マーケティング戦術</b></td>
   <td><b>取得する情報</b></td>
  </tr>
  <tr> 
   <td>メール一斉送信</td>
   <td>・メールの件名<br />
・予定日<br />
・メールコピー<br />
・コールトゥアクション<br />
・画像 — AEM Assetsの URL を直接参照してMarketoで使用<br />
・オーディエンス認定条件</td>
  </tr>
  <tr>
   <td>ウェビナー/イベント</td>
   <td>・イベント名<br />
・イベント日<br />
・イベント時刻<br />
・イベントの都市<br />
・イベントの説明<br />
・ウェビナー録画ページ — PageURL OnDemand<br />
・スピーカー名<br />
・スピーカータイトル<br />
・スピーカー画像<br />
・必要なメール（招待、確認、リマインダー、フォローアップ）<br />
・メールヘッダーの画像<br />
・オーディエンス認定条件</td>
  </tr>
  <tr>
   <td>育成</td>
   <td>・メール数<br />
・メールコピー<br />
・メールヘッダー<br />
・コールトゥアクション<br />
・オーディエンス認定条件</td>
  </tr>
  </tbody>
</table>

>[!NOTE]
>
>現在、トークンはスマートリストではサポートされていないので、自動化によるプログラムによるオーディエンスの構築はMarketo Engageに制限があります。 つまり、オーディエンスは、ユーザーがMarketo Engageして作成する必要があります。また、継続的に通信する事前に定義されたオーディエンスがある場合は、自動化プロセス中に複製されたプログラムテンプレートの一部に設定済みのスマートリストを含めます。

### 優れたセンターを確立 {#establish-your-center-of-excellence}

プログラムの作成を自動化する場合は、優れたMarketo Engageの中心が必要です。 卓越性の中心には、テンプレート化されたプログラムとアセットが含まれ、キャンペーン開発プロセスを迅速に、標準化します。 例えば、様々なキャンペーンニーズに対応したプログラムテンプレートを用意できます。メール、育成、対面イベント、ウェビナー。 さらに、異なる地域や異なる種類のメールのお知らせに使用する複数のメールプログラムテンプレートが存在する場合もあります。

Marketo Engageのプログラムテンプレートを使用して優れたセンターを構築することは、キャンペーンの実行に対してよりプログラム的なアプローチを取る最初のステップの 1 つで、キャンペーンリクエストを自動化する基盤の役割を果たします。

再利用可能なプログラムテンプレートのセットを用意したら、このブループリントで概要を説明する自動化を使用して、キャンペーン開発の速度を向上させ、作業をさらに拡大できます。

独自の優れた中心を作成する方法について詳しくは、 [Marketo Community](https://nation.marketo.com/t5/product-blogs/marketo-master-class-center-of-excellence-with-chelsea-kiko/ba-p/243221){target=&quot;_blank&quot;} のベストプラクティスを参照してください。

### トークンを使用したコンテンツの入力 {#use-tokens-to-populate-content}

Marketo Engageでは、トークンを使用してキャンペーンアセットにコンテンツを入力できます。 例えば、優れたセンターから電子メールテンプレートを複製した後、Workfront Fusion はWorkfrontのキャンペーンリクエストから詳細を取得し、Marketo Engageプログラムのマイトークンに渡すことができます。 その後、トークンの値を電子メールに直接継承して、電子メールを構築できます。

![](assets/intake-and-create-2.png)

### AEM Assetsからの画像の入力 {#populate-images-from-aem-assets}

Marketo EngageトークンとAEM Assets内のアセットへのリンクを組み合わせて使用することで、電子メールとランディングページの開発をさらに自動化できます。 キャンペーンリクエスト担当者は、リクエストプロセスの一環として、AEM Assetsから公開済みの画像リンクを送信できます。 その後、Workfront Fusion は、これらのリンクを取得し、Marketo Engageトークンを使用して電子メールのHTMLに埋め込むことができます。

Fusion がWorkfrontで送信した情報でトークンの値を更新できるように、マイトークンを利用するには、プログラムとプログラムテンプレートをMarketo Engageに構築する必要があります。

>[!NOTE]
>
>AEM Assetsは、このワークフローをサポートする必要はありませんが、campaign 開発サプライチェーン全体で campaign アセットを管理するための、より効率的なプロセスを可能にします。

### すべてのプログラムリクエストタイプのルックアップライブラリのアセンブリ {#assemble-a-lookup-library-for-all-program-request-types}

Workfrontリクエストから新しいMarketo Engageプログラムの作成を自動化する場合は、Workfrontリクエストから情報を取得し、Marketo Engageでクローンする必要のある適切なプログラムテンプレートを参照できる手順をWorkfront Fusion 自動化に含めることが重要です。

これをおこなうには、優れたMarketo Engageセンターにあるすべての様々なプログラムテンプレートのリストを含むデータセットをWorkfront Fusion にインポートします。

プログラムテンプレート参照ライブラリに含める基本情報は、次のとおりです。

<table> 
  <tr> 
   <td><b>列</b></td>
   <td><b>説明</b></td>
  </tr>
  <tr> 
   <td>キャンペーンタイプ</td>
   <td>電子メール、ウェビナー、育成、イベント、サードパーティのウェビナー、リストのインポートなどが該当します。キャンペーンのタイプは、リクエストされる内容を読み取り可能に説明します。</td>
  </tr>
  <tr> 
   <td>Workfront Request Type</td>
   <td>これは、Workfrontフォームで選択されるリクエストタイプです。これは、E メール、ウェビナー、育成、イベントなど、キャンペーンのタイプと同じである可能性があります。 これは、Workfrontフォームで選択した入力を、Marketoのプログラムテンプレートにマッピングするために使用します。</td>
  </tr>
  <tr> 
   <td>Workfront Form ID</td>
   <td>書き込み要求がMarketo Engageプログラムテンプレートにマッピングされていることを検証するために使用される、Workfront要求フォームの一意の ID です。</td>
  </tr>
  <tr> 
   <td>Marketo Program ID</td>
   <td>これは、実行中のリクエストにマッピングされるMarketo Engage内のプログラムテンプレートの ID です。 この情報をWorkfront Fusion ですぐに入手できるので、Fusion はMarketo Engageにリクエストを送信し、どのプログラムを複製するかを正確に把握できます。</td>
  </tr>
  </tbody>
</table>

## インテークと自動化フローの作成 {#intake-and-create-automation-flow}

次に、事前ビルドを使用して Fusion でワークフローロジックを組み立てる方法の例を示します [Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/workfront-modules.html){target=&quot;_blank&quot;} および [Marketo Engage](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/marketo-modules.html)自動処理を迅速に実行できる {target=&quot;_blank&quot;} モジュール。

![](assets/intake-and-create-3.png)

## リソース {#resources}

* [Adobe Marketo Engageモジュール](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/marketo-modules.html){target=&quot;_blank&quot;}

* [Adobe Workfrontモジュール](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/fusion-apps-and-modules/workfront-modules.html){target=&quot;_blank&quot;}

* [MarketoとWorkfrontの概要](/help/blueprints/optimize-campaign-supply-chain-with-marketo-and-workfront/overview.md){target=&quot;_blank&quot;}
