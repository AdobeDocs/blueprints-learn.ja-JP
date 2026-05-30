---
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 48%

---
# ユースケースパターンテンプレート

このファイルには、ユースケースパターンページの完全なマークダウンテンプレートが含まれています。 新しいパタ `{{placeholder}}` ンを生成する際に、すべての値を実際のコンテンツに置き換えます。

&#x200B;---

## Template

````markdown
---
title: {{Pattern Title}}
description: {{One-sentence description of what this pattern teaches}}
solution: {{Comma-separated Adobe solutions}}
exl-id: {{generate-uuid-placeholder}}
---
# {{Pattern title}}

This guide provides an overview of {{pattern name}} using {{solutions with [!DNL ...] formatting}}. It is designed for solution architects, marketing technologists, and implementation engineers who need to {{primary capability description}}.

## Use case pattern

**{{Pattern Name}}**

{{One-two sentence description of what the pattern does and enables.}}

**Execution plan:** {{Step 1}} > {{Step 2}} > {{Step 3}} > {{Step 4}} > {{Step 5}}

## Use case overview

{{Paragraph 1: Define the pattern. What does it do? How does it differ from related patterns? Provide a clear, specific definition.}}

{{Paragraph 2: Describe the typical trigger or starting condition. When does this pattern apply? What event, schedule, or condition initiates it?}}

{{Paragraph 3: Describe what the pattern delivers. What is the end result for the customer or business? What channels or touchpoints does it affect?}}

{{Paragraph 4: Clarify scope boundaries. What does this pattern NOT cover? What adjacent patterns handle those needs? Reference other patterns by name if relevant.}}

{{Paragraph 5 (optional): Identify typical stakeholders and teams involved in implementation. Who owns what?}}

## Key business objectives

The following business objectives are supported by this use case pattern.

**[{{Objective Name}}](../../business-objectives/{{category}}/{{objective-file}}.md)**

{{Brief description of how this pattern supports the objective -- 1-2 sentences.}}

| KPIs |
| --- |
| {{KPI1}}, {{KPI2}}, {{KPI3}} |

{{Repeat the above block for each supported business objective.}}

## Example tactical use cases

The following scenarios illustrate how {{pattern name}} can be applied across different business contexts.

- **{{Scenario name}}** -- {{Description of the scenario and how it uses this pattern}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
{{Include 6-10 scenarios total}}

## Key performance indicators

| KPI | Description | Measurement |
| --- | --- | --- |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |

## Applications

The following Adobe applications are used in this use case pattern.

- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}

## Related documentation

The following resources provide additional detail on the capabilities used in this pattern. Group the reference links to primary Experience League documents under descriptive subheadings.

### {{Topic group}}

- [{{Link text}}]({{URL}})
- [{{Link text}}]({{URL}})

### {{Topic group}}

- [{{Link text}}]({{URL}})
- [{{Link text}}]({{URL}})
````

&#x200B;---

## このテンプレートの使用に関する注意事項

- **YAML frontmatter:** `exl-id` はプレースホルダーの UUID にする必要があります（例：`xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`）。 パブリッシングパイプラインが実際の値を割り当てます。
- **セクションの順序：** `Use case pattern` セクションは、`Use case overview`の前の最初の導入直後に表示されます。 明確な一行の定義と、上位レベルの実行計画を読者に提供します。
- **Adobe商品名：** 本文およびテーブルでは、Adobe商品名に常に `[!DNL ...]` の構文を使用してください（例：`[!DNL Journey Optimizer]`）。 これは、製品名の翻訳を防ぐExperience Leagueの規則です。
- **ビジネス目標のリンク：** パターンファイルからビジネス目標ディレクトリへの相対パスを使用します：`../../business-objectives/{{category}}/{{filename}}.md`。
- **Kebab-case ファイル名：** パターンファイル名は、パターンタイトルからケバブケースに変換する必要があります。 例：「イベントトリガーメッセージ」が `event-triggered-messaging.md` になります。
- **実行計画：** ステップ間の区切り文字として` > ` （スペース、大きい値、スペース）を使用します。 ラベルを正確に`**Execution plan:**`のままにします。
- **関連ドキュメント：**&#x200B;記述的な`###`見出しの下のグループ参照リンク（アプリケーションまたは機能領域など）。 これらは、パターンで使用されるアプリケーションと機能に関するExperience Leagueのリファレンスです。
- **アーキテクチャ （オプション）:** パターンが参照アーキテクチャ図から恩恵を受ける場合、オプションの`## Architecture` セクションを`Applications`から`Related documentation`の間に配置できます。
- **スコープ：**&#x200B;このテンプレートは、詳細な実装セクション（基礎/サポート/アプリケーション機能、前提条件、実装オプション、段階的な実装手順）を意図的に除外しています。 これらの詳細は、`Related documentation`からリンクされたExperience League ドキュメントにあります。