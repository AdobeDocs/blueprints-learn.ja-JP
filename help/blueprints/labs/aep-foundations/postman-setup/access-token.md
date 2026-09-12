---
title: アクセストークン
description: PostmanでOAuth サーバー間アクセストークンを生成し、AEP API呼び出しを認証するために必要なヘッダーを理解します。
doc-type: article
solution: Experience Platform
exl-id: e38a1bd4-5a09-40c6-8303-c3770801c864
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# アクセストークン

## API セキュリティの概要



Adobe製品への安全なAPI接続を確立するには、AdobeでOAuth サーバー間資格情報を作成します。 そのためには、まずAdobe Developer Console内で開発者プロジェクトを作成する必要があります。 Developer Consoleにアクセスするには、Adobe Admin Console内で開発者権限が割り当てられている必要があります。 これらの権限を付与したら、Adobe製品関連の様々なAPIを使用して、開発者プロジェクトを作成できます。 ここで、OAuth Server-to-Server資格情報の出番です。 アクセストークンを生成するには、特定のクレームをAdobeのIdentity Management サービス（IMS）に渡す必要があります。 OAuth サーバー間の資格情報の場合、呼び出しの例は次のようになります。

```curl
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3?client_id={CLIENT_ID}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'client_secret={CLIENT_SECRET}&grant_type=client_credentials&scope={SCOPE}'
```

>[!NOTE]
>
>OAuth サーバー間の資格情報[ここ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/#generate-access-tokens)を使用して開発者プロジェクトを作成するためのe2e プロセスについて詳しく説明します。 ブートキャンプの場合、プロセス 😄のこのステップを「手を振る」ことにします



## ADOBE EXPERIENCE PLATFORM + ADOBE IMS

Adobe サービスへのあらゆるリクエストには、Authorization ヘッダーにアクセストークンと、デベロッパープロジェクトの作成中に生成されたクライアントシークレットを含める必要があります。 さらに、Experience Platformとその関連アプリケーションでは、各リクエストに他の2つのヘッダーパラメーターが存在する必要があります。

- `x-gw-ims-org-id` – このパラメーターは、リクエストが属する`IMS Org`を指定し、リクエストの処理が適切なSaaS環境に解決されるようにします
- `x-sandbox-name` – このパラメーターは、Experience Platform内でリクエストを処理するサンドボックスを指定します

AdobeがAPIをどのように保護し、それらを使用するために必要なものについて少し理解できたところで、今すぐ使用してください。

>[!CAUTION]
>
>`x-sandbox-name` パラメーターを指定しないと、期待どおりにリクエストが失敗しません。 代わりに、任意のExperience Platform環境で自動的にプロビジョニングされる`default` サンドボックスに処理するリクエストがデフォルトになります

>[!NOTE]
>
>このブートキャンプの一環として、デベロッパープロジェクトを作成し、`access_token`をリクエストするために必要なすべての値を含むPostman Environment ファイルを提供しました。 これは、ラボの前の手順でアップロードしたものです

## Postmanでの認証

1. Postmanを起動し、`IMS Authenticate`という名前のディレクトリに移動し、クリックしてリクエストを開きます
1. Postmanの右上隅に、環境ドロップダウンが表示されます。 ドロップダウンから`AEP Bootcamp`環境を選択します
1. 次に、「送信」ボタンをクリックして呼び出しを実行します

![IMS Authenticate呼び出しを送信してアクセストークンを生成した後のPostman リクエスト &#x200B;](assets/access-token-execute-ims-authenticate-request.png)

レスポンスの成功は次のようになります。

```none
200 OK Successful Authentication
```

レスポンスの成功

```json
{
    "token_type": "bearer",
    "access_token": "<value>",
    "expires_in": 86399979
}
```

`token_type` – 常にbearer タイプになります

`access_token` – すべてのAPI呼び出しの認証ヘッダーで認証と必須を証明します

`expires_in` - アクセストークンの有効期限が切れるまでのミリ秒（本日は24時間の有効期限）

>[!TIP]
>
>おめでとうございます。 認証が完了し、access\_tokenが環境ファイルに保存されました



## 一般的なエラー

### 無効なトークン

この問題は、環境ファイルの`private_key`の形式が正しくないか、無効になった場合に発生します。 これが表示されている場合は、改行を含むキー全体をコピーしていることを確認してください

例：

```none
-----BEGIN PRIVATE KEY----- 
some uber long varchar set is here
-----END PRIVATE KEY----- 
```

```none
400 invalid_token
```

>[!NOTE]
>
>JWT ベースの認証を使用する場合にのみ適用されます

### 無効なIMS\_ORG

このエラーは、ドロップダウンからpostman環境を設定するのを忘れた場合に発生します

Postman環境が選択されていない場合、![IMS_ORGがアクティブな環境エラーに見つかりません](assets/access-token-forgot-to-select-postman-environment.png)

>[!NOTE]
>
>API呼び出しを実行する際には、必ずpostman環境を設定してください
>
>![Postman環境ドロップダウンからのAEP Bootcamp環境の選択](assets/access-token-set-postman-environment.png)
