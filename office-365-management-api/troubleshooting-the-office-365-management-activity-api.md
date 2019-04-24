---
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Office 365 マネージメント アクティビティ API のトラブルシューティング
description: この API のサポートについて Microsoft サポートに最も多く寄せられる質問のまとめです。
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: 09/05/2018
localization_priority: Priority
ms.openlocfilehash: ed84984dc3009d03e0bb7cacba16eafb687c93e0
ms.sourcegitcommit: 5b1eaeb7f262b7b9f7ab30ccb9f10878814153ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "32223953"
---
# <a name="troubleshooting-the-office-365-management-activity-api"></a>Office 365 マネージメント アクティビティ API のトラブルシューティング

Office 365 マネージメント アクティビティ API (別名、*統合監査 API*) は、Office 365 のセキュリティおよびコンプライアンス機能の一部でしかありませんが、次の理由から大きな注目を集めています。

- 複数の監査パイプライン ワークロード (SharePoint や Exchange など) にプログラムでアクセスできます
- 監査データの集計およびインデックス作成のために、広範なサード パーティ ベンダーによって使用されるメイン インターフェイスです

マネージメント アクティビティ API と Office 365 サービス コミュニケーション API を混同しないでください。 マネージメント アクティビティ API は、各種のワークローでのエンド ユーザーのアクティビティを監査するためのものです。  サービス コミュニケーション API は、Office 365 で利用可能なサービス (Dynamics CRM や ID サービスなど) によって送信される状態やメッセージを監査するためのものです。

比較的に少数の操作を備えたシンプルな REST インターフェイスになっているにもかかわらず、マネージメント アクティビティ API の使用方法とデータ取得の正確なしくみについて多くの誤解があります。  マネージメント アクティビティ API の入門者が明確にしておく必要のあることの 1 つは、イベントが発生した日付、イベントの発生元になる可能性のあるサイト コレクション、イベントの種類などのイベントの詳細によってクエリを実行するという概念がないことです。  その代りに、特定のワークロード (SharePoint や Azure AD など) に対するサブスクリプションを作成します。また、それぞれのサブスクリプションはテナント単位にします。

この記事は、この API のサポートについて Microsoft サポートに最も多く寄せられる質問をまとめたものです。  ここでは、選りすぐりのシンプルな PowerShell スクリプトを示します。これらのスクリプトにより、ユーザーから最も多く寄せられる質問への回答を示すことができます。また、主な操作の用例が示されているためカスタム ソリューションの実装を開始する際に役立てることもできます。  この記事では説明されていない操作もありますが、「[Office 365 マネージメント アクティビティ API リファレンス](office-365-management-activity-api-reference.md)」には、すべての操作が示されています。

## <a name="questions-about-third-party-tools-and-clients"></a>サード パーティ製のツールとクライアントに関する質問

現時点でサポートの対象になっている質問のうち最も共通するカテゴリは、監査データのダウンロードおよび集計にサード パーティ製の製品を使用しているユーザーからのものです。 サード パーティ製の製品によっては、セットアップで問題が発生することや、該当する製品で公開されるデータに中断や矛盾が発生することがあります。 そのような場合は、まず、ベンダーのサポート組織に問い合せてください。 サポートに寄せられたすべてのサービス要求についてエンジニアが調べたところ、テナント固有のサービスの問題が原因になっていたケースは 1 つしかありませんでした。

それにもかかわらず、こうしたユーザーの問題が解決されていないことがあります。 ベンダーが問題はサービスにあると主張している可能性もありますが、ベンダーに問い合せる前にユーザーが最初の確認をしようとしているだけだとも考えられます。 

## <a name="connecting-to-the-api"></a>API への接続

ほとんどのアプリケーションは、簡単なクライアント資格情報の OAuth2 フローを使用して API に接続します。 そのため、最初の手順では、マネージメント アクティビティ API のデータへのアクセスに必要なアクセス許可を持つ Azure AD アプリケーションを作成します。 Azure AD アプリの登録を作成する手順に関する説明は、この記事の範囲外になります。 詳細については、「[クイック スタート: Azure Active Directory v1.0 エンドポイントを使用してアプリを登録する](https://docs.microsoft.com/ja-JP/azure/active-directory/develop/active-directory-integrating-applications)」を参照してください。

### <a name="azure-application-permissions"></a>Azure アプリケーションのアクセス許可

現在、Office 365 マネージメント アクティビティ API に使用されている 3 つのアクセス許可は次のとおりです。
1. 組織のアクティビティ データの読み取り
2. 組織のサービス正常性情報の読み取り
3. データ損失防止 (DLP) ポリシー イベントの読み取り (機密情報の検出を含む) 

> [!NOTE] 
> 上記のアクセス許可セットの少なくとも最初の 2 つには、「アプリケーションのアクセス許可」と「デリゲートされたアクセス許可」の両方を有効にする必要があります。 DLP ポリシー イベントの読み取りは、DLP ワークロードに注目する場合にのみ必要になります。

### <a name="getting-an-access-token"></a>アクセス トークンの取得

次に示す PowerShell スクリプトでは、アプリ ID とクライアント シークレットを使用して、マネージメント アクティビティ API 認証エンドポイントから OAuth2 トークンを取得します。 その後で、アクセス トークンを `$headerParams` 配列変数に格納します。HTTP 要求には、この配列変数を添付します。 

```powershell
# Create app of type Web app / API in Azure AD, generate a Client Secret, and update the client id and client secret here
$ClientID = "<YOUR_APPLICATION_ID"
$ClientSecret = "<YOUR_CLIENT_SECRET>"
$loginURL = "https://login.microsoftonline.com/"
$tenantdomain = "<YOUR_DOMAIN>.onmicrosoft.com"
# Get the tenant GUID from Properties | Directory ID under the Azure Active Directory section
$TenantGUID = "<YOUR_TENANT_GUID>"
$resource = "https://manage.office.com"
# auth
$body = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
$headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"} 
```

`$oauth` 変数には、応答オブジェクトを格納します。このオブジェクトには、アクセス トークンなど複数のプロパティが含まれています。 次に、応答例を示します。

```json
token_type     : Bearer
expires_in     : 3599
ext_expires_in : 0
expires_on     : 1508285860
not_before     : 1508281960
resource       : https://manage.office.com
access_token   : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyIsImtpZCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyJ9.eyJhdWQiOiJodHRwczov…
```

## <a name="checking-your-subscriptions"></a>サブスクリプションの確認

既存のマネージメント アクティビティ API クライアントまたはソリューションへのデータ フローに中断が発生したときには、サブスクリプションに何らかの問題が発生しているのではないかと疑われることがあります。 アクティブなサブスクリプションを確認するために、前述のスクリプトに次のコードを追加します。

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
```

#### <a name="sample-response"></a>応答例 

```json
StatusCode        : 200
Status Description : OK
Content           : [{"contentType":"Audit.Exchange","status":"enabled","webhook":null},{"contentType":"Audit.SharePoint","status":"enabled","webhook":{"authId":"","address":"https://mvcwebapiwebhookreceiver.azurewebsite...
RawContent        : HTTP/1.1 200 OK
                    Pragma: no-cache
                    Content-Length: 266
                    Cache-Control: no-cache
                    Content-Type: application/json; charset=utf-8
                    Expires: -1
                    Server: Microsoft-IIS/8.5,Microsoft-IIS/8.5
                    X-AspNet-Versi...
Forms             : {}
Headers           : {[Pragma, no-cache], [Content-Length, 266], [Cache-Control, no-cache], [Content-Type, application/json; charset=utf-8]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 266
```

これは、Audit.Exchange と Audit.SharePoint のサブスクリプションがテナントで有効になっていることを示しています。 Exchange サブスクリプションには使用可能な Webhook がありません (null)。SharePoint サブスクリプションには使用可能な Webhook があります (登録されたエンドポイントのアドレスが示されています)。

## <a name="creating-a-new-subscription"></a>新しいサブスクリプションの作成

新しいサブスクリプションを作成するには、/start 操作を使用します。

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"
```

> [!NOTE] 
> `$headerParams` のデータは、この記事の「[API への接続](#connecting-to-the-api)」に示したスクリプトの最初の部分で設定されています。

前述のコードにより、Audit.AzureActiveDirectory コンテンツ タイプに対する新しいサブスクリプションが作成されます (Webhook は Null になっています)。 その後で、この記事の「[サブスクリプションの確認](#checking-your-subscriptions)」セクションで示したコードを使用すると、サブスクリプションを確認できます。

## <a name="checking-content-availability"></a>コンテンツの利用の可否の確認

特定の期間中に、どのコンテンツ BLOB が作成されたかを確認するために、「API への接続」セクションに示したスクリプトに次の行を追加できます。

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

上記の例では、本日 (午前 12 時 00 分 UTC から現在の時刻までに) 利用可能になったすべてのコンテンツの通知を取得しています。 別の期間を指定する場合は、URI に *starttime* パラメーターと *endtime* パラメーターを追加します (照会可能な最長の期間は 24 時間である点に注意してください)。次に例を示します。

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE] 
> *starttime* パラメーターと *endtime* パラメーターは、「両方とも使用する」または「両方とも使用しない」のどちらかにする必要があります。

上記の要求により、指定した期間中に利用可能になった通知のコレクションを含む JSON オブジェクトが返されます。 応答は次のようになります。

```json
[{      "contentUri" : "https://manage.office.com/api/v1.0/<<your_tenant_guid>>/activity/feed/audit/20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentId" : "20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentType" : "Audit.SharePoint",
        "contentCreated" : "2017-10-13T18:00:51.748Z",
        "contentExpiration" : "2017-10-20T18:00:51.748Z",
}]
```

> [!IMPORTANT] 
> - *contentUri* プロパティは、コンテンツ BLOB を取得できる URI です。 イベントの詳細は BLOB 自体に格納されていて、1 ～ N 件のイベントに関する詳細が格納されています。 コレクションには 30 件の JSON オブジェクトが存在している可能性があり、それらの 30 件のコンテンツ URI には、さらに多くのイベントの詳細が存在している可能性があります。
> - *contentCreated* プロパティは、通知されるイベントが作成された日付ではありません。 通知が作成された日付です。 その BLOB で詳細が示されるイベントは、コンテンツ BLOB が作成されたときよりも相当前に作成されている可能性があります。 そのため、特定の期間内に発生したイベントについて API を直接照会することはできません。

### <a name="paging-contents-for-busy-tenants"></a>ビジー状態のテナントに対するコンテンツのページング

多くの大規模な Office 365 テナントでは、1 時間に数千ものイベントが生成されています。 これに該当する組織で、前述の例のように期間が 24 時間のクエリを実行すると、1 つの応答では返しきれないほどの通知の取得が必要になることがあります。 この場合、ある種の論理的なループの実装が必要になります。そのループでは、毎回、**NextPageUrl:** ヘッダー値について応答ヘッダーを調べます。 詳細については、Office 365 マネージメント アクティビティ API リファレンスの「[改ページ](office-365-management-activity-api-reference.md#pagination)」セクションを参照してください。 

このループのロジックは、次のようなものになります。

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

このループ コードのテストは、極度に活発なテナントが存在していないと難しくなります。 スクリプトで数千回の更新操作を実行してテストしてみましたが、**NextPageUrl** ヘッダーの送信が必要になるほどの数の通知を生成することができませんでした。

## <a name="using-webhooks"></a>Webhook の使用

コンテンツ BLOB が作成されたことを通知する方法は 2 つあります。 *プッシュ* アプローチは、Webhook エンドポイントによって実装されます。このエンドポイントは、ユーザーが作成する Web アプリケーションで、ユーザー自身またはクラウド プラットフォームでホストします。 Webhook は、監査対象のコンテンツ タイプに対するサブスクリプションを作成するときに登録します。 また、後述するアプローチを使用して、既存のサブスクリプションに Webhook の登録を追加することもできます。 *プル* アプローチでは、[/content 操作](office-365-management-activity-api-reference.md#list-available-content)を使用して、特定の期間 (24 時間以内) についてのクエリを実行する必要があります。 その応答によって、指定した期間中に作成されたコンテンツ BLOB が知らされます。

Webhook を追加する前に、次の 2 つの問題について注意してください。

1. Webhook は、デバッグやトラブルシューティングに難点があるため Microsoft では重要視されなくなっています。 通常、着信要求に応答する WebAPI エンドポイントはユーザーがホストすることになります。 多くのユーザーは、ホスティング環境 (ユーザーが完全には制御できない環境) またはオンプレミス環境 (着信 HTTP 要求の許可が困難な環境) のどちらかを使用します。 サポートでは、Office 365 監査パイプラインからの着信要求がファイアウォールやルーターによってブロックされるという多くの問題を確認しています。 この場合、API ではバックオフ アルゴリズムを実装することになりますが、このアルゴリズムは複雑になることがあり、サブスクリプションで Webhook が無効になる可能性があります。

2. Webhook は、開始操作の実行後に、検証要求に即座に応答できるように準備が整っている必要があります。 Webhook アプリケーションにバグがあると、検証に失敗して Webhook は無効になります。 検証要求スキーマの詳細については、Office 365 マネージメント アクティビティ API リファレンスの「[Webhook 検証](office-365-management-activity-api-reference.md#webhook-validation)」セクションを参照してください。 マネージメント アクティビティ API の通知に応答する実稼働可能な Webhook を作成する際の問題点について慎重に検討する必要があります。

Webhook を実装する場合は、最初に呼び出される Webhook エンドポイントを指定する /start 操作の前に、そのエンドポイントが検証要求と通常の通知要求の両方に HTTP 200 応答で応答する準備ができていることを検証するためのテストが必要です。 通常、この準備状況をテストするには、API からの疑似要求を使用します。 Office 365 マネージメント アクティビティ API リファレンスの「[Webhook 検証](office-365-management-activity-api-reference.md#webhook-validation)」セクションと「[コンテンツの取得](office-365-management-activity-api-reference.md#retrieving-content)」セクションの両方を慎重に読んで確認して、この 2 種類の要求のスキーマについて理解してください。

Webhook エンドポイントでサブスクリプションを追加する場合は、body パラメーターを /start エンドポイントへの POST に追加します。次に例を示します。

```json
$body = '{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }}'
$uri = "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed//subscriptions/start?contentType=Audit.SharePoint"
Invoke-RestMethod -Method Post -uri $uri -Headers $headerParams -Body $body
```

この呼出しの直後に、検証要求が `https://webhook.myapp.com/o365/ …` に送信されます。Office 365 マネージメント アクティビティ API リファレンスの「[Webhook 検証](office-365-management-activity-api-reference.md#webhook-validation)」セクションで説明されているように、この要求に応答できる状態のリスナーが存在している必要があります。 リスナーは、HTTP 200 で応答する必要があります。 この時点で即座に /list 操作を実行すると、検証が正常に返されるまで null として示される以外の Webhook は表示されません。

### <a name="checking-notifications-to-webhooks"></a>webhook への通知の確認

/notifications 操作と /content 操作は区別することが重要です。 通知の確認は、Webhook エンドポイントでサブスクライブした場合にのみ重要になります。 この操作により、Webhook への通知が成功したかどうかを確認できます。 この操作は、利用可能なコンテンツをリストするために使用しないでください。 すでに Webhook で受信している可能性のあるコンテンツが利用できるかどうかをクロスチェックする場合は、/content 操作を使用します。 ただし、[/notifications 操作](office-365-management-activity-api-reference.md#list-notifications)を使用して、失敗した通知について最初に確認しておく必要があります。

## <a name="requesting-content-blobs-and-throttling"></a>コンテンツ BLOB の要求と調整

コンテンツ URI のリストを取得したら、その URI で指定される BLOB を要求する必要があります。 次に、PowerShell を使用してコンテンツ BLOB を要求する例を示します。 この例は、この記事の「[アクセス トークンの取得](#getting-an-access-token)」セクションに示した例を使用してアクセス トークンを取得していることと、`$headerParams` 変数に適切な値が設定されていることを前提としています。

```powershell
# Get a content blob
$uri = 'https://manage.office.com/api/v1.0/<<your-tenant-guid>>/activity/feed/audit/<<ContentID>$audit_sharepoint$Audit_SharePoint'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

前述の例の *$uri* 変数に関して、次の事項に注目してください。

- PowerShell で *$* 記号が変数として解釈されないように、単一引用符を使用しています。
- URI 全体は、前の /content エンドポイントへの呼出しに対する応答の *contentUri* プロパティで返されます。 プレースホルダーのトークンは、単に説明のために示したものです。

利用可能なコンテンツ BLOB を取得しようとすると、多くのユーザー (ほとんどの場合は、ビジー状態のテナントを使用しているユーザー) に次のようなエラーが発生します。

```json
Response Code 403: {'error':{'code':'AF429','message':'Too many requests. Method=GetBlob, PublisherId=00000000-0000-0000-0000-000000000000'}}
```

これは、調整が原因になっていると考えられます。 PublisherId パラメーターの値に注目してください。この値は、クライアントが要求で *PublisherIdentifier* を指定していない可能性があることを示しています。 また、403 エラー応答に *PublisherId* と表示されていても、正しいパラメーター名は *PublisherIdentifier* である点にも注意が必要です。

> [!NOTE] 
> API リファレンスでは、どの API 操作にも *PublisherIdentifier* パラメーターが示されていますが、このパラメーターはコンテンツ BLOB の取得時の contentUri URL に対する GET 要求にも含める必要があります。

問題のトラブルシューティングのために単純な API 呼び出しを実行する場合は (たとえば、サブスクリプションがアクティブかどうかを確認する場合)、*PublisherIdentifier* パラメーターを省略してもかまいませんが、最終的に実稼働用に使用するコードでは、すべての呼び出しに必ず *PublisherIdentifier* パラメーターを含める必要があります。

会社のテナントに対応するクライアントを実装する場合、*PublisherIdentifier* はテナント GUID になります。 複数の顧客に対応する ISV アプリケーションまたはアドインを作成する場合、*PublisherIdentifier* は ISV のテナント GUID にする必要があります (エンド ユーザーの会社のテナント GUID ではありません)。

有効な *PublisherIdentifier* を含めると、テナントごとに 1 分あたり 60K の要求が割り当てられるプールに入れられます。 これは、莫大な数の要求です。 ただし、*PublisherIdentifier* パラメーターを含めていないと、すべてのテナントに対して 1 分あたり 60K の要求が割り当てられる汎用プールに入れられます。 この場合、呼び出しが調整される可能性が高くなります。 これを防止するために、*PublisherIdentifier* を使用してコンテンツ BLOB を要求する方法を示します。

```powershell
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

前述の例は、*$response* 変数が /content エンドポイントに対する要求の応答で設定されていることと、*$headerParams* 変数に有効なアクセス トークンが含まれていることを前提としています。 このスクリプトでは、応答からのコンテンツ URI の配列内で最初の項目を取得し、その BLOB をダウンロードするために GET を呼び出して、*$contents* 変数に格納します。 ユーザーのコードでは、*contentUri* ごとに GET を発行して、contentUri コレクション全体をループ処理することになります。

## <a name="frequently-asked-questions-about-the-office-365-management-api"></a>Office 365 マネージメント API についてよく寄せられる質問

#### <a name="what-is-the-maximum-time-i-will-have-to-wait-before-a-notification-is-sent-about-a-given-office-365-event"></a>特定の Office 365 イベントに関する通知が送信されるまでに必要な最長の待ち時間はどれくらいですか?

通知の配信について最長の待機時間に対する保証はありません (つまり、SLA はありません)。 Microsoft サポートの認識では、ほとんどの通知がイベントの発生から 1 時間以内に送信されます。 この待機時間は大幅に短くなることも、長くなることもあります。 ワークロードごとに多少の違いはありますが、原則的に、ほとんどの通知はイベントの発生から 24 時間以内に配信されます。

#### <a name="arent-webhook-notifications-more-immediate-after-all-arent-they-are-event-driven"></a>webhook 通知のほうが早くなりませんか? 結局のところ、イベント駆動型ではないですか?

いいえ。 Webhook 通知は、イベントによって通知がトリガーされるという意味ではイベント駆動ではありません。 コンテンツ BLOB の作成は依然として必要であり、コンテンツ BLOB の作成が通知の配信をトリガーします。 最近では、webhook の使用時の通知の待機時間は、/content 操作で API を直接クエリするよりも長くなっています。 そのため、マネージメント アクティビティ API は、リアルタイムのセキュリティ警告システムとして捉えることはできません。 Microsoft は、その目的のための別の製品を用意しています。 セキュリティに関する限り、マネージメント アクティビティ API のイベント通知は、長期間にわたる使用パターンを判断するために使用するほうが適しています。 

#### <a name="can-i-query-the-management-activity-api-for-a-particular-event-id-or-recordtype-or-other-properties-in-the-content-blob"></a>コンテンツ BLOB 内の特定のイベント ID や RecordType などのプロパティについてマネージメント アクティビティ API を照会できますか?

いいえ。 マネージメント アクティビティ API によって利用可能になるデータは、従来の意味での「ログ」と考えないでください。 それよりも、イベントの詳細についてのダンプと考えてください。 カスタムのアプリケーションやサード パーティ製のツールを使用して、これらのイベントの詳細をすべて収集し、ローカルに保存してインデックスを作成し、独自のクエリ ロジックを実装することは、ユーザーの裁量に任されています。

#### <a name="how-do-i-know-the-data-coming-from-my-existing-auditing-solution-which-collects-data-from-the-management-activity-api-is-accurate-and-complete"></a>マネージメント アクティビティ API からデータを収集する既存の監査アプリケーションのデータが正確で完全であることを確認する方法はありますか?

簡潔に答えると、Microsoft は特定のアプリケーションやサード パーティ (ISV) のアプリケーションをクロスチェックできるようなログは提供していません。 同じパイプラインからデータを取り出す Microsoft セキュリティ製品もありますが、そうした製品についての説明は、この記事の範囲外であり、マネージメント アクティビティ API を直接クロスチェックするために使用することはできません。 既存のソリューションが提供する内容と予測した内容の矛盾について懸念している場合は、前述の操作を実装する必要があります。 ただし、既存のツールやソリューションがデータをリストする方法とデータにインデックスを作成する方法によっては、これは困難なことになります。 既存のソリューションが実際のイベントの作成時刻で並べ替えたデータを表示するだけならば、結果セットを比較できるようにイベントの作成時刻で API を照会する方法は存在しません。 このシナリオでは、通知されたコンテンツ BLOB を数日間にわたって収集し、手動でインデックスを作成するか並べ替えてから、大まかな比較を実行する必要があります。

#### <a name="how-long-will-the-content-blobs-remain-available"></a>コンテンツ BLOB の利用可能期間はどれくらいですか?

コンテンツ BLOB は、コンテンツ BLOB が利用可能になったことが通知されてから 7 日間利用できます。 そのため、コンテンツ BLOB の作成に大幅な遅延があった場合は、コンテンツ BLOB が利用できなくなるまで、実際のイベント作成日の後に、それよりも長い時間 (遅延 + 7 日) 利用可能になります。

#### <a name="if-there-is-a-24-hour-delay-in-getting-a-notification-doesnt-that-mean-i-will-have-only-6-days-to-retrieve-the-content-blob"></a>通知されるまでに 24 時間の遅延があった場合、コンテンツ BLOB を取得するための期間は 6 日間しかないことになりますか?

いいえ。 通知が非常に長い期間遅延した場合でも (サービスの中断などの場合)、元のイベントに関連するコンテンツ BLOB をダウンロードする通知が最初に利用可能になってから 7 日間の期間があります。












