---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---
# アーキテクチャ図ページテンプレート

これは、アーキテクチャ ダイアグラム ページの完全なマークダウン テンプレートです。 `{placeholder}`ごとに、スキルワークフローのフェーズ 1で収集された値に置き換えます。 適用されない任意のセクション（例：`>[!MORELIKETHIS]` ブロック）を削除します。生成されたファイルに空のプレースホルダーを残さないでください。

&#x200B;---

```markdown
---
title: {Page title}
description: {1-2 sentence page purpose, used for search snippets and previews}
solution: {Comma-separated Adobe solutions, e.g. Experience Platform, Journey Optimizer, Customer Journey Analytics}
---
# {Page title}

{Opening paragraph -- 1-2 sentences describing what the diagrams collectively illustrate. Frame the page as a top-level architecture reference, not a use case walkthrough.}

>[!MORELIKETHIS]
>
>[{Related-content link text}]({Related-content URL}).

## {Diagram 1 section title}

{1-2 sentence explanation of what the diagram shows and why it matters.}

<img src="assets/{filename-1}" alt="{Alt text for diagram 1}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## {Diagram 2 section title}

{1-2 sentence explanation.}

<img src="assets/{filename-2}" alt="{Alt text for diagram 2}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## Primary data flows and integration points

- {Flow or integration 1 -- e.g., "Real-time event ingestion from [!DNL Web SDK] to [!DNL Edge Network]"}
- {Flow or integration 2 -- e.g., "Profile sync between [!DNL Experience Platform] Hub and Edge"}
- {Flow or integration 3}
- {Flow or integration 4}
- {Flow or integration 5}

## Use case patterns supported

The architecture above supports the following use case patterns:

- [{Pattern 1 name}](/help/blueprints/use-case-patterns/{category}/{pattern-1-file}.md) -- {1-line note on why this architecture enables the pattern}
- [{Pattern 2 name}](/help/blueprints/use-case-patterns/{category}/{pattern-2-file}.md) -- {1-line note}
- [{Pattern 3 name}](/help/blueprints/use-case-patterns/{category}/{pattern-3-file}.md) -- {1-line note}

## Further reading

- [{Article 1 title}]({Experience League URL 1})
- [{Article 2 title}]({Experience League URL 2})
- [{Article 3 title}]({Experience League URL 3})
```

&#x200B;---

## Frontmatterのルール

- **必須フィールド：** `title`、`description`、`solution`。
- **禁止フィールド** （公開時に自動割り当て）: `exl-id`、`product_v2`、`feature_v2`、`role_v2`、`topic_v2`、`TQID`、`kt`、`thumbnail`。 新しく作成したファイルにこれらを含めないでください。

## 本文の規則

- **One H1** — ページタイトル。 `title`の前面部分を正確に一致させます。
- **図ごとに1つのH2。** 図のセクション内にH3を配置しない。1～2文のイントロと画像を配置します。
- **`<img>`埋め込み** — インラインスタイルと`class="modal-image"`が必要です。 Experience Leagueモーダルズーム操作を実行します。
- **画像パス** – 常に`assets/{filename}` （ページのトピックフォルダーに対して）。 絶対パスは使用しないでください。
- **Adobeの商品名** – 本文と箇条書きで`[!DNL ...]`を囲みます。 例：`[!DNL Real-Time CDP]`、`[!DNL Journey Optimizer]`、`[!DNL Experience Platform]`。
- **ユースケースパターンリンク** – 常に絶対`/help/blueprints/use-case-patterns/{category}/{file}.md`形式を使用して、このコンテンツをトランスクルージョンする可能性のあるページからリンクを解決します。
- **Experience League リンク** — `https://experienceleague.adobe.com/ja`で始まる絶対URL。 ローカライズされたバリエーションよりも、規範的なドキュメントのURLを優先する。

## セクションの順序

読者が予測可能にスキャンできるように、すべてのアーキテクチャページで順序の一貫性を保ちます。

1. Frontmatter
2. H1 +段落を開く
3. （オプション） `>[!MORELIKETHIS]` コールアウト
4. 図ごとに1つのH2 （ユーザー指定の順序）
5. `## Use case patterns supported`
6. `## Primary data flows and integration points`
7. `## Further reading`

## 期待する長さ

40～100行のマークダウンが一般的です。 ページが150行を超えた場合、コンテンツはユースケースパターンの領域にドリフトしている可能性があります（`scope-guardrails.md`を再確認し、分割を検討してください）。
