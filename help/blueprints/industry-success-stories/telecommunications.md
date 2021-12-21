---
title: 通信業界 — Journey Optimizer、トリガーメッセージ
description: 顧客に合わせてリアルタイムの契約を提供し、顧客の長期ロイヤリティに対する効率的なオンボーディングを提供します。
solution: Experience Platform, Journey Optimizer
kt: 9486
source-git-commit: 7a81ea5d71355323a784e12207542fb7dd6b286b
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 12%

---


# 電気通信業界のビジネス課題

このブループリントを実装する前に、通信会社の「新しい行を追加」E メールキャンペーンは、ユーザーがコンバージョンを行い、7 日間の待機期間の後にのみ確認したかどうかに依存していました。 これらの条件を満たすと、追加のタッチポイントが開始されます。

この制限は、現在の状態の 7 日間の待機期間よりも早い行を追加したいユーザーに対して、タイムライヤーのフォローアップを開始するために解決する必要がありました。

## Adobe法

* Adobe Journey Optimizerで使用するデータソースとして、変換に失敗して新しい行を追加したユーザーを識別するAdobe Analyticsデータが含まれます。
* Adobe Journey Optimizerは、顧客が自分のアカウントに新しい行を追加して顧客にコンバージョンを促すように設計された、カスタマイズされた「放棄」メッセージを受け取ったときに、ルールを使用します。


## ビジネス価値の提供

| 目標 | 戦術 | ロック解除された値 |
|---|---|---|
| **キャンペーンのコンバージョン率の向上&#x200B;**<br></br>**年間アカウント収益の増加**</ul> | <ul><li>行の追加に関心を示したが、まだコンバージョンに至っていないユーザーに対して、ほぼリアルタイムで新しいセグメントを作成します。</li><li>コンバータに興味のある非コンバータに対する第 2 のタッチポイントを使用して、変換されていない顧客のフォローアップを推進します。 </li><li>テスト戦略を使用して、ジャーニーのパフォーマンスを測定し、E メールによるコンバージョンを最適化します。</li></ul> | <ul><li><strong>高品質で関連性の高いエクスペリエンス：</strong> ジャーニーオーケストレーションを導入することで、顧客はより関連性の高いメッセージを体験し、メールリストの変更を減らすことができます。</li><li><strong>Journey Orchestrationのスケール：</strong>パーソナライズされたタイムリーなジャーニーを作成して、コンバージョンと合計売上高を増やすことができます。</li></ul> |

## キーブループリント：オーディエンスとアクティベーション (Experience Cloudアプリ )

<strong>説明</strong>
<ul><li>ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとしての Adobe Experience Platform と、ストリーミングジャーニーオーケストレーションとメッセージ配信のための Journey Orchestration を使用して、トリガーされるメッセージとストリーミングメッセージングを実行します</li></ul>

<strong>Experience Cloud アプリケーション</strong>
<ul><li>Adobe Journey Optimizer</li></ul> 
<br>

### ブループリントアーキテクチャ

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=ja"><img alt="通信事業向けのサムネイル画像は、顧客が長期的なロイヤリティを実現する効率的なオンボーディングを行いながら、リアルタイムにカスタマイズされた契約を提供します。" src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/journey-optimizer.png?lang=en"/></a>





