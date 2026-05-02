---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---
# ブループリント評価ルーブリック

このルールは、「アーキテクチャ図とブループリント」セクションの下にあるすべてのドキュメントに適用されます
[TOC.md](../help/blueprints/TOC.md) （76 ～ 133行目）のうち、各ブループリントを
**ユースケースパターン**、**アーキテクチャダイアグラム**、両方（**分割**）、またはフラグが設定されている
**既存のパターンの**&#x200B;を複製します。

このルーブリックを適用する出力は[blueprint-audit.md](blueprint-audit.md)です。

## 定義

- **ユースケースパターン** – 特定のビジネスまたは技術目標を説明する文書
Adobe Workfrontの導入の目的を達成するために考えられるアプローチと考慮事項を説明します。
正規シェイプ：`.claude/skills/use-case-pattern-builder/references/pattern-template.md`。
- **アーキテクチャ図** — システムの機能を表す視覚図、
データフローがあります。 ストーリーは最小限に抑え、ダイアグラムはアーティファクトです。
正規の例：[platform-data-flow.md](../help/blueprints/experience-platform/platform-data-flow.md)

## スコアリング

各ブループリントはエンドツーエンドで読み取られ、8つのバイナリシグナルに対してスコアリングされます。 各シグナルは
+1をパターンスコアまたはダイアグラムスコアに設定します。

### パターン信号（各=+1 パターン）

1. **ビジネス目標の設定** – 収益、リテンション、獲得、リードジェネレーション、コストを設定
顧客体験などのビジネス成果に影響を与えることができます。
2. **KPIまたは成功指標** – 指標、コンバージョン率、一致率、ROI、または
同様の成果指標。
3. **複数の実装オプションまたは成熟度レベル** — オプション A / オプション B、基本vsを表示します。
読者が選択する高度な、または同等の選択肢。
4. **前提条件または準備状況のチェックリスト** – 実装する前に必要な前提条件をリストします。
5. **ナラティブ実装ステップ > ～30行** – 実体的な実装方法のガイダンスではなく
概要を説明しましょう。

### ダイアグラム信号（各= +1 ダイアグラム）

&#x200B;6. システム トポロジを示す&#x200B;**アーキテクチャ/データフロー画像** — `.svg`、`.png`または`.jpg`、
データフロー、または統合矢印。
&#x200B;7. **システム間の統合トポロジ、デプロイメントの形状、またはガードレール** – 方法を説明します
コンポーネントは、データの保存場所、デプロイメントモデル（エッジとハブの比較）、または容量制限に接続します。
&#x200B;8. **Audience is solution architect** — デプロイメント、SDK、edge、hubなどを使用したフレーミング
マーケター向けのフレーミングではなく、アーキテクト向けの用語（キャンペーン，
audiences）。

## レコメンデーションロジック

最初にルールの上書きを適用します。 上書き火災がない場合は、スコアから推奨事項を導き出します。

### ルールの上書き（最優先）

1. **ファイルの名前は`overview.md`**&#x200B;です→推奨事項= `Navigation`。 移行から除外されました。
ページは、子ファイルが解決した後に修正される目次スタイルのランディングページです。
2. **同等のパターンが`help/blueprints/use-case-patterns/`**→に既に存在します
推奨事項= `Duplicate`。 移行アクションは、ブループリントを純粋なものに簡素化することです
アーキテクチャ図を作成し、既存のパターンに「ユースケースパターンを参照」のクロスリンクを追加します。
既存のパターンパスを`duplicate_of`列に記録します。
3. **ファイルは`experience-platform/`にあり、ビジネス目標信号（#1）**&#x200B;がありません。デフォルト→
   他のスコアに関係なく`Diagram`。 このフォルダーはアーキテクチャ概要層です。

### スコアベースのレコメンデーション（上書きしない場合）

| パターンスコア | ダイアグラムスコア | 推奨事項 | 推論 |
| --- | --- | --- | --- |
| ≥ 3 | ≤ 1 | `Pattern` | 強力なパターン信号、弱い図形信号→パターンに移行します。 |
| ≤ 1 | ≥ 2 | `Diagram` | 弱いパターン信号、支配的な視覚的/トポロジの焦点→図として維持します。 |
| ≥ 3 | ≥ 2 | `Split` | 豊富なパターンコンテンツと意味のある図の両方→パターンを抽出し、オリジナルを図に減らし、クロスリンクします。 |
| 2 | 2 | `Split` | 適度な強度で結び→分割します。 |
| 2 | ≤ 1 | `Pattern` | パターンの傾き、大きな図形値なし。 |
| ≤ 1 | ≤ 1 | `Diagram` | 既存の最小限のアーキテクチャページで済むかもしれません。 |

## ルーブリックの適用方法

スコープ内の各ブループリントマークダウンファイルについて：

1. ファイル全体をエンドツーエンドで読み取ります。
2. 8つのシグナルの各々に存在/不存在をマークする。
3. 上書きルールを順番に適用します。 1本が燃えた場合は、それをお勧めします。
4. それ以外は、パターンスコアとダイアグラムスコアを計算して、レコメンデーションを検索します。
5. `Pattern`および`Split`件の推奨事項について、次を提案します。
   - `proposed_pattern_category` — 1つ：
     `audience-building-activation`, `personalization`, `campaign-management-orchestration`,
     `analysis`、`conversational-experience`、または`(new) <name>`というラベルの付いた新しいカテゴリ。
   - `proposed_pattern_title` – 既存のパターンに続く、アクション指向の短いタイトル
命名スタイル：
6. `Diagram`および`Split`件の推奨事項について、次を提案します。
   - `proposed_diagram_title` – 通常、既存のタイトルはビジネスフレームでトリミングされます。
7. ブループリントの範囲を既存のパターンカタログと比較して見つかった重複をキャプチャします
`duplicate_of`に含まれます。
8. 未解決の質問、保存する価値のある固有の技術コンテンツ、または移行リスクを`notes`に記録します。

## 既存のユースケースパターンカタログ（重複検出用）

| カテゴリ | パターン |
| --- | --- |
| audience-building-activation | audience-activation-to-destinations, audience-collaboration-segment-match, b2b-audience-activation, event-forwarding |
| personalization | anonymous-visitor-web-personalization, known-visitor-web-app-personalization, offer-decisioning, behavioral-recommendation |
| campaign-management-orchestration | batch-outbound-message-activation, event-triggered-messaging, multi-step-orchestrated-journey, cross-channel-journey-with-decisioning, buying-group-based-marketing |
| 分析 | customer-analytics-insight-generation, b2b-analytics |
| conversational-experience | brand-concierge-conversational-experience |
