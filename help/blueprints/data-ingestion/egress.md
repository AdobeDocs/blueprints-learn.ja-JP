---
title: データのアクセスと書き出しのブループリント
description: Adobe Experience Platformとアプリケーションからデータにアクセスし、書き出す方法について説明します。
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-Time Customer Data Platform, Data Collection
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 91%

---

# データアクセスおよびブループリントの書き出し

データのアクセスと書き出しのブループリントは、アプリ [!DNL Experience Platform] ーションやアプリケーションからデータにアクセスしたり書き出したりできる、あらゆる方法の概要を示しています。

ブループリントは [!DNL Experience Platform] とアプリケーションからのデータアクセス用に 2 つのカテゴリに分類されています。

1 つ目は、[!DNL Experience Platform] およびアプリケーションからデータを出力するアプローチです。 これは、データ出力の _プッシュ_ タイプの方法と見なされます。

2 つ目のアプローチは、アプリ [!DNL Experience Platform] ーションおよびアプリケーションからデータにアクセスするアプローチです。 これは、データアクセスの _プル_ タイプの方法と見なされます。

データアクセスのアプローチ

* [リアルタイム顧客プロファイルアクセス API](#rtcp-profile-access-api)
* [データアクセス API](#data-access-api)
* [クエリサービス](#query-service)

データ書き出しのアプローチ：

* [クライアントサイドのタグ](#client-side-tags-extensions)
* [イベント転送](#event-forwarding)
* [Real-time Customer Data Platform の宛先](#RTCDP-destinations)
* [Journey Optimizer カスタムアクション](#jo-custom-actions)

## データアクセスおよび書き出しの概要アーキテクチャ

<img src="../experience-platform/assets/aep_data_flow.svg" alt="データ準備と取り込みブループリントの参照アーキテクチャ" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## データのアクセス方法と書き出し方法

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1133px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:39px; vertical-align:top; width:1133px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">ストリーミング宛先</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">方法</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">一般的なユースケース</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プロトコル</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">注意点</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja" style="color:#0563c1; text-decoration:underline">イベント転送</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">分析および収集のために Adobe SDK から収集された未処理データのエンタープライズシステムへの転送</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">拡張機能を使用したサードパーティデータ収集の軽量タグ付け<sup></sup></span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プッシュ</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">低レベルの未処理イベント</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">集計または前のレコードコンテキストが追加されていない</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=ja#:~:text=containing%20profile%20exports.-,Streaming%20segment%20export%20destinations,-Segment%20export%20destinations" style="color:#0563c1; text-decoration:underline">RTCDP - ストリーミングセグメントの書き出し</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">RTCDP からマーケティングおよび広告、システムに対してオーディエンスをアクティブ化</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プッシュ</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">オーディエンスメンバーシップを表す集計データ</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">未処理のエクスペリエンスイベントデータのアクティベーションがない</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=ja#:~:text=file%2Dbased)%20destinations-,Streaming%20profile%20export%20destinations%20(enterprise%20destinations),-IMPORTANT" style="color:#0563c1; text-decoration:underline">RTCDP - プロファイル書き出しの宛先</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">RTCDP の豊富な行動プロファイルとオーディエンスを活用して、消費者エクスペリエンスとマーケティングを強化。</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">RTCDP からマーケティングおよび広告、オーディエンスおよびプロファイル属性を操作するシステムに対して、オーディエンスおよびプロファイル属性をアクティブ化。 </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">AEP プロファイルをメールサービスプロバイダー、リード育成、CRM システムに対してアクティブ化。</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プッシュ</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">オーディエンスメンバーシップとプロファイルレコード属性を表す集計データ</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">未処理のエクスペリエンスイベントデータのアクティベーションがない</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=ja" style="color:#0563c1; text-decoration:underline">RTCDP - 宛先のパーソナライゼーション</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">ブラウザーおよびクライアントサイドのエクスペリエンスでリアルタイム顧客プロファイルにアクセスし、クライアントサイドのパーソナライゼーションを強化。 </span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">WebSDK のデプロイが必要</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-sdk/overview.html?lang=ja" style="color:#0563c1; text-decoration:underline">RTCDP - Destination SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">RTCDP の宛先で、カスタマイズした宛先カードを設定。</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">ファイルおよびストリーミングタイプの宛先をサポート</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">CSV</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">パートナーおよびブランドがカスタム宛先カードを設定することを許可</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=ja" style="color:#0563c1; text-decoration:underline">RTCDP - Profile Lookup Hub API</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プロファイルにアクセスして、サポートやセールス担当者のインタラクションなど、担当者が支援するエクスペリエンスの消費者エクスペリエンスを強化。</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プル</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">ハブ参照は 500 ms 以上のユースケースにのみ最適</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">RTCDP - Profile Lookup Edge API* ベータ版</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">エッジ上のプロファイルにアクセスして、パーソナライゼーションや web およびモバイルに関するオファーの決定など、200 ms 以内のリアルタイムのエクスペリエンスに対して消費者エクスペリエンスを強化。</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プル</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:27px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">リアルタイムのエクスペリエンスおよびサーバー間統合の場合</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:240px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=ja" style="color:#0563c1; text-decoration:underline">Journey Optimizer カスタムアクション</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:467px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">外部システムに通知する 1 対 1 のジャーニーイベントとトリガーのアクティベーション。買い物かごの放棄、アプリケーションの放棄、登録。</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プッシュ</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">JSON</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">特定のプロファイルに対する単一イベントのアクティベーション。集計または一括操作向きではない</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

<p> </p>

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1132px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:39px; vertical-align:top; width:1132px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">バッチの宛先</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">方法</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">一般的なユースケース</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プロトコル</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">注意点</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/data-access/api.html?lang=ja" style="color:#0563c1; text-decoration:underline">データアクセス API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Experience Platform 外のデータサイエンスおよび ML ワークフローの未処理データへのアクセス。</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プル</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Parquet ファイル</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">使用可能なデータセットに parquet ファイルにアクセスして処理するには、開発プロセスが必要</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ja" style="color:#0563c1; text-decoration:underline">クエリサービス</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">集計されたインサイトとレポートに対して、データセットのクエリ結果を保持。 </span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プル</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">PostgreSQL </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">SQL クライアント</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">集計データのみ。10 分のクエリ制限。</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:245px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-datasets.html?lang=ja" style="color:#0563c1; text-decoration:underline">データセット書き出し* ベータ版</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:462px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">外部のレポート、分析、データサイエンスツールで使用する Experience Platform イベントデータを書き出し。 </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">外部のレポート、分析、データサイエンスツール用に、集計されたプロファイルインサイトとオーディエンスメンバーシップの書き出し。 </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:144px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">プッシュ</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">REST API </span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">CSV</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:281px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">現在ベータ版で、データセットタイプのサブセットから開始。</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>



## データアクセスのアプローチ

### リアルタイム顧客プロファイルアクセス API {#rtcp-profile-access-api}

顧客は、リアルタイム顧客プロファイルアクセス API を使用して、すべてのプロファイル ID、オーディエンスメンバーシップ、属性、エクスペリエンスイベントを含む、リアルタイム顧客プロファイル格納から単一の統合プロファイルにアクセスすることができます。

詳しくは、[リアルタイム顧客プロファイルアクセス API](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=ja) ドキュメントを参照してください。

#### ユースケース

* 単一のプロファイルを検索して、チャットやコールセンターを通じたサポートインタラクション、店頭でのセールスインタラクションなど、エージェントの顧客インタラクションにコンテキストを追加します。
* 外部システム（Web パーソナライゼーションシステムやオファー決定支援システムなど）によっておこなわれるパーソナライゼーションの決定に、コンテキストの追加を許可します。

#### 注意点

* リアルタイム顧客プロファイル[ガードレール](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)が適用されます。
* 一度に 1 つのプロファイル参照用に設計されています。一括プロファイルアクセスや、分析やデータ サイエンスに使用するプロファイル母集団全体のダウンロードには使用されません。
* プロファイル参照の応答時間は、プロファイルガードレールに従います。リアルタイムの低遅延要件（同じページのパーソナライゼーション要件の場合など）は、[Adobe Target 接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ja) または [カスタムパーソナライゼーション接続](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=ja)から Edge プロファイルを利用して、ブラウザー内およびアプリ内パーソナライゼーションのリアルタイムプロファイルアクセスを行う必要があります。

### データアクセス API {#data-access-api}

データアクセス API を使用すると、顧客が Experience Platform データレイクに保存されている生データのセットファイルに直接アクセスすることができます。

* データアクセス API の使用に関する詳細は、[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=ja)を参照してください。

#### ユースケース

* エンタープライズ環境での保存と評価のために、生データファイルと処理済みデータファイルを Experience Platform からプルします。

#### 注意点

* データにバッチ非同期でアクセスすると、タグの活用、イベント転送、RTCDP 宛先などのストリーミングデータ送り出しのアプローチと比較して、データへのアクセスは潜在的に遅延します。
* データファイルが Experience Platform に取り入れられて処理されると、ファイルのコレクションとしてバッチで保存され、圧縮されて Parquet 形式で保存されます。したがって、ファイルにアクセスして別の環境にダウンロードする場合は、データセット全体ではなく、バッチとファイルによって体系的にアクセスする必要があり、データに対する操作では、parquet 形式で圧縮されているファイルを考慮する必要があります。

### クエリサービス {#query-service}

Experience Platform クエリサービスを使用すると、顧客は Experience Platform 内でデータセットに対してクエリを実行し、クエリの結果を保持することができます。SQL クライアントを使用してクエリを実行し、SQL クライアントがサポート可能な目的の保存先に、クエリのレスポンスを保持することができます。クエリサービス UI を使用して、SQL 結果を Experience Platform 内のターゲットデータセットに保存したり、結果をローカルマシンに保存したりすることができます。

* Experience Platform クエリサービスからの SQL 結果を保持するための SQL クライアントへの接続の詳細については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=ja)を参照してください。

#### ユースケース

* Experience Platform データセットから生データをクエリし、クエリ結果を保持します。
* プロファイルスナップショットデータセットをクエリして、リアルタイム顧客プロファイルのインサイトを抽出します。[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=ja#profile-attribute-datasets)。
* クエリ結果を、アクセス用に別のデータセットに保存するか、RTCDP やリアルタイム顧客プロファイルにアクセスするその他の Experience Cloud アプリケーションを介して後で出力できるプロファイル対応のデータセットに保存します。

#### 注意点

* データがバッチ非同期的にクエリされるため、タグの活用、イベント転送、RTCDP 宛先などのストリーミングデータ送り出しのアプローチと比較して、データへのアクセスは潜在的に遅延します。
* Experience Platform データレイクで使用可能なデータのみが、クエリサービスを使用してクエリすることができます。リアルタイム顧客プロファイル格納、ID グラフ、Customer Journey Analytics は、クエリサービスを使用して直接クエリすることができません。プロファイルスナップショットデータセットの例に示すように、データセットがデータレイクにエクスポートされている場合にのみ、これらのデータセットをクエリすることができます。
* クエリ結果の数とクエリタイムアウトのガードレールは、[クエリサービスガードレール](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ja)ドキュメントで概説されているように適用されることご注意ください。

## データ書き出しのアプローチ

### クライアントサイドのタグ拡張機能 {#client-side-tags-extensions}

拡張機能は、アドビのタグソリューションを使用してデプロイすることができます。拡張機能がデプロイされると、データリクエストがクライアントブラウザーまたはアプリケーションに直接デプロイされ、リクエストを呼び出して、目的の宛先にデータとリクエストを送信することができます。

詳しくは、[タグの概要](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ja)ドキュメントを参照してください。

#### ユースケース

* タグ付けを使用して、クライアント側の環境から直接生のストリーミング情報を収集します。

#### 注意点

* Experience Platform のリアルタイム顧客プロファイルやオーディエンスメンバーシップなど、サーバー側の情報に直接アクセスすることはできません。
* ページにデータ収集タグを追加すると、ページの読み込み時間が長くなる場合があります。
* 特定の条件が満たされた場合にのみデータをリクエストするルールを設定する機能。
* データはクライアントから直接収集され、データ収集の前に実行することができる変換とエンリッチメントのタイプを制限します。

### イベント転送 {#event-forwarding}

データ収集リクエストは、Adobeの [!DNL Edge Network] に直接収集されます。 [!DNL Edge Network] から外部の RESTful エンドポイントへのリクエストは、これらのリクエストを外部の宛先に転送するように設定できます。

詳しくは、以下の[イベント転送](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ja)ドキュメントを参照してください。

#### ユースケース

* アドビのサーバー側イベント転送を使用して、生のストリーミング情報をクライアント側環境からエンタープライズエンドポイントに直接収集します。

#### 注意点

* イベント転送を使用するには、Web SDK または MobileSDK を使用してデータを [!DNL Edge Network] に送信する必要があります。
* イベント転送のアプローチでは、ページにタグが追加されるので、ページの読み込み時間と重み付けが軽減されます。
* エッジプロファイルまたは他のデータソースからのエンリッチメントは、現在サポートされていません。
* 限定的なデータフィルタリングと単純なマッピング変換がサポートされています。

### Real-time Customer Data Platform の宛先 {#RTCDP-destinations}

プロファイル属性データとオーディエンスメンバーシップデータを、企業や広告の宛先に対してアクティブ化することができます。これは、送信されたデータを Experience Platform のリアルタイム顧客プロファイルに取り込む必要があることを意味します。

詳しくは、 [Real-time Customer Data Platform の宛先](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=ja)ドキュメントを参照してください。

#### ユースケース

* 内部エンタープライズデータ格納、分析ツール、電子メールシステムやサポートシステムへのオーディエンスメンバーシップを含む、プロファイル属性情報をアクティブ化します。
* 外部の広告ベンダーに対してプロファイルオーディエンスのメンバーシップをアクティブ化し、プロファイルに対するコンテンツのターゲティングとパーソナライズを行います。

#### 注意点

* プロファイル属性とオーディエンスメンバーシップをアクティブ化することができます。生のエクスペリエンスイベントは現在、RTCDP の宛先の一部としては、アクティブ化することができません。
* セグメント評価の特性と、宛先が受け入れる取り込みプロトコルの特性に応じて、ストリーミングまたはバッチで、アクティブ化が発生します。

### Journey Optimizer カスタムアクション {#jo-custom-actions}

Journey Optimizer を使用すると、顧客はジャーニーキャンバスからカスタムアクションを呼び出して、設定された外部 API エンドポイントにペイロードまたはメッセージを送信することができます。アクションは、JSON 形式のペイロードを使用して REST API を介して呼び出すことができる任意のプロバイダーの任意のサービスに対して設定することができます。このペイロードには、イベント情報、プロファイル属性と以前のイベントデータ、ジャーニーで設定された変換とエンリッチメントを含めることができます。

詳しくは、 [Journey Optimizer のカスタムアクション](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=ja)ドキュメントを参照してください。

#### ユースケース

* リアルタイム顧客プロファイルからの追加情報を含む Experience Platform および Journey Optimizer からのアクティベーションイベント。
* 顧客がジャーニーの特定のポイントに到達したときに、外部システムに通知します。

#### 注意点

* [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=ja)によってサポートされるスループットのガードレール、および[リアルタイム顧客プロファイル](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ja)によってサポートされるエンリッチメントのガードレールに適用されます。
* カスタムアクションは、ジャーニーのイベントまたはプロファイルごとに 1 つずつストリーミングで実行することができます。ファイルまたはカスタマージャーニー全体の集約されたリクエストの形式での一括操作または一括データ送信は、実行することができません。
* アクティベーションペイロードに含めることができる、リアルタイム顧客プロファイル属性とエクスペリエンスイベントへのストリーミングアクセス。
* イベントを外部の宛先に送信する前に、イベントデータをフィルタリングし、単純なマッピング変換を適用することができます。
