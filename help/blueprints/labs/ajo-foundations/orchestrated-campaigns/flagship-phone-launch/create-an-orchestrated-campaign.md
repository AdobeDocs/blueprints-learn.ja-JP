---
title: オーケストレーションされたキャンペーンの作成
description: オーケストレーションされたキャンペーンのシェルを作成し、そのデフォルトのスケジューリングオプションを確認する方法を説明します。
doc-type: article
solution: Experience Platform
exl-id: e4e8eabd-ab91-4693-9b8a-0f94dd15db13
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# オーケストレーションされたキャンペーンの作成

## 目標

次の一連の手順では、任意のキャンペーンの開始点となるオーケストレーションキャンペーン（アクティビティなし）のシェルを作成します。



## キャンペーンに移動

1. まず、ブラウザーの右上にあるアプリドロワーからアプリケーションを選択して、Adobe Journey Optimizer アプリケーションにログインしていることを確認します

   ![ アプリドロワーからAdobe Journey Optimizerを選択](assets/create-an-orchestrated-campaign-select-ajo-app.png)



2. 左側のナビゲーションパネルで、**キャンペーン**&#x200B;を選択します
3. 次に、右上の「**キャンペーンを作成**」ボタンをクリックします

   ![ キャンペーンナビゲーションの「キャンペーンを作成」ボタン ](assets/create-an-orchestrated-campaign-click-create-campaign.png)



4. 表示されるモーダルで、**Orchestration - Marketing**&#x200B;を選択し、**Confirm**&#x200B;をクリックします

![ オーケストレーション – マーケティングを選択し、「確認」をクリックします](assets/create-an-orchestrated-campaign-select-orchestration-marketing.png)

## キャンペーン設定

1. 必要なキャンペーンメタデータに次の情報を入力します。
   - **名前** —> `Flagship Phone Launch`
   - **説明** —> *空のままにする*
   - **結合ポリシー** —> `Default Timebased`
   - **タグ** —> *空のままにする*

   完了すると、画面は以下のようになります。

   ![ キャンペーン設定が名前と結合ポリシーで入力されました](assets/create-an-orchestrated-campaign-settings-filled.png)

2. 「**保存**」ボタンをクリックして続行します。



## スケジュールについて

キャンペーンを作成した後、すぐにワークフローキャンバスに移動する必要があります。  右上には、このワークフローをキャンペーンに実行する頻度を示すスケジュール設定オプションがあります。

デフォルトは常に&#x200B;**できるだけ早く**&#x200B;に設定されます。 この演習では、既定値を使用しますが、他にも多くのオプションを利用できます。

キャンペーンワークフローが「スケジューラーオプション」を実行する頻度の![ スケジューラーオプション ](assets/create-an-orchestrated-campaign-scheduler-options.png " スケジューラーオプション ")



## まとめ

これで、オーケストレーションされたキャンペーンの作成方法と、スケジューリングに関して使用可能な一般的なオプションを確認しました。
