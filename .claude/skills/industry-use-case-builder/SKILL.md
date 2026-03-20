---
name: industry-use-case-builder
description: Adobe Experience Platform ブループリントリポジトリに関する新しい業界のユースケースの作成ガイドです。 業界の業種（小売、自動車、ヘルスケア、金融サービス、保険、メディアとエンターテイメント、通信、旅行とホスピタリティ、B2B）に新しいユースケースを追加する場合、ユーザーが業界ページにビジネスシナリオを追加する場合、またはユースケースカタログを更新する場合は、このスキルを使用します。 完全なワークフローを処理：ユースケースの詳細の収集、成熟度レベルの評価、コンテンツの生成、業界の概要ページとユースケースカタログの更新、アイコン作成のユースケース – icon-generator スキルの呼び出しを行います。
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---


# 業界のユースケースビルダー

このスキルでは、Adobe Experience Platform ブループリントリポジトリの新しい業界ユースケースの作成について説明します。 各段階を順番に進めます。 開始する前に、参照ファイルを読み取ってください。

- `references/use-case-template.md` - ユースケースセクションの正確なテンプレート
- `references/catalog-row-template.md` - カタログテーブルの行の正確な形式
- `references/maturity-criteria.md` – 成熟度評価の詳細なルーブリック

## フェーズ 1：情報収集

コンテンツを生成する前に、ユーザーにインタビューして、必要な詳細をすべて収集します。

### 必須フィールド

1. **業種** – 次のいずれかである必要があります。
   - 自動車
   - b2b
   - 金融サービス
   - ヘルスケア
   - 保険
   - メディア・エンターテインメント
   - 小売
   - 通信
   - 旅行ホスピタリティ

2. **ユースケース名** – わかりやすいタイトル（「放棄された買い物かごのメール回復」、「薬の服従キャンペーン」など）。

3. **説明** - ビジネスシナリオと重要な理由を説明する 1～2 文です。

4. **ビジネスへの影響** – 特定の指標を使用して結果を数値化（「クリックスルー率が 20～30% 向上」、「リフィル率が 15～25% 向上」など）。

5. **ユースケースパターン** – 次の既存のパターンの 1 つに正確にマッピングする必要があります。
   - Audience Activationから宛先へ
   - Segment Match を使用した Audience Collaboration
   - イベント転送
   - B2B Audience Activation
   - 匿名訪問者の Web Personalization
   - 既知の訪問者の Web/アプリPersonalization
   - Offer Decisioning
   - 行動の推奨事項
   - バッチ送信メッセージの有効化
   - イベントトリガーメッセージ
   - 複数ステップの調整されたジャーニー
   - Decisioning を使用したクロスチャネルジャーニー
   - 購買グループベースのマーケティングおよびジャーニー管理
   - Customer Analytics &amp; Insightの生成
   - B2B 分析
   - Brand Concierge会話体験

6. **技術的な考慮事項** - データ要件、統合、規制/コンプライアンスのニーズ、パフォーマンスに関する考慮事項、アーキテクチャに関する注意事項を 4～8 項目の要点で説明します。

続行する前に、不足しているフィールドがないかどうかを確認します。 詳細を想定したり捏造したりしないでください。

## フェーズ 2：成熟度評価

完全なルーブリックについては、`references/maturity-criteria.md` を参照してください。 次の 3 つの成熟度レベルのいずれかを割り当てます。

- **基本** `[!BADGE Foundational]{type=Neutral}` – 単一ステップまたはイベントトリガーパターン（イベントトリガーメッセージング、バッチアウトバウンド）、わかりやすいデータ要件、最小限の AI/ML、標準統合。
- **新たな** `[!BADGE Emerging]{type=Informative}` – 複数ステップのジャーニー、行動データ、レコメンデーションモデル、既知の訪問者パーソナライゼーション、適度な統合の複雑さ。
- **詳細** `[!BADGE Advanced]{type=Caution}` — クロスチャネル判定、AI を利用した予測、Offer Decisioning、複雑なオーケストレーション、複数のシステム統合。

### 評価ワークフロー

1. ユースケースがマッピングされるユースケースパターンを識別します。
2. クイックマッチの成熟度条件の「典型的なパターン」リストを確認します。
3. パターンが成熟度を明確に示さない場合は、データの複雑さ、AI/ML 要件および統合の範囲を評価します。
4. 「パターンマッピング（{pattern}）と {key factors} に基づいて、{reasoning} の理由で {level} と分類します。」という理由を付けて、評価をユーザーに提示します。
5. ユーザーが確認または上書きするのを待ってから、コンテンツの生成に進みます。

## フェーズ 3：コンテンツの生成

2 つのファイルのコンテンツを生成または更新します。

### A.業界概要ファイル

**ファイル パス：** `/help/blueprints/industry-use-cases/{industry}/{industry}-overview.md`

最初に既存のファイルを読んで、現在の構造とコンテンツを理解します。 次に、`references/use-case-template.md` の正確なテンプレートに従って、新しいセクションを追加します。

```markdown
## {Use Case Title}

{1-2 sentence description of the business scenario and why it matters}

### Business impact

{Quantified business outcomes, e.g., "Retailers typically see a 20-30% increase in click-through rates..."}

### How to implement

Use the [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) pattern. {1-2 sentence explanation of why this pattern applies}

### Technical considerations

- {4-8 bullet points covering data integration, regulatory, performance, or architectural considerations}
```

一貫した形式を維持して、既存のユースケースのセクションの後に新しいセクションを配置します。

### B. ユースケースカタログ

**ファイル パス：** `/help/blueprints/industry-use-cases/use-case-catalog.md`

最初に既存のカタログ ファイルを読み込みます。 新しい行を正しい「業界」タブに追加します。 カタログでは、`>[!TAB {Industry}]` のマーカーを持つタブ付きの構造を使用しています。 各タブには、次の列を含むテーブルが表示されます。

| 列 | コンテンツ |
| --- | --- |
| アイコン | `<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">` （アイコンがまだない場合は空のままにします） |
| ユースケース | アンカーがケバブケースの見出しである場合の `[{Use Case Title}]({industry}/{industry}-overview.md#{anchor})` |
| 説明 | 1 文の概要 |
| 成熟度 | 割り当てられたレベルのバッジ構文 |
| パターン | `[{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md)` |

**プレースメントルール：** 各業界タブ内で、行は成熟度に基づいて、基礎的、新興、詳細の順にグループ化されます。 新しい行を適切な成熟度グループの最後に配置します。

パターンファイルのパスは次のとおりです。
- `audience-building-activation/audience-activation-to-destinations.md`
- `audience-building-activation/audience-collaboration-segment-match.md`
- `audience-building-activation/event-forwarding.md`
- `audience-building-activation/b2b-audience-activation.md`
- `personalization/anonymous-visitor-web-personalization.md`
- `personalization/known-visitor-web-app-personalization.md`
- `personalization/offer-decisioning.md`
- `personalization/behavioral-recommendation.md`
- `campaign-management-orchestration/batch-outbound-message-activation.md`
- `campaign-management-orchestration/event-triggered-messaging.md`
- `campaign-management-orchestration/multi-step-orchestrated-journey.md`
- `campaign-management-orchestration/cross-channel-journey-with-decisioning.md`
- `campaign-management-orchestration/buying-group-based-marketing.md`
- `analysis/customer-analytics-insight-generation.md`
- `analysis/b2b-analytics.md`
- `conversational-experience/brand-concierge-conversational-experience.md`

## フェーズ 4：アイコンの生成

コンテンツが作成されたら、`use-case-icon-generator` スキルを呼び出して、新しいユースケースのアイコン仕様を生成します。 スキルに次を提供：
- ユースケース名
- 業種
- ユースケースの簡単な説明

ユーザーが生成されたアイコンファイルを取得したら、カタログ行を更新してアイコン参照を含めます。

```
<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">
```

## フェーズ 5：検証

完了する前に、次のすべてを確認します。

1. **テンプレートへの準拠** – 業界概要のセクションでは、テンプレートが正確に説明されています（##見出し、説明、### ビジネスへの影響、###実装方法、##技術的な考慮事項）。
2. **カタログのプレースメント** - カタログ行は、正しい「業界」タブと正しい「成熟度」グループ（基礎、新興、詳細）に表示されます。
3. **パターンリンクの有効性** – 概要とカタログの両方のパターンリンクが、上記のリストの有効なパターンファイルパスを使用します。
4. **アンカーの一貫性** - カタログリンク（`#abandoned-cart-email-recovery` など）のアンカーは、ケバブケースに変換された概要ファイルの `##` 見出しと一致します。
5. **アイコンパスの規則** - アイコンパスは `assets/use-case-icons/{industry}/icon-{kebab-name}.png` に従います。

検証中に見つかった問題を報告して、完了前に修正してください。
