---
title: 通信業界 - トリガーメッセージ用の Journey Optimizer
description: 顧客の長期ロイヤリティに対する効率的なオンボーディングと併せ、顧客に合わせてリアルタイムの契約を提供します。
solution: Journey Optimizer
kt: 9486
exl-id: fa4a6569-3972-4b97-91f1-7ca8ffd3c5b3
source-git-commit: bf99ef23bb07c845a396767a65114874f3a18180
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 78%

---

# 通信業界のビジネス課題

このブループリントを実装する前は、通信会社の「新しい行を追加」電子メールキャンペーンは、ユーザーがコンバージョンを行い、7 日間の待機期間の後にのみ確認したかどうかに依存していました。これらの条件を満たすと、追加のタッチポイントが開始されます。

この制限は、現在の状態の 7 日間の待機期間よりも早い行を追加したいユーザーに対して、よりタイムリーなフォローアップを開始するために解決する必要がありました。

## Adobe法

* Adobe Journey Optimizer で使用するデータソースとして、変換に失敗して新しい行を追加したユーザーを識別する Adobe Analytics データが含まれます。
* Adobe Journey Optimizerは、顧客がカスタマイズされた「放棄」メッセージを受け取ったときにルールを使用し、顧客のアカウントに新しい行を追加して顧客にコンバージョンを促すように設計します。


## 提供されるビジネス価値

| 目標 | 戦術 | 解放されたバリュー |
|---|---|---|
| **キャンペーンのコンバージョン率の向上&#x200B;**<br></br>**年間アカウント収益の増加**</ul> | <ul><li>行の追加に関心を示しはしたたが、まだコンバージョンに至っていないユーザーに対して、ほぼリアルタイムで新しいセグメントを作成します。</li><li>コンバータに関心はあるが、まだコンバージョンに至っていない顧客に対して、第 2 のタッチポイントを使用してフォローアップを推進します。 </li><li>テスト戦略を使用して、ジャーニーのパフォーマンスを測定し、電子メールによるコンバージョンを最適化します。</li></ul> | <ul><li><strong>高品質で関連性の高いエクスペリエンス：</strong> ジャーニーオーケストレーションを導入することで、顧客はより関連性の高いメッセージを体験し、メールリストの頻繁な変更を回避できます。</li><li><strong>大規模な Journey Orchestration：</strong>パーソナライズされた、よりタイムリーなジャーニーを作成して、コンバージョンと総収入を増やすことができます。</li></ul> |

## プライマリブループリント：オーディエンスとアクティベーション (Experience Cloudアプリ )

### 説明

<ul><li>ストリーミングデータ、顧客プロファイル、セグメント化の中央ハブとしての Adobe Experience Platform と、ストリーミングジャーニーオーケストレーションとメッセージ配信のための Journey Orchestration を使用して、トリガーされるメッセージとストリーミングメッセージングを実行します</li></ul>

### Experience Cloud

<ul><li>Adobe Journey Optimizer</li></ul>

### ブループリントアーキテクチャ

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=ja"><img alt="通信ビジネス向けの画像は、顧客が長期的なロイヤリティを実現する効率的なオンボーディングを行い、リアルタイムで顧客に合わせた契約を提供します。" src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/journey-optimizer.png?lang=en"/></a>
