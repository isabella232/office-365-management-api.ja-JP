---
ms.technology: o365-service-communications
ms.TocTitle: Get started with Office 365 Management APIs
title: Office 365 Management API の使用を開始する
description: この API では、Azure AD を使用してサービスへのアクセス権をアプリケーションに付与するための認証サービスを提供します。
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: ''
ms.localizationpriority: high
ms.openlocfilehash: 96a0cd71c55251160117d1ae598c8935479b6780
ms.sourcegitcommit: 13b50617b1a73f5890414087d8eabe6b2240cfb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2021
ms.locfileid: "58510147"
---
# <a name="get-started-with-office-365-management-apis"></a>Office 365 Management API の使用を開始する

Office 365 Management API と同じようにセキュリティで保護されたサービスへのアクセスを必要とするアプリケーションを作成するときは、アプリケーションがサービスへのアクセス権を保持しているかを確認する方法をサービスに提供する必要があります。Office 365 Management API では、Azure AD を使用してサービスへのアクセス権をアプリケーションに付与するための認証サービスを提供します。 

以下の 4 つの手順があります。

1. **Azure AD でアプリケーションを登録する**。アプリケーションが Office 365 Management API にアクセスできるようにするには、アプリケーションを Azure AD に登録する必要があります。これにより、アプリケーションの ID を設定して、API へのアクセスに必要なアクセス許可レベルを指定できるようになります。
    
2. **Office 365 テナント管理者の同意を得る**。Office 365 Management API を使用してアプリケーションがテナントのデータにアクセスする許可への同意を、Office 365 テナント管理者が明示的に付与する必要があります。同意プロセスでは、テナント管理者がブラウザーを操作して **Azure AD の同意 UI** にサインインし、アプリケーションが要求するアクセス許可を確認して要求を許可または拒否します。同意が与えられると、UI は認証コードを含めた URL を使用してユーザーをアプリケーションにリダイレクトします。アプリケーションは Azure AD にサービス間の呼び出しを行い、この認証コードをテナント管理者とアプリケーションの両方に関する情報が含まれているアクセス トークンと交換します。テナント ID はアクセス トークンから抽出して、将来使用するために格納しておく必要があります。
    
3. **Azure AD からアクセス トークンを要求する**。Azure AD で設定されているアプリケーションの資格情報を使用すると、アプリケーションは、テナント管理者の追加の操作を必要とすることなく、継続的に同意済みのテナントの追加のアクセス トークンを要求します。これらのアクセス トークンはテナント管理者に関する情報が含まれていないため、アプリ専用トークンと呼ばれます。
    
4. **Office 365 Management API の呼び出し**。アプリケーションを認証して承認するため、アプリ専用アクセス トークンが Office 365 Management API に渡されます。
    
次の図は、同意とアクセス トークンの要求のシーケンスを示しています。

![管理 API が承認フローを開始する](images/authorization-flow.png)

> [!IMPORTANT]
> Office 365 管理アクティビティ API を介してデータにアクセスする前に、Office 365 組織の統合監査ログを有効にする必要があります。 これを実行するには、Office 365 監査ログをオンにします。 手順については、「[Office 365 監査ログの検索を有効または無効にする](/office365/securitycompliance/turn-audit-log-search-on-or-off)」を参照してください。 <br/><br/>Office 365 サービス通信 API のみを使用している場合は、統合監査ログを有効にする必要はありません。

## <a name="register-your-application-in-azure-ad"></a>Azure AD でアプリケーションを登録する

Office 365 Management API は、Office 365 テナント データに対し、Azure AD を使用してセキュリティ保護された認証を行います。Office 365 Management API にアクセスするには、アプリを Azure AD で登録する必要があり、構成の一部としてアプリが API にアクセスするために必要なアクセス許可レベルを指定します。


### <a name="prerequisites"></a>前提条件

Azure AD でアプリを登録するには、Office 365 サブスクリプションと、Office 365 サブスクリプションに関連付けられている Azure のサブスクリプションが必要です。開始するには、Office 365 と Azure の両方に、試用版のサブスクリプションを使用できます。詳細については、「[Office 365 開発者プログラムへようこそ](/office/developer-program/office-365-developer-program)」を参照してください。


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a>Azure の管理ポータルを使用してアプリケーションを Azure AD で登録する

適切なサブスクリプションを持つ Microsoft のテナントがあれば、Azure AD でアプリケーションを登録できます。

1. 使用する Office 365 サブスクリプションを持つ Microsoft のテナントの資格情報を使用して、[Azure の管理ポータル](https://manage.windowsazure.com/)にサインインします。Azure の管理ポータルには、[Office の管理ポータル](https://portal.office.com/)の左側のナビゲーション ペインに表示されるリンク経由でアクセスすることもできます。
    
2. 左側のナビゲーション パネルで、[Active Directory] (1) を選択します。[ディレクトリ] タブ (2) が選択されていることを確認してから、ディレクトリ名 (3) を選択します。
    
   ![O365 の [サインアップ] ページ](images/o365-sign-up-page.png)
    
    
3. ディレクトリのページで、**[アプリケーション]** を選択します。Azure AD により、現在テナントにインストールされているアプリケーションの一覧が表示されます。
    
4. **[追加]** を選択します。
    
   ![Office 365 の [管理] ページ](images/o365-admin-page.png)
    
    
5. **[所属組織が開発しているアプリケーションの追加]** を選択します。
    
6. アプリケーションの **名前** を入力し、**[タイプ]** に [Web アプリケーション] または [WEB API] を指定します。
    
7. 適切なアプリのプロパティを入力します。
    
   - **サインオン URL**。ユーザーがサインインし、アプリを使用している URL です。必要に応じて後から変更することができます。
    
   - **アプリ ID URI**。アプリの一意の論理識別子として使用される URI です。URI は、アプリに Windows Azure AD 内のデータにアクセスする権限を付与する外部ユーザーの検証済みのカスタム ドメインでなければなりません。たとえば、Microsoft のテナントが **contoso.onmicrosoft. com** の場合、アプリ ID URI は **https://app.contoso.onmicrosoft.com** などになります。
    
8. アプリが Azure AD に登録されて、クライアント ID が割り当てられます。ただし、構成しなければならない、アプリの重要な側面がまだ残っています。
    

### <a name="configure-your-application-properties-in-azure-ad"></a>Azure AD でアプリケーションのプロパティを構成する

アプリケーションを登録すると、いくつかの重要なプロパティを指定する必要があります。プロパティでは、Azure AD 内でアプリケーションがどのように機能するか、また、テナント管理者が Office 365 Management API を使用してアプリケーションにテナント データへのアクセス許可に同意する方法を指定します。

Azure AD アプリケーションの全般的なアプリケーション構成の詳細については、「[Application オブジェクトのプロパティ](/azure/active-directory/develop/active-directory-application-objects)」を参照してください。


1. **クライアント ID**。この値は Azure AD で自動的に生成されます。アプリケーションは、テナント管理者に同意を求めるとき、および Azure AD からアプリ専用トークンを要求するときに、この値を使用します。
    
2. **アプリケーションはマルチ テナントです**。テナント管理者が Office 365 Management API を使用してアプリケーションにテナント データへのアクセス許可に同意するには、このプロパティは **[はい]** に設定する必要があります。このプロパティが **[いいえ]** に設定されている場合、アプリケーションは、独自のテナント データにしかアクセスすることはできません。
    
3. **応答 URL**。これは、Office 365 Management API を使用してアプリケーションのデータへのアクセス許可に同意した後にテナント管理者がリダイレクトされる URL です。必要に応じて、複数の応答 URL を設定できます。Azure は、アプリケーションを作成する際、指定したサインオン URL に最初に一致した URL を自動的に設定しますが、必要に応じてこの値を変更することができます。
    
これらのプロパティを変更した後は、必ず **[保存]** をクリックしてください。


### <a name="generate-a-new-key-for-your-application"></a>アプリケーションの新しいキーを生成する

キー (クライアント シークレットとも呼ばれます) は、アクセス トークンの認証コードを交換するときに使用されます。


1. Azure 管理ポータルで、アプリケーションを選択し、上部メニューの **[構成]** を選択します。**[キー]** までスクロールダウンします。
    
2. キーの期間を選択し、**[保存]** をクリックします。
    
   ![[Azure サブスクリプション] ページ](images/azure-subscription-page.png)
    
    
3. Azure では、保存後にのみアプリケーション シークレットが表示されます。クリップボード アイコンをクリックして、クライアント シークレットをクリップボードにコピーします。
    
   ![Azure ポータル ページ](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > Azure は、クライアント シークレットを最初に生成したときにのみ表示します。その後で、このページに戻って、クライアント シークレットを取得することはできません。

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a>サービス間の呼び出しを有効にする X.509 証明書を構成します。

デーモンやサービスなど、バックグラウンドで実行されているアプリケーションは、最初の同意が与えられた後、繰り返しテナント管理者に同意を求めることがなく、アプリ専用アクセス トークン要求にクライアントの資格情報を使用できます。 

詳細については、「[クライアント資格情報を使用したサービス間の呼び出し](https://msdn.microsoft.com/library/azure/dn645543.aspx)」を参照してください。

Azure AD からアプリ専用アクセス トークンを要求するときは、X.509 証明書をクライアントの資格情報として使用するよう、アプリケーションを構成しなければなりません。プロセスは 2 つの手順で行います。

- X.509 証明書を取得する。自己署名証明書または公的に信頼された証明機関によって発行された証明書を使用することができます。
    
- 拇印と、証明書の公開キーを含むようにアプリケーション マニフェストを変更します。
    
次の手順は、Visual Studio または Windows SDK _makecert_ ツールを使用して自己署名証明書を生成し、base64 でエンコードされたファイルに公開キーをエクスポートする方法を示しています。


1. コマンド ラインから、次を実行します。
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > X.509 証明書の生成時に、キーの長さが 2048 以上になっていることを確認します。 キーの長さがそれより短い場合は、有効なキーとして受け入れられません。

2. 証明書 MMC スナップインを開き、自分のユーザー アカウントに接続します。 
    
3. 個人用フォルダーで新しい証明書を検索し、base64 でエンコードされたファイル (mycompanyname.cer など) に公開キーをエクスポートします。アプリケーションは Azure ADとの通信にこの証明書を使用して、ユーザーが秘密キーへのアクセスを同様に保持できるようにします。
    
   > [!NOTE] 
   > Windows PowerShell を使用して、拇印と base64 でエンコードされた公開キーを抽出できます。他のプラットフォームには、証明書のプロパティを取得するための同様のツールが用意されています。

4. Windows PowerShell プロンプトから、次を入力して実行します。
    
   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. `$base64Thumbprint`、`$base64Value`、および `$keyid` の値を保存します。これらの値は、次の一連の手順でアプリケーション マニフェストを更新するときに必要になります。
    
   ここで、証明書から抽出された値と、生成されたキー ID を使用して、Azure AD のアプリケーション マニフェストを更新する必要があります。
    
6. Azure 管理ポータルで、アプリケーションを選択し、上部メニューの **[構成]** を選択します。
    
7. コマンド バーの **[管理マニフェスト]** を選択してから、**[マニフェストをダウンロード]** を選択します。
    
   ![コマンド ライン証明書の表示](images/command-line-certificate-display.png)
    
    
8. 編集するためにダウンロードしたマニフェストを開き、空の KeyCredentials プロパティを次の JSON で置き換えます。
    
   ```json
      "keyCredentials": [
        {
            "customKeyIdentifier" : "$base64Thumbprint_from_above",
            "keyId": "$keyid_from_above",
            "type": "AsymmetricX509Cert",
            "usage": "Verify",
            "value": "$base64Value_from_above"
        }
    ],
   ```


   > [!NOTE] 
   > [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) プロパティは、ロール オーバー シナリオでは複数の X.509 証明書のアップロードを可能にする、または漏えいシナリオでは証明書を削除することを可能にするコレクションです。

9. 変更内容を保存します。コマンド バーの **[管理マニフェスト]** を選択して **[マニフェストをアップロード]** を選択し、更新したマニフェスト ファイルを参照してそのファイルを選択することで、更新済みのマニフェストをアップロードします。
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a>アプリが Office 365 Management APIにアクセスするために必要な許可を指定します。

最後に、Office 365 Management API でアプリがどのようなアクセス許可を必要とするかを具体的に指定する必要があります。これを行うには、アプリに Office 365 Management API へのアクセスを追加して、必要なアクセス許可を指定します。


1. Azure 管理ポータルで、アプリケーションを選択して、上部メニューの **[構成]** を選択します。 **[他のアプリケーションに対するアクセス許可]** までスクロール ダウンして、**[アプリケーションの追加]** を選択します。
    
   ![Azure AD のページ](images/azure-ad-page.png)
    
    
2. **Office 365 Management API** を選択して (1) **[選択済み]** 列に表示し、(2) 右下のチェック マークを選択して (3) 選択内容を保存し、アプリケーションのメインの構成ページに戻ります。
    
   ![[Azure AD アプリ] ページ](images/azure-ad-apps-page.png)
    
    
3. これで、目的のアプリケーションがアクセス許可を必要とするアプリケーションの一覧に、Office Management API が表示されます。 **[アプリケーションのアクセス許可]** と **[デリゲートされたアクセス許可]** の両方で、アプリケーションで必要なアクセス許可を選択します。 各アクセス許可の詳細については、それぞれ特定の API リファレンスを参照してください。  

   > [!NOTE] 
   > 活動レポートおよび将来的に削除される脅威インテリジェンスと関連した、未使用のアクセス許可が現在 4 つあります。 これらのアクセス許可は不要なため、いずれも選択しないでください。
    
   ![[アプリケーションの追加] ダイアログ](images/add-an-application-dialog.png)
    
    
4. **[保存]** を選択して、構成を保存します。
    

## <a name="get-office-365-tenant-admin-consent"></a>Office 365 テナント管理者の同意を得る

アプリケーションに Office 365 Management APIを使用するために必要なアクセス許可が構成されたため、テナント管理者は、アプリケーションが API を使用してテナントのデータにアクセスするために、これらのアクセス許可を明示的に与える必要があります。同意を与えるには、テナント管理者は、次の特別に作成された URL を使用して、Azure AD にログインする必要があります。この URL では、アプリケーションの要求したアクセス許可を確認することができます。独自のテナントのデータにアクセスするためにAPI を使用する場合、この手順は必要ではありません。


```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

リダイレクト URL は、Azure AD でアプリケーション用に構成された応答 URL のいずれかと一致するか、サブ パスである必要があります。

次に例を示します。

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

同意 URL をテストするには、その URL をブラウザーに貼り付けて、アプリケーションの登録に使用したテナント以外のテナントの Office 365 管理者の資格情報を使用してサインインします。Office Management API を使用するために必要なアプリケーションのアクセス許可を付与する要求が表示されます。


![Azure AD アプリの追加ページ](images/azure-ad-app-added-page.png)

**[承諾]** を選択すると、指定のページにリダイレクトされます。ページにはクエリ文字列でコードが記載されています。 

次に例を示します。

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

アプリケーションはテナント ID を抽出できるAzure AD からアクセス トークンを取得するために、この認証コードを使用します。テナント ID を抽出し、格納したら、テナント管理者のログインを必要とせずその後のアクセス トークンを取得できます。


## <a name="request-access-tokens-from-azure-ad"></a>Azure AD からアクセス トークンを要求する

Azure AD からアクセス トークンを要求する方法は 2 つです。

- 
  [承認コードの許可フロー](https://msdn.microsoft.com/library/azure/dn645542.aspx)では、テナント管理者が明示的な同意を与え、それによりアプリケーションに認証コードが返されます。その後、アプリケーションはアクセス トークンの認証コードを交換します。このメソッドは、アプリケーションが API を使用してテナントのデータにアクセスするために必要な初期の同意を取得するために必要です。また、この初期の同意は、テナント ID を取得し、保存するために必要です。
    
- [クライアント資格情報の許可フロー](https://msdn.microsoft.com/library/azure/dn645543.aspx)では、古いアクセス トークンが期限切れになったときに、テナント管理者がサインインして同意を明示的に与える必要なしで、アプリケーションは以降のアクセス トークンを要求できるようになります。 このメソッドは、初期テナント管理者の同意が与えられた後、API を呼び出すバックグラウンドで継続的に実行するアプリケーションで使用する必要があります。
    

### <a name="request-an-access-token-using-the-authorization-code"></a>承認コードを使用してアクセス トークンを要求する

テナント管理者が同意を与えると、テナント管理者が Azure AD によって指定の URL にリダイレクトされるときに、アプリケーションはクエリ文字列パラメーターとして認証コードを受け取ります。

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

アプリケーションはアクセス トークン取得のため、認証コードと交換するために、Azure AD に HTTP REST POST を実行します。テナント ID がまだ不明であるため、POSTは「一般的な」エンドポイントに送られます。このエンドポイントの URL にはテナント ID が埋め込まれていません。

```http
https://login.windows.net/common/oauth2/token
```

POST の本文には、次の記述が含まれています。

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a>要求の例

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

アクセス トークンを含むいくつかのプロパティには、応答の本文が含まれます。 

#### <a name="sample-response"></a>応答例

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

返されるアクセス トークンは、同意とアクセスを要求するアプリケーションの両方に関する情報が含まれる JWT トークンです。エンコードされていないトークンの例を次に示します。アプリケーションは、このトークンからテナント ID「tid」を抽出し、期限切れの際に管理者のさらなる介入なしに追加のアクセス トークンを要求するために使用できるよう、保存する必要があります。

#### <a name="sample-token"></a>トークンの例

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1427246416,
  "nbf": 1427246416,
  "exp": 1427250316,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "amr": [
    "pwd"
  ],
  "oid": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
  "upn": "admin@contoso.onmicrosoft.com",
  "puid": "1003BFFD8EC47CA6",
  "sub": "7XpD5OWAXM1OWmKiVKh1FOkKXV4N3OSRol6mz1pxxhU",
  "given_name": "John",
  "family_name": "Doe",
  "name": "Contoso, Inc.",
  "unique_name": "admin@contoso.onmicrosoft.com",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1",
  "scp": "ActivityFeed.Read ServiceHealth.Read",
  "acr": "1"
}
```

### <a name="request-an-access-token-by-using-client-credentials"></a>クライアントの資格情報を使用してアクセス トークンを要求する

テナント ID が判明すると、アプリケーションは、Azure AD にサービス間の呼び出しを行い、期限切れの際に追加のアクセス トークンを要求することができます。これらのトークンには、同意を許可した管理者ではなく、要求元のアプリケーションについての情報のみが含まれます。サービス間の呼び出しでは、アプリケーションが X.509 証明書を使用して、base64 でエンコードされ、SHA256 で署名されている JWT ベアラー トークンの形式でクライアントのアサーションを作成する必要があります。

.NET でアプリケーションを開発するときには、[Azure AD Authentication Library (ADAL)](/azure/active-directory/develop/active-directory-authentication-libraries) を使用してクライアントのアサーションを作成できます。他の開発プラットフォームにも同様のライブラリが必要です。

エンコードされていない JWT トークンは、次のプロパティを持つヘッダーとペイロードで構成されます。

```json
HEADER:

{
  "alg": "RS256",
  "x5t": "{thumbprint of your X.509 certificate used to sign the token",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/{tenantid}/oauth2/token",
  "iss": "{your app client ID}",
  "sub": "{your app client ID}"
  "jti": "{random GUID}",
  "nbf": {epoch time, before which the token is not valid},
  "exp": {epoch time, after which the token is not valid},
}

```

#### <a name="sample-jwt-token"></a>JWT トークンの例


```json
HEADER:

{
  "alg": "RS256",
  "x5t": "YyfshJC3rPQ-kpGo5dUaiY5t3iU",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token",
  "iss": "a6099727-6b7b-482c-b509-1df309acc563",
  "sub": "a6099727-6b7b-482c-b509-1df309acc563"
  "jti": "0ce254c4-81b1-4a2e-8436-9a8c3b49dfb9",
  "nbf": 1427248048,
  "exp": 1427248648,
}
```

クライアントのアサーションは、アクセス トークンを要求するサービス間の呼び出しの一部として Azure AD に渡されます。クライアントの資格情報を使用してアクセス トークンを要求する際は、HTTP POST をテナント固有のエンドポイントに使用してください。このエンドポイントのURL には、以前に抽出され、格納されたテナント ID が埋め込まれています。


```http
https://login.windows.net/{tenantid}/oauth2/token
```

POST の本文には、次の記述が含まれています。


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a>要求の例

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

応答は前と同じになりますが、トークンは同じプロパティを持ちません。同意を許可する管理者のプロパティが含まれていないためです。 

#### <a name="sample-response"></a>応答例

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a>アクセス トークンの例

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1431655194,
  "nbf": 1431655194,
  "exp": 1431659094,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "roles": [
    "ServiceHealth.Read",
    "ActivityFeed.Read"
  ],
  "oid": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "sub": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "idp": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1"
}
```


## <a name="build-your-app"></a>アプリを作成する

Azure AD でアプリを登録して、必要なアクセス許可を構成したため、これでアプリを作成する準備ができました。以下は、アプリを設計し、作成する際に考慮すべき重要な側面の一部です。

- **同意エクスペリエンス**。お客様からの同意を得るには、ブラウザーにAzure AD の Web サイトに移動させる必要があります。前述の特別に作成された URL を使用し、同意を得た後に Azure AD がリダイレクトする Web サイトを準備する必要があります。この Web サイトは URL から認証コードを抽出し、それを使用してテナント ID を取得するアクセス トークンを要求する必要があります。
    
- **システムにテナント ID を格納する**。Azure AD からアクセス トークンを要求するとき、および Office Management API を呼び出すときに必要となります。
    
- **アクセス トークンを管理する**。必要に応じてアクセス トークンを要求および管理するコンポーネントが必要です。アプリが定期的に API を呼び出す場合、トークンをオンデマンドで要求することができます。また、データ取得のために継続的に API を呼び出す場合は、定期的な間隔 (たとえば、45 分ごと) でトークンを要求することができます。
    
- 必要に応じて使用している特定の API により **Webhook リスナーを実装する**。
    
- **データを取得し、格納する**。使用している特定の API によって、連続的なポーリングを使用して、または Webhook 通知への応答として、各テナントのデータを取得するコンポーネントが必要があります。
    
