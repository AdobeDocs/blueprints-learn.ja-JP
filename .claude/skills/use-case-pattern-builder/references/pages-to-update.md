---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---
# ユースケースパターン追加時に更新するページ

新しいユースケースパターンを作成したら、パターンを検出でき、正しくリンクされるように、次のページを更新する必要があります。

## 必要な更新

### 1. TOC.md
- **ファイル：** `/help/blueprints/TOC.md`
- **アクション：** 正しいカテゴリセクションに新しいエントリを追加します
- **形式：** `    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)`
- **カテゴリー別所在地：**
   - オーディエンスの作成とアクティベーション：47 行目まで後（そのセクションの既存のエントリの後）
   - Personalization：行の後～52
   - キャンペーン管理とオーケストレーション：ライン後～58 行目
   - 分析：行の後～61
   - 会話経験：63 行目より後

#### カテゴリと目次のマッピング

| カテゴリ見出し | 目次セクションの見出し | アンカー |
| --- | --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation` | `{#audience-building-activation}` |
| `personalization` | `+ Personalization` | `{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration` | `{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis` | `{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience` | `{#conversational-experience-patterns}` |

#### インデントルール

- カテゴリ見出しには、2 つのスペースと `+` を使用します（例：`  + Personalization{#personalization-patterns}`）
- パターンエントリには、4 つのスペース + `+` を使用します（例：`    + [Pattern Title](path)`）

### &#x200B;2. ユースケースパターンの概要
- **ファイル：** `/help/blueprints/use-case-patterns/overview.md`
- **アクション：** 新しい行を正しいカテゴリ テーブルに追加します
- **形式：** `| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |`
- **概要のカテゴリ：**
   - オーディエンスの構築とアクティブ化（18 行目）
   - Personalization（29 行目）
   - キャンペーンの管理とオーケストレーション（40 行以下）
   - 解析（52 行目）
   - 会話経験（61 行目）

#### 行形式の例

```
| [Event-Triggered Messaging](campaign-management-orchestration/event-triggered-messaging.md) | Listen for a real-time behavioral or system event, then deliver a contextual message to the triggering profile | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
```

## 検証チェックリスト

- [ 正 ] いカテゴリディレクトリに作成されたパターンマークダウンファイル
- [ ] Frontmatter には、タイトル、説明、ソリューション、exl-id が含まれます
- [ 正 ] いカテゴリに TOC.md エントリが追加されました
- [ Overview.md テーブル行 ] 正しいカテゴリに追加されました
- [ ] すべてのビジネス目標のリンクが既存のファイルを指している
- [ ] ファイルでは kebab-case 命名規則を使用します
- [ ] すべてのExperience League リンクは有効な URL です
- [ Adobeの製品名 ] は `[!DNL ...]` 構文を使用します
- [ 関数チェーン ] 区切り記号 ` > ` 使用します
- [ パターンファイル ]、必要なすべてのセクションが含まれています（pattern-template.md を参照）。
