---
source-git-commit: e0ecfa4d74b8fcc0bbaf35d44c33c725a1b1a539
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---
# カテゴリの概要.md テンプレート

`help/blueprints/architecture-diagrams/`の下のすべてのカテゴリーフォルダーには、他の5つのフォルダーと同じように`overview.md`が必要です。 この正確な構造を使用します。

## Frontmatter

```yaml
---
title: {Category Label}
description: {One-sentence summary of what this category covers.}
solution: {Primary Adobe solution(s), comma-separated}
doc-type: overview-page
---
```

新しいページに`exl-id`、`product_v2`、`feature_v2`、`role_v2`、`topic_v2`、`TQID`、`kt`または`thumbnail`を含めないでください。公開パイプラインはこれらのページに自動入力します。

## 本文

```markdown
# {Category Label}

{1-3 paragraph intro describing what this category of diagrams covers and why it matters.}

| Diagram | Description |
| --- | --- |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
```

ルール：

- カテゴリ内のすべてのページを、TOC.mdと同じ順序で一覧表示します。
- リンクのターゲットは相対ファイル名です（プレフィックス `/help/blueprints/...`は存在しません）。概要は兄弟ページと一緒に存在します。
- 説明は1文で、ラベルのように読む場合は末尾の期間は必要ありません。
- カテゴリーに自然なサブグループが含まれる場合（例：カスタマージャーニーの下の「非推奨の図」）、同じ形式で`## {Sub-group name}`見出しとその後の独自の2列テーブルを追加します。図のサムネールや追加の列をテーブルに混在させないでください。
- このテーブルに`<img>`図のサムネールを埋め込まないでください。 2つの列（`Diagram` （リンク）と`Description` （テキスト）に保存します。 サムネールは、カテゴリの概要ではなく、個々のコンテンツページに属します。
- テーブル セル内でネストされた`<ul><li>` HTMLを使用しないでください。 プレーンテキストのみ。

## 例（顧客インサイト）

```markdown
---
title: Customer Insights
description: Unify and analyze data and customer behaviors from across the customer journey
solution: Customer Journey Analytics
doc-type: overview-page
---
# Customer Insights

Customer Journey Analytics shows how brands can unify customer data and behavior from various interaction channels and sources to create a journey-based view of all customer interactions.

| Diagram | Description |
| --- | --- |
| [Adobe Customer Journey Analytics](cja.md) | Core Customer Journey Analytics architecture, including B2B and audience-sharing derivations |
| [Adobe Customer Journey Analytics & Adobe Journey Optimizer integration](cja-ajo-integration.md) | Campaign and journey insights integration between Customer Journey Analytics and Journey Optimizer |
```
