---
source-git-commit: 2ed15399073fce5ebd1c2ba07b1cf70ec706452c
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%
---
# ユースケースパターンへの移行ステータス「€」ブループリント

このドキュメントでは、ブループリント再編の取り組みの状況をキャプチャし、セッション全体でクリーンに再開できるようにします。

**最終更新日：** 2026-09-24

## 現在の状況と

B2B セクションの一時停止は解除されました。 公開されているアーキテクチャの範囲は、オーディエンス/プロファイルおよびアカウントのアクティベーションページに限定され、廃止されたページはカテゴリの概要にリダイレクトされます。

**現在の状態：** B2B アーキテクチャのクリーンアップが完了しました。 オーディエンス/プロファイルおよびアカウントのアクティベーション ページは、アーキテクチャ図カテゴリに残ります。他のB2B アーキテクチャ ページは廃止され、カテゴリの概要にリダイレクトされました。

## 作業中のアプローチ

> 以下の作業手法は過去のものであり、その後、B2B セクションは上記のように位置付けられました。

このセッションで合意された現在の作業パターンは次の通りです。

1. **ブループリントを有効に保つ**€&quot; no deprecation. それぞれのブループリントは、アーキテクチャに焦点を当てたページとして維持されます。
2. **H1の直後に、関連/重複するユースケース パターンを含むすべてのブループリントにクロスリンク TIP**&#x200B;を追加します。

   ```
   >[!TIP]
   >This blueprint is also available as a [use case pattern](<absolute path>) under <Category>.
   ```

3. **図の移行** ′&quot; ブループリントに、関連するパターンが不足しているアーキテクチャダイアグラムがある場合は、絶対パスを介して同じSVGを参照するパターンに`## Architecture` セクションを追加します。 アセットは元の場所に残ります（ファイルコピーはありません）。
4. パターンでカバーされているブループリントから&#x200B;**実装ステップ**&#x200B;をトリミングします。 削除するセクションには、通常、`## Implementation steps`、`## Implementation patterns`、`## Implementation considerations`、場合によっては`## Prerequisites`が含まれます。 ブループリントごとに判断を行う：
5. **ブループリントごとに変更を提案し、ユーザーの承認を得てから適用します。**€&quot;

### 普遍的なルール

- クロスリンクのヒントの文言は一貫しています：`>This blueprint is also available as a [use case pattern](...) under <Category>.`
- 新しいファイル （移行中に作成されたユースケースパターン） **には`exl-id`**€&quot;が含まれていません。Adobe パブリケーションは、次のファイルを割り当てます。
- 新しく作成されたファイルの画像参照では、相対パスではなく絶対パス （`/help/blueprints/...`）が使用されます。
- 既存のページ上の既存の`exl-id`値は保持されます。
- `redirects.csv`のリダイレクトは、`source,dest`形式に従い、`/en/docs/...`個のパスを含みます（no `.html`）。

## フェーズが完了しました

| フェーズ | 結果 |
| --- | --- |
| A | `B2B Activation & Marketing`個のユースケース パターン カテゴリを作成しました。 3つの既存のパターン （`b2b-audience-activation`}&#39; `b2b/account-audience-activation`, `buying-group-based-marketing`&#39;†&#39; `b2b/buying-group-marketing`, `b2b-analytics`&#39;†`b2b/account-analytics`）を再配置†ました。 3件のリダイレクトが追加されました。 |
| B | 4 B2B ブループリントを`use-case-patterns/b2b/`にコピーしました（`marketo-data-journeys`、`paid-media-orchestration`、`campaign-intake-and-creation`、`campaign-review-and-approval`）。 |
| C | B2B以外の4つのブループリント （`real-time-profile-lookup`、`data-science-profile-enrichment`、`edge-profile-access`、`campaign-v8-orchestration`）をコピーしました。 |
| D | 2つの分割ブループリント （`audience-sharing-with-target`、`third-party-messaging`）をコピーしました。 |
| E | クロスリンクのヒントを9つの重複分類ブループリントに追加しました。 |

ユースケースパターンの合計は、A′€&quot;Eの後です：6つのカテゴリにまたがる&#x200B;**26 パターン**。

## セクションごとのチュートリアル（進行中）

セクションのチュートリアルでは、ユーザーレビューの下で、各ブループリントに対して個別にクロスリンク/ダイアグラム移行/インプリトリムアプローチを適用します。

### 「。.. オーディエンスとプロファイルのアクティベーション」が8/8完了

| # | ブループリント | 実行されたアクション |
| --- | --- | --- |
| 1 | `audience-manager.md` | クロスリンクのヒント +図をパターン （`anonymous-visitor-web-personalization`）に移行+ RTCDPの埋め込み手順を削除 |
| 2 | `enterprise-destinations.md` | クロスリンクのヒント +図をパターン （`audience-activation-to-destinations`）に移行しました |
| 3 | `advertising-activation.md` | Impl手順を削除しました（99°†&#39; 35行） |
| 4 | `customer-activity.md` | Impl手順を削除しました（51†&#39; 40行） |
| 5 | `data-science.md` | Implの考慮事項が削除されました（46†&#39; 40行） |
| 6 | `real-time-lookup.md` | Prereq + impl パターン/ステップ/考慮事項の削除（156†&#39; 73行） |
| 7 | `segment-match.md` | **変更なし** （ユーザーは現状のまま残すことを選択しました） |
| 8 | `rtcdp-target.md` | Impl パターン +考慮事項を削除（99°†&#39; 74行） |

### ‣B2B アクティベーションとマーケティング€&quot; 1/10進行中

| # | ブループリント | ステータス |
| --- | --- | --- |
| 1 | `b2b/overview.md` | 完了 – B2B カテゴリの概要を更新しました |
| 2 | `b2b/b2bactivation.md` | 廃止 – アーキテクチャ図のオーディエンス/プロファイルページに置き換え |
| 3 | `b2b/b2b-account-activation.md` | 保持 – アーキテクチャ図B2B カテゴリに移行 |
| 4 | `b2b/b2b-buying-group-journeys.md` | 退職日 |
| 5 | `b2b/b2b-journeys-with-marketo.md` | 退職日 |
| 6 | `b2b/ajo-b2b-paid-media-controller.md` | 退職日 |
| 7 | `b2b/marketo-engage-and-workfront-integration-blueprint/overview.md` | 退職日 |
| 8 | `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | 退職日 |
| 9 | `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | 退職日 |
| 10 | `b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md` | 退職日 |

### âsÀCustomer Journey Analytics€&quot; 0/5まだ始まっていない

ファイル：`overview.md`、`b2b-cja.md` （フェーズ Eの重複、クロスリンクの追加）、`cja-rtcdp.md` （グループ 2€&quot;、`customer-analytics-insight-generation`へのクロスリンクを推奨）、`cja-ajo.md` （グループ 2€&quot;、同じ）、`analysis.md` （グループ 3、場合によってはexperience-platform/）です。

### âsçお客様のジャーニー@€&quot;退職クリーンアップ完了、ページの移行を保留中

ファイル：`overview.md`; `journey-optimizer/` （4つのファイル：概要、ジャーニー[ フェーズ E]、キャンペーン [ フェーズ E]、3rd パーティのメッセージ [ フェーズ D]）、`campaign-v8/` （3つのファイル：概要[ フェーズ C]、rtcdp-and-v8、ajo-and-v8）。 `decision-management/`と`campaign-v7/`は完全に廃止されました。これらの履歴エントリは監査に残り、URLは承認済みの概要ページにリダイレクトされます。

### âsÀExperience Platform€&quot; 0/6まだ始まっていない

ファイル：`experience-cloud.md`、`platform-applications.md`、`platform-data-flow.md`、`guardrails.md`、`deployment/websdk.md`、`deployment/appsdk.md`。 すべてのスコアは、監査で0 パターンの信号を含むダイアグラムのみのスコアです。 **すべての「変更なし」**€」は、ユースケースパターンが重複しない基本アーキテクチャです。

意思決定管理とCampaign v7の退職決定が完了しました。 関連する未解決の質問
は履歴のみであり、残りの移行作業をブロックしないでください。

## 参照ファイル

| ファイル | 目的 |
| --- | --- |
| [blueprint-audit.md](blueprint-audit.md) | ブループリントごとの監査テーブル（43行）と推奨事項 |
| [rubric.md](rubric.md) | ブループリントの分類に使用する採点基準 |
| [migration-redirects.csv](migration-redirects.csv) | 移行からの段階的なリダイレクト |
| [redirects.csv](../redirects.csv) | 正規表現でファイルをリダイレクトします（フェーズ Aで3行が追加されます） |

## 未解決の未解決の質問を開く（監査から）

2. `event-triggered-messaging`の不確かな重複としてフラグが立てられた&#x200B;**`journey-optimizer-journeys.md`** ′&#39;。トリミングする前に範囲を確認してください。
3. **`customer-journey-analytics/analysis.md`**@」の内容は、CJAではなくExperience Platform Query Serviceに関するものです。`experience-platform/`への再配置を検討してください。
4. **`customer-success-stories.md`**-&quot; リンク専用ページ。ナビゲーションの分類を確認してください。
5. 過去のTOC アンカーの質問を、完了したB2B アーキテクチャの処分に置き換えました。

## 再開の方法

このリポジトリで新しいClaude コードセッションを開き、次のように言います。

> ブループリントの移行を再開しましょう。 `_evaluation/migration-status.md`を読んで、中断したところから再開してください。

B2B アーキテクチャのクリーンアップが完了します。 検証後、次に計画されたアーキテクチャカテゴリに進みます。
