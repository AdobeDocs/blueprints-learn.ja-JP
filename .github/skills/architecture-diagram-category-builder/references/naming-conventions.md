---
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
# 命名規則：アーキテクチャ図とブループリント

このドキュメントは、`+ Architecture Diagrams and Blueprints{#architecture-diagrams}`の下のカテゴリの命名方法に関する信頼できる唯一の情報源です。 `architecture-diagram-category-builder` スキル （新しいカテゴリ）と`architecture-diagram-page-builder` スキル （既存のカテゴリ内の新しいページ）の両方は、これらのルールに従う必要があります。

## ルール

**フォルダー名=目次アンカースラグ =目次ラベル全体のケバブケース。** 3つの値は、省略形や切り捨てのない正確に一致する必要があります。

| 目次ラベル | アンカー | フォルダー |
| --- | --- | --- |
| アーキテクチャの概要 | `#architecture-overviews` | `architecture-overviews/` |
| オーディエンスとプロファイルのアクティベーション | `#audience-profile-activation` | `audience-profile-activation/` |
| B2B アクティベーション/マーケティング | `#b2b-activation-marketing` | `b2b-activation-marketing/` |
| 顧客インサイト | `#customer-insights` | `customer-insights/` |
| カスタマージャーニー | `#customer-journeys` | `customer-journeys/` |

これは、5つのカテゴリすべての現在の修正された状態です（2026-09-16時点）。 このリポジトリの履歴の前に、これらのいくつかは省略されました（`architecture-overview`, `audience-activation`, `b2b-activation`）。この不整合は修正されました。 新規または既存のカテゴリの省略形のフォルダー/アンカー名を再導入しないでください。

## なぜこれが重要なのか

- **予測可能性。** コントリビューター（人間またはエージェント）は、TOC.mdを開かずに、目次ラベルからフォルダーパスを推測できます。
- **安全な自動化。** ラベル（またはパスからのラベル）からパスを生成するスキルとスクリプトは、マッピングが正確で機械的な場合（kebab ケース、略語なし）にのみ確実に機能します。
- **ハイジーンをリダイレクトします。** 名前を変更するたびに、`redirects.csv`に新しいエントリが必要です。 名前を最初から安定して完全にわかりやすくしておくと、名前の変更を繰り返す必要がなくなります。

## ラベルからスラグを派生させる方法

1. ラベルを小文字にします。
2. `&`をすべてドロップし、周囲の単語をハイフンで結合します（例：`Audience & Profile Activation` -> `audience-profile-activation`）。
3. スペースをハイフンに置き換えます。
4. ハイフン以外の句読点を削除します。
5. ラベルから単語を省略化、切り捨て、削除しないでください（「B2B アクティベーションとマーケティング」の場合は`b2b-activation`ではなく、`b2b-activation-marketing`を使用）。

## カテゴリごとの必要なアセット

`help/blueprints/architecture-diagrams/`の直下にあるすべてのカテゴリ フォルダーには、次を含める必要があります。

1. **`overview.md`** — カテゴリのランディングページ。 必要な構造については、`./category-overview-template.md`を参照してください。 各カテゴリの概要ページは同じように見える必要があります。イントロ段落の後、カテゴリ内のすべてのページをリストする1つの`| Diagram | Description |` テーブル（目次の順）。 ネストされた`<ul><li>` セル、埋め込み図画像、または3番目の列は、既存の5つのカテゴリと完全に一致して使用しないでください。
2. **`assets/`** – 作成時に空のダイアグラム画像のフォルダー（最初のダイアグラムを追加したら作成）。

## TOC.mdの要件

- カテゴリの`+ [Overview](/help/blueprints/architecture-diagrams/{folder}/overview.md)` エントリは、コンテンツページの前に、常にカテゴリ見出しの下の&#x200B;**最初の** エントリです。
- カテゴリ見出しとそのアンカーは、他の5つのカテゴリと同じ2 スペースのインデントレベルで`+ Architecture Diagrams and Blueprints{#architecture-diagrams}`のすぐ下に配置されます。
- コンテンツページには4つのスペース（`+`の先頭に4つの先頭スペース）がインデントされます。 ネストされたサブグループ（オーディエンスとプロファイルアクティベーションの下のRTCDP グループなど）には、インデントが6つ付けられます。

## ランディングページの要件

`help/blueprints/architecture-diagrams/overview.md` （最上位のアーキテクチャ図およびブループリント ランディングページ）には、カテゴリごとに目次の順序で1枚のカードが必要です。 各カード：

- カテゴリの`overview.md`へのリンク （コンテンツページではありません）。
- そのカテゴリの`assets/` フォルダーの代表的な図形画像をサムネールとして使用し、標準カード CSS （`background-color:#ffffff; border:1px solid #d3d3d3;`+既にファイル内にある共有サイズ / パディング ルール）でスタイル設定します。
- カテゴリ名（太字/強）と、カテゴリ概要の概要に一致する1文の説明が含まれます。

カテゴリの数が3の倍数の場合、テーブルはクリーンな完全な行（セルごとに3列、`table-layout:fixed`、`width:33%`）としてレンダリングされます。 3の倍数でない場合は、最後の行の不足しているスロットごとに1つの空の`<td>`を追加します（テーブルのタグ付けやスタイル設定を解除しないでください）。
