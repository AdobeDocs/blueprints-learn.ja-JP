---
title: 最終マッピングセットをチェック
description: 顧客アカウントスキーマのシンプルなフィールドマッピングと計算されたフィールドマッピングを、期待される最終的なマッピングセットと比較します。
doc-type: article
solution: Experience Platform
exl-id: d1521d08-1ccb-405f-b728-a2777598cb9f
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 最終マッピングセットをチェック

>[!NOTE]
>
>ストリーミング取り込みラボからアクセスする場合は、以下のリンクをクリックして、そのラボの次の手順に進んでください。
>
>[&#x200B; ストリーミング取り込みラボ – 最終マッピングセットを確認](../../stream-ingestion/check-final-mapping-set.md)



## シンプルなマッピング

>[!NOTE]
>
>\&lt;tenant-name>をサンドボックスの値に置き換えます

| Sourceフィールド | ターゲットフィールド |
| ------------------------- | --------------------------------- |
| account\_create\_date | \&lt;tenant-name>.account.createDate |
| account\_end\_date | \&lt;tenant-name>.account.endDate |
| customer\_id | \&lt;tenant-name>.customerID |
| plan\_name | \&lt;tenant-name>.plan.name |
| plan\_id | \&lt;tenant-name>.plan.planID |
| billing\_city | billingAddress.city |
| billing\_zip\_code | billingAddress.postalCode |
| billing\_state | billingAddress.state |
| billing\_street\_address | billingAddress.street1 |
| email\_optIn | consents.marketing.email.val |
| mobile\_phone | mobilePhone.number |
| firstName | person.name.firstName |
| lastName | person.name.lastName |
| メール | personalEmail.address |
| createDate | repo.createDate |
| modifyDate | repo.modifyDate |
| shipping\_city | shippingAddress.city |
| shipping\_zip\_code | shippingAddress.postalCode |
| shipping\_state | shippingAddress.state |
| shipping\_street\_address | shippingAddress.street1 |

>[!NOTE]
>
>続行する前に、最終的なマッピングが以下に示す内容と一致していることを確認してください。



## 計算マッピング

| 計算フィールド | XDM フィールド |
| ------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| iif （sms\_optIn == nullまたはsms\_optIn == &quot;&quot;, &#39;n&#39;, sms\_optIn） | consents.marketing.sms.val |
| concat （date\_part （&quot;month&quot;, date （birth\_Date,&quot;M/d/yyyy&quot;））.toString （）, &quot;-&quot;, date\_part （&quot;day&quot;, date （birth\_Date,&quot;M/d/yyyy&quot;）.toString （）） | person.birthDayAndMonth |
| date\_part （&quot;yyyy&quot;,date （birth\_Date,&quot;M/d/yyyy&quot;）） | person.birthYear |

>[!NOTE]
>
>続行する前に、最終的なマッピングが以下に示す内容と一致していることを確認してください
