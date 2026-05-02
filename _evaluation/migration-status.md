---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 2%

---
# 移行ステータス：ユースケースパターンの設計図

このドキュメントでは、ブループリント再編の取り組みの状況をキャプチャし、セッション全体でクリーンに再開できるようにします。

**最終更新日：** 2026-04-29

## 現在の状況と

**現在、** `b2b/overview.md`で一時停止しています（B2B セクション ブループリント #1 / 10）。そのまま残すか、新しいB2B アクティベーションとマーケティングパターンのセクションに相互参照を追加するか、テーブルを更新してすべてのブループリントを一覧表示するか、相互参照を追加するかの決定を待っています。

**再開するには、**&#x200B;様が&#x200B;**A** （そのまま残す、推奨）、**B** （相互参照を追加）、または&#x200B;**C** （テーブルを更新+相互参照を追加）で応答します。 次に、ブループリント #2 （`b2b/b2bactivation.md`）を続行します。

## 作業中のアプローチ

このセッションで合意された現在の作業パターンは次の通りです。

1. **ブループリントを有効に保つ** – 非推奨にはなりません。 それぞれのブループリントは、アーキテクチャに焦点を当てたページとして維持されます。
2. **H1の直後に、関連/重複するユースケース パターンを含むすべてのブループリントにクロスリンク TIP**&#x200B;を追加します。

   ```
   >[!TIP]
   >This blueprint is also available as a [use case pattern](<absolute path>) under <Category>.
   ```

3. **図の移行** – ブループリントに関連するパターンが不足しているアーキテクチャダイアグラムがある場合は、絶対パスを介して同じSVGを参照するパターンに`## Architecture` セクションを追加します。 アセットは元の場所に残ります（ファイルコピーはありません）。
4. パターンでカバーされているブループリントから&#x200B;**実装ステップ**&#x200B;をトリミングします。 削除するセクションには、通常、`## Implementation steps`、`## Implementation patterns`、`## Implementation considerations`、場合によっては`## Prerequisites`が含まれます。 ブループリントごとに判断を行う：
5. **ブループリントごとに変更を提案し、ユーザーの承認を得てから適用します**。

### 普遍的なルール

- クロスリンクのヒントの文言は一貫しています：`>This blueprint is also available as a [use case pattern](...) under <Category>.`
- 新しいファイル （移行中に作成されたユースケースパターン） **には`exl-id`**&#x200B;が含まれていません – Adobe パブリケーションはこれらのファイルを割り当てます。
- 新しく作成されたファイルの画像参照では、相対パスではなく絶対パス （`/help/blueprints/...`）が使用されます。
- 既存のページ上の既存の`exl-id`値は保持されます。
- `redirects.csv`のリダイレクトは、`source,dest`形式に従い、`/en/docs/...`個のパスを含みます（no `.html`）。

## フェーズ A～E （初期の構造作業） – 完了

| フェーズ | 結果 |
| --- | --- |
| A | `B2B Activation & Marketing`個のユースケース パターン カテゴリを作成しました。 既存の3つのパターン（`b2b-audience-activation` → `b2b/account-audience-activation`, `buying-group-based-marketing` → `b2b/buying-group-marketing`, `b2b-analytics` → `b2b/account-analytics`）を再配置しました。 3件のリダイレクトが追加されました。 |
| B | 4 B2B ブループリントを`use-case-patterns/b2b/`にコピーしました（`marketo-data-journeys`、`paid-media-orchestration`、`campaign-intake-and-creation`、`campaign-review-and-approval`）。 |
| C | B2B以外の4つのブループリント （`real-time-profile-lookup`、`data-science-profile-enrichment`、`edge-profile-access`、`campaign-v8-orchestration`）をコピーしました。 |
| D | 2つの分割ブループリント （`audience-sharing-with-target`、`third-party-messaging`）をコピーしました。 |
| E | クロスリンクのヒントを9つの重複分類ブループリントに追加しました。 |

A-E後のユースケースパターンの合計：6つのカテゴリにわたる&#x200B;**26 パターン**。

## セクションごとのチュートリアル（進行中）

セクションのチュートリアルでは、ユーザーレビューの下で、各ブループリントに対して個別にクロスリンク/ダイアグラム移行/インプリトリムアプローチを適用します。

### ✅ オーディエンスとプロファイルのアクティベーション — 8/8完了

| # | ブループリント | 実行されたアクション |
| --- | --- | --- |
| 1 | `audience-manager.md` | クロスリンクのヒント +図をパターン （`anonymous-visitor-web-personalization`）に移行+ RTCDPの埋め込み手順を削除 |
| 2 | `enterprise-destinations.md` | クロスリンクのヒント +図をパターン （`audience-activation-to-destinations`）に移行しました |
| 3 | `advertising-activation.md` | 取り除かれたImpl手順（99→35行） |
| 4 | `customer-activity.md` | 取り外されたインプル手順（51→40行） |
| 5 | `data-science.md` | Implの考慮事項が削除されました（46→40行） |
| 6 | `real-time-lookup.md` | Prereq + impl パターン/ステップ/考慮事項の削除（156→73行） |
| 7 | `segment-match.md` | **変更なし** （ユーザーは現状のまま残すことを選択しました） |
| 8 | `rtcdp-target.md` | Impl パターンと考慮事項の削除（99→74行） |

### 🟡件のB2B アクティベーションとマーケティング —1/10進行中

| # | ブループリント | ステータス |
| --- | --- | --- |
| 1 | `b2b/overview.md` | **一時停止** – 決定A/B/C待ち（上記の「現在の状況」を参照） |
| 2 | `b2b/b2bactivation.md` | 保留中 – フェーズ Eが重複しています。クロスリンクが追加されました。ダイアグラムのレビューが必要です+ トリムを埋める |
| 3 | `b2b/b2b-account-activation.md` | 保留中：図は分類されています。`b2b/account-audience-activation.md`へのクロスリンクが必要+図の移行を検討してください |
| 4 | `b2b/b2b-buying-group-journeys.md` | 保留中 – フェーズ Eの重複、クロスリンクの追加、レビューが必要 |
| 5 | `b2b/b2b-journeys-with-marketo.md` | 保留中 – フェーズ B コピー、パターンはコピー、プリンプステップのトリミングが必要 |
| 6 | `b2b/ajo-b2b-paid-media-controller.md` | 保留中：フェーズ Bのコピー。インプリステップトリミングが必要 |
| 7 | `b2b/marketo-engage-and-workfront-integration-blueprint/overview.md` | Pending — Section landing page |
| 8 | `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | 保留中：フェーズ Bのコピー。インプリステップトリミングが必要 |
| 9 | `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | 保留中：フェーズ Bのコピー。インプリステップトリミングが必要 |
| 10 | `b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md` | 保留中 – リンク専用ページ（ナビゲーションとしてフラグ付けされた監査） |

### ⚪ Customer Journey Analytics — 0/5はまだ開始されていません

ファイル：`overview.md`、`b2b-cja.md` （フェーズ Eの重複、クロスリンクの追加）、`cja-rtcdp.md` （グループ 2 — `customer-analytics-insight-generation`へのクロスリンクを推奨）、`cja-ajo.md` （グループ 2 – 同じ）、`analysis.md` （グループ 3、場合によってはexperience-platform/）です。

### ⚪件のお客様のジャーニー — 14分の0はまだ開始されていません

ファイル：`overview.md`; `journey-optimizer/` （4つのファイル：概要、ジャーニー[ フェーズ E]、キャンペーン [ フェーズ E]、サードパーティのメッセージ [ フェーズ D]）、`decision-management/` （3つのファイル：概要、エッジ [ フェーズ E]、ハブ [ フェーズ E]）、`campaign-v8/` （3つのファイル：概要[ フェーズ C]、rtcdp-and-v8、ajo-and-v8）、`campaign-v7/` （廃止予定）。

### ⚪ Experience Platform — 0/6はまだ開始されていません

ファイル：`experience-cloud.md`、`platform-applications.md`、`platform-data-flow.md`、`guardrails.md`、`deployment/websdk.md`、`deployment/appsdk.md`。 すべてのスコアは、監査で0 パターンの信号を含むダイアグラムのみのスコアです。 **すべて「変更なし」である可能性があります**。ユースケース パターンが重複しない基盤アーキテクチャです。

## 参照ファイル

| ファイル | 目的 |
| --- | --- |
| [blueprint-audit.md](blueprint-audit.md) | ブループリントごとの監査テーブル（43行）と推奨事項 |
| [rubric.md](rubric.md) | ブループリントの分類に使用する採点基準 |
| [migration-redirects.csv](migration-redirects.csv) | 移行からの段階的なリダイレクト |
| [redirects.csv](../redirects.csv) | 正規表現でファイルをリダイレクトします（フェーズ Aで3行が追加されます） |

## 未解決の未解決の質問を開く（監査から）

1. **意思決定管理エッジ + ハブ** – 現在、両方とも`offer-decisioning`にクロスリンクしています。 単一のデプロイメントオプション図に統合することを検討してください。
2. **`journey-optimizer-journeys.md`** — `event-triggered-messaging`の不確かな重複としてフラグ付けされました。トリミングの前に範囲を確認してください。
3. **`customer-journey-analytics/analysis.md`** — コンテンツはCJAではなくExperience Platform Query Serviceに関するものです。`experience-platform/`への再配置を検討してください。
4. **Campaign v7 （非推奨のファイルが3つ）** – 目次から移行、離脱、削除しますか？
5. **`customer-success-stories.md`** — リンク専用ページ。ナビゲーションの分類を確認してください。
6. 新しいB2B セクションの&#x200B;**目次アンカー**&#x200B;は`{#b2b-patterns}`です。実稼動リダイレクトを作成する前に確認してください。

## 再開の方法

このリポジトリで新しいClaude コードセッションを開き、次のように言います。

> ブループリントの移行を再開しましょう。 `_evaluation/migration-status.md`を読んで、中断したところから再開してください。

次の具体的なステップ：`b2b/overview.md`の決定（A/B/C）に対応します。 次にブループリント #2 （`b2b/b2bactivation.md`）に進み、B2B セクションからCustomer Journey Analytics、カスタマージャーニー、Experience Platformに進みます。
