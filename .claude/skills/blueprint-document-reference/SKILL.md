---
name: blueprint-document-reference
description: Adobe Digital Experience Blueprint ドキュメントの作成と編集に関するリファレンス。 新しいブループリントを作成する場合、ブループリントページを追加する場合、またはユーザーがブループリントの構造、セクション、テンプレート、またはAdobe Experience Leagueの参照について尋ねる場合に使用します。
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# ブループリントドキュメント参照

このスキルは、このリポジトリでブループリントドキュメントを作成または編集する際に使用します。 ブループリントとは、確立されたビジネス上の課題に対処し、アーキテクチャ図、技術的な考慮事項、Adobe Experience Leagueの関連ドキュメントへのリンクを含む、繰り返し可能な実装のことです。

## 適用するタイミング

- 新しいブループリントドキュメントまたはブループリントの概要ページの作成
- 既存のブループリントでのセクションの追加または再構築
- Adobe Experience League ドキュメントへのリンクまたは引用
- 新しいコンテンツとブループリントの表記法（前頭部分、見出し、図）の整合

## クイックリファレンス

1. **ドキュメントの目的**: ブループリントは、Adobe Experience Platformとアプリケーションがどのように統合されているかを示すシステムとデータフローのアーキテクチャを提供します。 マーケティングではなく、ビジュアルとテクニカルです。
2. **セクション**: テンプレートの標準セクションを使用します。該当しない場合のみ省略します（[reference.md](reference.md)を参照）。
3. **Experience League**：製品ドキュメント、API、ガードレール、チュートリアルには、Experience Leagueへのリンクを使用します。 完全なURLを使用します。URL パターンと形式については、[reference.md](reference.md)を参照してください。
4. **リポジトリ構造**: ブループリントは`help/blueprints/`の下にあります。 ブループリントページの追加または移動時に`help/blueprints/TOC.md`を更新します。

## ドキュメントテンプレート

あらゆるブループリントページは、この構造に従う必要があります。 適用されるセクションのみを含めます。

```markdown
---
title: [Short descriptive title]
description: "[One sentence: what this blueprint shows and why it matters.]"
solution: [Product name, e.g. Real-Time Customer Data Platform, Journey Optimizer]
exl-id: [UUID - if this is already popultated keep it as is. Disregard and remove this field if it is a new blueprint as blank values will be rejected by the publishing flow. If the field and value are not present, it will be auto-generated as part of the Experience League publishing flow]
---
# [H1 - same as title or expanded]

[1–3 paragraphs: what the blueprint covers, key capabilities, and who it’s for.]

## Applications

* [Product 1]
* [Product 2]

## Use cases

* [Use case 1]
* [Use case 2]

## Prerequisites

[Bullets or short paragraphs: required products, config, or setup.]

## Architecture Diagram

<img src="[path to SVG/image]" alt="[Descriptive alt]" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Guardrails

[Link to Experience League guardrails and any blueprint-specific limits.]

## Implementation patterns

[Optional: named patterns with bullets.]

## Implementation steps

1. [Step with link to Experience League where relevant]
2. ...

## Implementation considerations

[Optional: identity, performance, security, etc.]

## Related documentation

[Grouped links to Experience League: product docs, APIs, tutorials.]
```

概要ページまたはハブページの場合は、短い構造（紹介、ユースケース（またはタブ）、アーキテクチャ画像、シナリオ/パターンテーブル、前提条件、ガードレール、関連ドキュメント）を使用します。 例については、`help/blueprints/`の既存の概要を参照してください。

## Frontmatter

| フィールド | 必須 | 備考 |
|-------|----------|--------|
| `title` | はい | 短い。Adobe スタイルごとに`[!DNL Product Name]`を使用します |
| `description` | はい | 1文；検索とカードで使用 |
| `solution` | はい | プライマリ製品（例：Real-Time Customer Data Platform、Journey Optimizer） |
| `exl-id` | はい | UUID。新しいページの場合は空白のままにします |
| `doc-type` | 概要の場合 | メイン ブループリントの概要ページに`overview-page`を使用 |
| `kt` | オプション | リンクされている場合のナレッジベース記事ID |

## Adobe Experience Leagueの参照

- **リンクするタイミング**：製品ドキュメント、API リファレンス、ガードレール、チュートリアル、設定手順については、Experience Leagueにリンクします。 長い手順を複製しないでください。要約してリンクします。
- **URL形式**：完全なURLを使用します。 `https://experienceleague.adobe.com/docs/?lang=ja...`または`https://experienceleague.adobe.com/ja/docs/...`を優先します。 開発者ドキュメントの場合、`https://developer.adobe.com/...`も有効です。
- **リンクテキスト**：説明テキストを使用します（例：「[ スキーマを作成] (url)」は「ここをクリック」ではありません）。 リンクテキスト内の製品名には、適切な場合は`[!DNL Product Name]`を使用します。
- **関連ドキュメントのセクション**: 「関連ドキュメント」セクションでブループリントを終了し、リンクをカテゴリ別にグループ化します（例：配信先の設定、SDK ドキュメント、プロファイルとセグメント化、チュートリアル）。

URL パターン、リンクのグループ化、および例の詳細については、[reference.md](reference.md)を参照してください。

## 送信前のチェックリスト

- [ ] Frontmatterには`title`、`description`、`solution`、`exl-id`があります
- [ ] H1がタイトルに一致するか、適切に拡張します
- [ ]個のアーキテクチャ図が存在し、代替テキストが記述されています
- [ ]実装ステップは、手順が公開されているExperience Leagueにリンクしています
- [ Experience Leagueの公式ガードレール ドキュメントへの] ガードレール セクション リンク
- [ ]関連ドキュメント セクションには、関連するExperience League リンクが含まれています
- [ ]新しいページまたは移動されたページが`help/blueprints/TOC.md`に反映されます

## その他のリソース

- 完全なテンプレートとセクションのメモ：[reference.md](reference.md)
- 既存のブループリント：`help/blueprints/` （例：`audience-activation/real-time-lookup.md`、`customer-journeys/journey-optimizer/journey-optimizer-overview.md`）
- 目次とナビゲーション：`help/blueprints/TOC.md`
