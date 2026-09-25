---
name: architecture-diagram-category-builder
description: Adobe Experience Platform ブループリントリポジトリの「アーキテクチャ図とブループリント」の下にある、まったく新しいトップレベルカテゴリ（サブセクション）の作成をガイドします。 このスキルは、提案されたアーキテクチャ図が既存のカテゴリー（アーキテクチャの概要、オーディエンスとプロファイルのアクティベーション、B2B アクティベーションとマーケティング、顧客インサイト、カスタマージャーニー）に適合せず、新しいアーキテクチャ図が必要な場合に使用します。 完全なワークフローを処理します。新しいカテゴリが実際に保証されていることを確認し、フォルダー/アンカーの命名規則を適用し、フォルダー構造とoverview.md ランディングページを作成し、TOC.md サブセクションを追加し、architecture-diagrams ランディングページグリッドを更新します。 *existing* カテゴリにページを追加するには、代わりにarchitecture-diagram-page-builderを使用します。
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%
---

# アーキテクチャ図カテゴリビルダー

このスキルは、`/help/blueprints/TOC.md`の`+ Architecture Diagrams and Blueprints{#architecture-diagrams}`の下に新しいトップレベルカテゴリを作成する際に役立ちます。 カテゴリーは、`customer-insights/`または`b2b-activation-marketing/`のようなフォルダーです。関連するアーキテクチャ図ページのグループで、独自の`overview.md` ランディングページと独自の目次サブセクションがあります。

**これはまれな操作です。** 今日は5つのカテゴリがあります。 6つ目のレポートを追加する際には、アーキテクチャコンテンツの新しい領域が既存の領域に当てはまらない場合にのみ行うべきであり、既存のカテゴリでページを整理する際のショートカットとして使うべきではありません。

## 開始する前に読む必要があります

- `./references/naming-conventions.md` — フォルダー/アンカー/ラベルの命名規則とその重要性。 この記事は、カテゴリの命名に関する信頼できる唯一の情報源です。
- `./references/category-overview-template.md` – 新しいカテゴリの`overview.md`に必要な正確な構造。
- まだスキム `../architecture-diagram-page-builder/SKILL.md`を行っていない場合は、カテゴリが存在すると、このスキルではなく、そのカテゴリ内の個々のページがそのスキルを使用して追加されます。

## フェーズ 1：新しいカテゴリーが実際に必要であることを確認する

他の作業を行う前に、既存の5つのカテゴリとその範囲をユーザーにリストアップします。

| カテゴリ | フォルダー | 範囲 |
| --- | --- | --- |
| アーキテクチャの概要 | `architecture-overviews/` | トップレベルのAdobe Experience Cloud/Experience Platformアーキテクチャ、ガードレール、デプロイメント SDK |
| オーディエンスとプロファイルのアクティベーション | `audience-profile-activation/` | Real-Time CDP、Audience Managerによるオーディエンス/プロファイルの構築とアクティベーション |
| B2B アクティベーション/マーケティング | `b2b-activation-marketing/` | アカウントベースのアクティベーション，購買グループジャーニー，Marketo/Workfront |
| 顧客インサイト | `customer-insights/` | Customer Journey Analyticsとその統合 |
| カスタマージャーニー | `customer-journeys/` | Journey Optimizer、意思決定管理、Campaign v7/v8 |

提案されたコンテンツがこれらのいずれにも適合しないことをユーザーに確認してもらいます。 それが近い場合（新しいB2B図、新しいパーソナライゼーション図など）、新しいカテゴリを作成する代わりに、既存のカテゴリの`architecture-diagram-page-builder`にリダイレクトします。 ユーザーが真に新しいカテゴリの保証を確認した場合にのみ、フェーズ 2に進みます。

## フェーズ 2：カテゴリ情報の収集

質問フォームを使用して、1回のラウンドで収集します。

1. **カテゴリーラベル** – 人間が読み取れる完全な目次ラベル（例：「Commerce Architecture」、略語ではない）。 2～3の提案されたフレーズと「その他」を提示します。
2. **1文の説明** – このカテゴリがカバーする、`overview.md`のフロントマターとランディングページのカード。
3. **Adobe ソリューション** — frontmatter `solution` フィールド用。
4. **最初のページ** – ユーザーは、既にこの1つ以上のページをこのカテゴリに配置する準備ができていますか。それとも、ページを後でフォローするためのカテゴリの基礎を構築しているだけですか？

`./references/naming-conventions.md`のスラグルールを使用して、カテゴリーラベルからフォルダー名とアンカーを派生させます（小文字、ドロップ `&`、ハイフネート、略語なし）。 ユーザーに派生フォルダー/アンカーを表示し、続行する前に確認します。これは、後で修正するためにコストがかかる詳細です。

## フェーズ 3: フォルダー構造を作成する

```
help/blueprints/architecture-diagrams/{new-folder}/
help/blueprints/architecture-diagrams/{new-folder}/assets/
help/blueprints/architecture-diagrams/{new-folder}/overview.md
```

`./references/category-overview-template.md`を使用して`overview.md`を生成します。 ユーザーが最初のページを作成できる場合は、今すぐテーブルにリストします（`architecture-diagram-page-builder`を使用してそれらのページファイル自体を生成します。このスキルでは、個々のダイアグラムページではなく、カテゴリの足場とその概要ページのみが作成されます）。 ページがまだ存在しない場合、最初のページが追加されるまで、テーブルは空または省略される可能性があります。プレースホルダー行を発明するのではなく、ユーザーにこの点を注意してください。

作成時に`assets/` フォルダーを空にできます。このフォルダーは存在するので、カテゴリに追加された最初のダイアグラム ページには、画像を配置する場所があります。

## フェーズ 4:TOC.md サブセクションを追加する

ユーザーが特に指定しない限り、新しいカテゴリを`+ Architecture Diagrams and Blueprints{#architecture-diagrams}`の下の最上位エントリとして挿入し、最後の既存のカテゴリの後に配置します。

```
  + {Category Label}{#{folder-slug}}
    + [Overview](/help/blueprints/architecture-diagrams/{new-folder}/overview.md)
    + [{Page title}](/help/blueprints/architecture-diagrams/{new-folder}/{filename}.md)
```

ルール：

- カテゴリ見出しの2 スペースインデントで、他の5つに一致します。
- アンカー`{#{folder-slug}}`は、フォルダー名と完全に同じである必要があります（naming-conventions.mdを参照）。
- `+ [Overview]`は、常にコンテンツページの前の最初のエントリで、4 スペースのインデントです。
- 他のすべてのTOC.md エントリの既存の順序とコンテンツを保持します。無関係なセクションのみを挿入、並べ替えまたは書き換えはありません。

## フェーズ 5：アーキテクチャ図とブループリントのランディングページを更新する

他の5枚のカードで使用されているのと同じ`<table style="table-layout:fixed; width:100%;">` グリッドで、`help/blueprints/architecture-diagrams/overview.md`に新しいカードを追加します。 新しいカード：

- `{new-folder}/overview.md`へのリンク。
- `{new-folder}/assets/`の代表的なダイアグラムのサムネールを使用します（ダイアグラムがまだ存在しない場合は中立的なプレースホルダーノートを使用します。画像パスを発明するのではなく、ユーザーにフラグを付けます）。
- 既存のカードとまったく同じインラインスタイルブロックを使用します（画像上では`width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;`、テキスト div上では`min-height:100px;`）。

**グリッドレイアウトを再計算します。** 既存の5枚のカードは、3列のグリッド（2行、末尾に1つの空のセル）を埋めます。 6枚目のカードを追加すると、その空のセルが正確に埋まります。レイアウトの変更は必要ありません。 これが7番目、8番目などカテゴリの場合は、新しいカードで新しい`<tr>`を追加し、その行の残りの空のセルを空白の`<td style="width:33%; ...;"></td>`要素で埋めて、行がラグ付きにならないようにします。

## フェーズ 6：検証

確認してユーザーに報告：

1. **命名規則** — フォルダー名、目次アンカー、カテゴリーラベルのスラグが同じです（命名規則.mdごとに）。
2. **overview.md構造** — `category-overview-template.md`に一致します（イントロ + 2列`Diagram | Description` テーブル、テーブルに埋め込まれた画像またはネストされたリストがありません）。
3. **TOC.md placement** – 新しいサブセクションがアーキテクチャ図とブループリントの下にあり、`+ [Overview]`が最初で、インデントが正しく、他のエントリは変更されませんでした。
4. **ランディングページカード** – 正しいグリッド位置に追加され、標準のカードのスタイル設定が使用され、新しい`overview.md`へのリンクが表示されます。
5. **リダイレクト** – このカテゴリが、以前に他の場所に存在していたコンテンツを統合または名前変更する場合（真新しいカテゴリではまれですが、チェックする場合）、以前のアーキテクチャ図の名前変更に使用されていた既存の`source,dest`形式に従って`redirects.csv`にエントリを追加します。

タスクの完了を検討する前に、検証の問題を修正します。

## 備考

- 後でユーザーがカテゴリ（ラベル、フォルダー、アンカー）の名前を変更する場合、それは名前変更操作であり、新しいカテゴリ操作ではありません。新しい名前のnaming-conventions.md ルールに従い、すべての内部リンク（TOC.md、両方の概要ページ、兄弟リンク、スキルドキュメント）を更新し、リダイレクトエントリを追加します。 このリポジトリで以前にカテゴリ名の変更が処理されているのと同じように処理します。フォルダー`git mv`。その後、リポジトリ全体で古いパスフォームの検索と置換を行い、関連のない外部URLと競合する可能性のあるブラインドグローバル文字列の置換は行いません（例：`experienceleague.adobe.com/docs/experience-platform/...`製品ドキュメントリンク）。
- このスキルと`architecture-diagram-page-builder`を同期しておきます。`architecture-diagram-page-builder`の`references/toc-placement.md`のサブセクションマッピングテーブルがまだ新しいカテゴリをリストしていない場合は、そこに追加します。
