---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---
# ユースケースカタログ行テンプレート

## 行の形式

ユースケースカタログテーブルの各行の形式は、次のとおりです。

```
| <img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40"> | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

### アイコンのない行（アイコンがまだ使用できない場合に使用）

```
| | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

## フィールド参照

| フィールド | 書式設定 | 例 |
| --- | --- | --- |
| 業種 | kebab-case ディレクトリ名 | 小売、金融サービス、旅行ホスピタリティ |
| ケバブ名 | アイコンのケバブケースのユースケース名 | 放棄された買い物かご、リード育成 |
| 代替テキスト | タイトルケース、短 | 放棄された買い物かご、リード育成 |
| 見出しアンカー | 概要の##見出しのケバブケース | anoned-cart-email-recovery |
| 成熟度+ タイプ | バッジ構文 | `[!BADGE Foundational]{type=Neutral}`, `[!BADGE Emerging]{type=Informative}`, `[!BADGE Advanced]{type=Caution}` |

## カタログの「業界」タブマーカー

カタログ ファイルでは、次のタブ構造を使用します。

- `>[!TAB Retail]`
- `>[!TAB Automotive]`
- `>[!TAB Financial Services]`
- `>[!TAB Healthcare]`
- `>[!TAB Insurance]`
- `>[!TAB Media & Entertainment]`
- `>[!TAB Telecommunications]`
- `>[!TAB Travel & Hospitality]`
- `>[!TAB B2B]`

## タブ内の順序

行は成熟度レベルで並べ替えられます。

1. **基本** 行が最初（type=Neutral）
2. **新興行** 秒（type=Informative）
3. **詳細** 最後の行（type=注意）

同じ成熟度レベル内で、そのグループの最後に新しい行を追加します。
