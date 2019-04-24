---
ms.TocTitle: Office 365 Management Activity API reference
title: Office 365 管理アクティビティ API リファレンス
description: Office 365 管理アクティビティ API は、Office 365 と Azure AD のアクティビティ ログから、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を取得するために使用します。
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: 01/10/2018
localization_priority: Priority
ms.openlocfilehash: e6675628a384ab4b2dac3342875332b50586526f
ms.sourcegitcommit: 5b1eaeb7f262b7b9f7ab30ccb9f10878814153ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "32223981"
---
# <a name="office-365-management-activity-api-reference"></a>Office 365 管理アクティビティ API リファレンス

Office 365 管理アクティビティ API は、Office 365 と Azure AD のアクティビティ ログから、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を取得するために使用します。 

Office 365 と Microsoft Azure Active Directory の監査ログとアクティビティ ログに記録されたアクションとイベントを使用して、監視、分析、およびデータ可視化を提供するソリューションを作成できます。 このソリューションにより、企業はそのコンテンツに対して実行されたアクションの可視性を向上させることができます。 これらのアクションとイベントは、Office 365 アクティビティ レポートからも入手できます。 詳細については、「[Office 365 セキュリティ/コンプライアンス センターで監査ログを検索する](https://support.office.com/ja-JP/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c)」を参照してください。

Office 365 管理アクティビティ API は、REAT Web サービスの 1 つであり、任意の言語と、HTTPS および X.509 証明書をサポートするホスト環境を用いて、ソリューションの開発に使用できます。この API は、認証と承認に Azure AD と OAuth2 プロトコルを使用します。アプリケーションからこの API にアクセスする場合は、まず Azure AD で登録し、適切なアクセス許可で設定する必要があります。これにより、アプリケーションで、API を呼び出すために必要な OAuth2 アクセス トークンを要求できます。詳細については、「[Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。

> [!NOTE] 
> Office 365 管理アクティビティ API で返されるデータのスキーマについては、「[Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)」を参照してください。


## <a name="working-with-the-office-365-management-activity-api"></a>Office 365 管理アクティビティ API の操作

Office 365 管理アクティビティ API は、アクションとイベントを、タイプ別およびコンテンツのソース別に分類されたテナント固有コンテンツ blob に集約します。現時点では、次のコンテンツ タイプがサポートされています。

- Audit.AzureActiveDirectory
    
- Audit.Exchange
    
- Audit.SharePoint
    
- Audit.General (上記のコンテンツ タイプに含まれない、その他すべてのワーク ロードが含まれます)

- DLP.All (すべてのワークロードの DLP イベントのみ)
    
イベントおよびこれらのコンテンツ タイプに関連付けられているプロパティの詳細については、「[Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)」を参照してください。

テナントのコンテンツ blob の取得を開始するには、まず目的のコンテンツ タイプのサブスクリプションを作成します。複数のテナントのコンテンツ blob を取得する場合は、テナントごとに 1 つずつ、目的の各コンテンツ タイプの複数のサブスクリプションを作成します。

サブスクリプションを作成したら、ダウンロードできる新しいコンテンツ blob を発見するために定期的にポーリングできます。または Webhook エンドポイントをサブスクリプションに登録して、新しいコンテンツ blob が入手可能になったときにそのエンドポイントで通知を受け取ることができます。


> [!NOTE] 
> サブスクリプションを作成した場合、最初のコンテンツ BLOB がそのサブスクリプションで利用可能になるには、最大で 12 時間かかることがあります。 blob コンテンツは、複数のサーバーとデータセンターにまたがってアクションとイベントを収集および集約することで作成されます。 この分散プロセスの結果として、コンテンツ blob に入れられたイベントとアクションは、必ずしも発生した順序で表示されるとは限りません。 コンテンツ blob によっては、それよりも前のコンテンツ blob に入っているものよりも前に発生したアクションとイベントが含まれる場合があります。 アクションとイベントの発生時からそれらをコンテンツ blob 内で参照できるようになるまでの遅延時間は短縮が図られていますが、発生順での表示は保証できません。


> [!NOTE] 
> DLP 機密データは、「DLP 機密データの読み取り」アクセス許可が付与されたユーザーが、アクティビティ フィード API でのみ利用できます。 データ損失防止 (DLP) の詳細については、「[データ損失防止ポリシーの概要](https://support.office.com/ja-JP/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)」を参照してください。

## <a name="activity-api-operations"></a>アクティビティ API の操作

すべての API 操作のスコープは単一のテナントであり、API のルート URL にはテナント コンテキストを示すテナント ID が含まれています。テナント ID は、GUID です。GUID を取得する方法の詳細については、「[Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

Webhook に送信される通知には**テナント ID** が含まれるため、同じ Webhook を使用してすべてのテナントの通知を受け取ることができます。

すべての API 操作には、Azure AD から取得したアクセス トークンを使用する認証 HTTP ヘッダーが必要です。アクセス トークンのテナント ID は、API のルート URL 内のテナント ID と一致する必要があり、アクセス トークンには、ActivityFeed.Read 要求 (Azure AD でアプリケーションに対して設定したアクセス許可 [組織のアクティビティ データの読み取り] に相当) が含まれている必要があります。

```json
Authorization: Bearer eyJ0e...Qa6wg
```

アクティビティ API は、次の操作をサポートします。

- **サブスクリプションの開始**。テナントの通知の受け取りとアクティビティ データの取得を開始します。
    
- **サブスクリプションの停止**。テナントのデータの取得を中止します。
    
- **現在のサブスクリプションのリストの作成**
    
- **利用可能なコンテンツのリストの作成**。これには対応するコンテンツの URL も含まれます。
    
- **通知の受け取り**。この通知は新しいコンテンツが利用可能になったときに Webhook により送信されます。
    
- **コンテンツの取得**。コンテンツ URL を使用して実行します。
    
- **通知のリストを作成**。この通知は Webhook によって送信されます。

- **リソースのフレンドリ名の取得**。GUID で識別されるデータ フィード内のオブジェクトに関して実行します。
    

## <a name="start-a-subscription"></a>サブスクリプションの開始

この操作は、指定したコンテンツ タイプのサブスクリプションを開始します。指定したコンテンツ タイプのサブスクリプションが既に存在する場合、この操作は次の目的で実行します。

- アクティブな Webhook のプロパティを更新します。
    
- 失敗通知数の超過により無効になった Webhook を有効にします。
    
- 新しい (または null の) 有効期限日を指定することで、有効期限切れの Webhook を再度有効にします。
    
- Webhook を削除します。
    
||サブスクリプション|説明|
|:-----|:-----|:-----|
|**パス**| `/subscriptions/start?contentType={ContentType}`||
|**パラメーター**|contentType|有効なコンテンツ タイプである必要があります。|
||PublisherIdentifier|API に対するコードを作成するベンダーのテナント GUID。 これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。 このパラメーターは、要求率の調整に使用します。 専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。 このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。|
|**Body**|webhook|次の 3 つのプロパティが指定された、オプションの JSON オブジェクト:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>address</b>: Required HTTPS endpoint that can receive notifications.  A test message will be sent to the webhook to validate the webhook before creating the subscription.</p></li><li><p><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</p></li><li><p><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</p></li></ul>|
|**Response**|contentType|呼び出しで指定するコンテンツ タイプ。|
||status|サブスクリプションの状態。サブスクリプションが無効の場合、コンテンツを取得したりそのリストを作成したりすることはできません。|
||webhook|Webhook の状態と一緒に、呼び出しに指定される Webhook のプロパティ。Webhook が無効である場合、通知は受け取りませんが、サブスクリプションが有効であれば、コンテンツを取得したりそのリストを作成したりできます。|

#### <a name="sample-request"></a>要求のサンプル

```json
POST {root}/subscriptions/start?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Content-Type: application/json; utf-8
Authorization: Bearer eyJ0e...Qa6wg

{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }
}

```


#### <a name="sample-response"></a>応答のサンプル

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
    "contentType": "Audit.SharePoint",
    "status": "enabled",
    "webhook": {
        "status": "enabled",
        "address":  "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": null
    }
}

```


## <a name="webhook-validation"></a>Webhook の検証

/Start 操作が呼び出され、Webhook が指定されると、アクティブ リスナーが通知を受け入れて処理できることを検証するために、指定された Webhook アドレスに検証通知が送信されます。HTTP 200 OK 応答が返信されない場合は、サブスクリプションは作成されません。または、Webhook を既存のサブスクリプションに追加するために /start が呼び出されているものの、HTTP 200 OK の応答が返信されない場合は、Webhook は追加されず、サブスクリプションは変更されません。

#### <a name="sample-request"></a>要求のサンプル

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId) if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a>応答のサンプル

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a>サブスクリプションの停止

この操作は、指定したコンテンツ タイプのサブスクリプションを停止します。 

サブスクリプションを停止すると、通知を受け取ることはなくなり、利用可能なコンテンツを取得することはできません。サブスクリプションを後で再開すると、その時点から新しいコンテンツにアクセスできるようになります。サブスクリプションが停止して再開するまでの間に使用可能であったコンテンツは取得できません。


||サブスクリプション|説明|
|:-----|:-----|:-----|
|**パス**| `/subscriptions/stop?contentType={ContentType}`||
|**パラメーター**|contentType|有効なコンテンツ タイプである必要があります。|
||PublisherIdentifier|API に対するコードを作成するベンダーのテナント GUID。 これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。 このパラメーターは、要求率の調整に使用します。 専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。 このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。|
|**Body**|(空)||
|**応答**|(空)|||

#### <a name="sample-request"></a>要求のサンプル

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>応答のサンプル

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a>現在のサブスクリプションのリストの作成

この操作は、現在のサブスクリプションのコレクションと、関連する Webhook を返します。

||サブスクリプション|説明|
|:-----|:-----|:-----|
|**パス**| `/subscriptions/list`||
|**パラメーター**|PublisherIdentifier|API に対するコードを作成するベンダーのテナント GUID。 これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。 このパラメーターは、要求率の調整に使用します。 専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。 このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。|
|**Body**|(空)||
|**応答**|JSON 配列|各サブスクリプションは、次の 3 つのプロパティが指定された JSON オブジェクトで表されます。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b>:コンテンツ タイプを示します。</p></li><li><p><b>status</b>: Indicates the status of the subscription.</p></li><li><p><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.  If a subscription does not have a webhook, the webhook property will be present but with null value.</p></li></ul>|


#### <a name="sample-request"></a>要求のサンプル

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>応答のサンプル

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType" : "Audit.SharePoint",
        "status": "enabled",
        "webhook": {
            "status": "enabled",
            "address": "https://webhook.myapp.com/o365/",
            "authId": "o365activityapinotification",
            "expiration": null
        }
    },

    ...

    {
        "contentType": "Audit.Exchange",
        "webhook": null
    }
]

```


## <a name="list-available-content"></a>利用可能なコンテンツのリストの作成

この操作は、指定したコンテンツ タイプの、現在取得可能なコンテンツのリストを作成します。コンテンツは、複数のデータセンターにある複数のサーバーから収集されたアクションとイベントの集約です。コンテンツは、集約が利用可能になった順にリストされされますが、集約内のイベントとアクションは必ずしも連続的にはなりません。サブスクリプションの状態が無効である場合は、エラーが返されます。


||サブスクリプション|説明|
|:-----|:-----|:-----|
|**パス**| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**パラメーター**|contentType|有効なコンテンツ タイプである必要があります。|
||PublisherIdentifier|API に対するコードを作成するベンダーのテナント GUID。 これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。 このパラメーターは、要求率の調整に使用します。 専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。 このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。|
||startTime endTime|Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available. The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>YYYY-MM-DD</p></li><li><p>YYYY-MM-DDTHH:MM</p></li><li><p>YYYY-MM-DDTHH:MM:SS</p></li></ul>開始時刻と終了時刻の両方を指定する (または両方を省略する) 必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。 By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.<p>**注**: 24 時間よりも長い間隔になる startTime と endTime を指定することもできますが、そのような設定はお勧めできません。 さらに、24 時間よりも長い間隔の要求に対する応答で結果が得られたとしても、部分的な結果になっている可能性があり、結果と見なすべきではありません。 要求の発行の際には、間隔が 24 時間以内になる startTime と endTime を指定してください。</p>|
|**Response**|JSON 配列|利用可能なコンテンツは、次のプロパティが指定された JSON オブジェクトで表されます。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b>:コンテンツ タイプを示します。</p></li><li><p><b>contentId</b>:コンテンツを一意に識別する、符号化文字列です。</p></li><li><p><b>contentUri</b>:コンテンツを取得するときに使用する URL です。</p></li><li><p><b>contentCreated</b>:コンテンツが利用可能になった日付/時刻です。</p></li><li><p><b>contentExpiration</b>:コンテンツ取得の締切となる日付/時刻です。</p></li></ul>|


#### <a name="sample-request"></a>要求のサンプル

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>応答のサンプル

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


### <a name="pagination"></a>改ページ

ある時間範囲の利用可能なコンテンツのリストを作成する場合、返される結果の数は、応答のタイムアウトを防ぐために制限されます。指定の時間範囲内に 1 つの応答で返せるよりもより多くの結果がある場合、結果は切り捨てられ、次ページの結果を取得するために使用する URL を示すヘッダーが応答に追加されます。この URL には、元の要求に指定されているのと同じ _startTime_ および _endTime_ パラメーターと、次ページの内部 ID を示すパラメーターが含まれます。元の要求で _startTime_ と _endTime_ が指定されていなかった場合、それらは元の要求が出された時点に先行する 24 時間間隔を反映するように設定されます。


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

指定の時間の範囲にある利用可能なすべてのコンテンツのリストを作成するために、**NextPageUri** ヘッダーがない応答を受信するまで、複数のページを取得することが必要になる場合があります。


## <a name="receiving-notifications"></a>通知の受け取り

新しいコンテンツが利用可能になると、サブスクリプションの設定済み Webhook に通知が送信されます。通知にはテナント ID が含まれるので、同じ Webhook を使用して、サブスクリプションがあるすべてのテナントの通知を受け取ることができます。

通知は、指定の Webhook アドレスに HTTP POST over TLS (TLS 1.0 以降のバージョン) として行われます。 Webhook 構成に認証 ID が含まれている場合、HTTP ヘッダー Webhook-AuthID として送信されます。 HTTP 200 OK 以外の応答はエラーと見なされ、通知が再試行されます。 クライアント証明書ベースの認証を要求するように Webhook を設定することもでき、manage.office.com 証明書を使用して認証されます。

要求の本文には、利用可能なコンテンツ blob を表す、1 つ以上の JSON オブジェクトの配列が含まれます。通知を比較的小さいサイズにしておくために、各通知内のコンテンツ blob の数は制限されています。この制限は変更される場合があるので、実装では、固定サイズを前提とするのではなく、配列の長さを照会する必要があります。各オブジェクトには、/content 操作によって返されたのと同じプロパティ、データが属するテナントの GUID、およびサブスクリプションを作成したアプリケーションの GUID が含まれます。これにより、Webhook は、複数のテナントとアプリケーションでの使用中に、コンテキストを確立することができます。

- **tenantId**:コンテンツが属するテナントの GUID です。
    
- **clientId**:サブスクリプションを作成したアプリケーションの GUID です。
    
- **contentType**:コンテンツ タイプを示します。
    
- **contentId**:コンテンツを一意に識別する、符号化文字列です。
    
- **contentUri**:コンテンツを取得するときに使用する URL です。
    
- **contentCreated**:コンテンツが利用可能になった日付/時刻です。
    
- **contentExpiration**:コンテンツ取得の締切となる日付/時刻です。
    
通知の例を次に示します。

```json
POST https://webhook.myapp.com/o365/ 
Content-Type: application/json; utf-8
Webhook-AuthID: o365activityapinotification

[
    {
        "tenantId": "{GUID}"
        "clientId": "{GUID}"
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


## <a name="notification-failure-and-retry"></a>通知の失敗および再試行

通知システムは、新しいコンテンツが利用可能になったときに通知を送信します。 通知の送信時に何度も障害が発生した場合は、再試行メカニズムによって再試行の間隔が指数関数的に長くなります。 障害が継続的に発生する場合、Webhook が無効にされ、通知の送信が完全に停止されることがあります。 /start 操作を実行すると、無効にされた Webhook を再度有効にできます。


## <a name="retrieving-content"></a>コンテンツの取得

コンテンツ blob を取得するには、利用可能なコンテンツのリストと Webhook に送信された通知に含まれている、対応するコンテンツ URI に対して GET 要求を行います。返されるコンテンツは、JSON 形式の、1 つ以上のアクションまたはイベントのコレクションになります。

#### <a name="sample-request"></a>要求のサンプル

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a>応答のサンプル

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "CreationTime": "2015-06-29T20:03:19",
        "Id": "80c76bd2-9d81-4c57-a97a-accfc3443dca",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "failed",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "ExtendedProperties": [
            {
                "Name": "LoginError",
                "Value": "-2147217390;PP_E_BAD_PASSWORD;The entered and stored passwords do not match."
            }
        ],
        "Client": "Exchange",
        "LoginStatus": -2147217390,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:03:34",
        "Id": "4e655d3f-35fa-42e0-b050-264b2d255c7a",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "success",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Client": "Exchange",
        "LoginStatus": 0,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:04:55",
        "Id": "b567caf0-088e-4c1c-a4ea-633a1e3d66c8",
        "Operation": "Add User.",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 8,
        "ResultStatus": "success",
        "UserKey": "1003BFFD8EC47CA6@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ObjectId": "user001@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Actor": [
            {
                "ID": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
                "Type": 2
            },
            {
                "ID": "admin@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "1003BFFD8EC47CA6",
                "Type": 3
            }
        ],
        "ActorContextId": "41463f53-8812-40f4-890f-865bf6e35190",
        "InterSystemsId": "c2ced078-ad57-4079-a743-5c37f5284790",
        "IntraSystemId": "d1497f7e-15b4-49aa-83ad-11a17ca4a2f4",
        "Target": [
            {
                "ID": "user001@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "10037FFE91510806",
                "Type": 3
            }
        ],
        "TargetContextId": "41463f53-8812-40f4-890f-865bf6e35190"
    }
]

```


## <a name="list-notifications"></a>通知のリスト作成

この操作では、指定したコンテンツ タイプのすべての通知の試行についてのリストが作成されます。 コンテンツ タイプへのサブスクリプションを開始するときに Webhook を含めなかった場合は、取得される通知はありません。 通知の再試行が障害発生時に行われるため、この操作では同じコンテンツ対する複数の通知が返される場合があり、通知が送信される順序は、コンテンツが利用可能になった順序と必ずしも一致しません (特に障害と再試行が複数回繰り返される場合はそうなります)。 

この操作は、Webhook と通知に関連する問題の調査に使用できますが、どのコンテンツが現在取得可能であるかを特定するためには使用しないでください。 その場合は代わりに、/content 操作を実行します。 サブスクリプションの状態が無効である場合は、エラーが返されます。


||サブスクリプション|説明|
|:-----|:-----|:-----|
|**パス**| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**パラメーター**|contentType|有効なコンテンツ タイプである必要があります。|
||PublisherIdentifier|API に対するコードを作成するベンダーのテナント GUID。 これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。 このパラメーターは、要求率の調整に使用します。 専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。 このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。|
||startTime endTime|コンテンツが利用可能になったときを基点として、コンテンツが返される時間の範囲を示す、オプションの日付/時刻 (UTC)。 この時間の範囲には、_startTime_ (_startTime_ <= contentCreated) は含まれ、_endTime_ (_contentCreated_ < endTime) は含まれません。これにより、利用可能なコンテンツのページングに、重複することのない増分の時間間隔を使用できます。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>YYYY-MM-DD</p></li><li><p>YYYY-MM-DDTHH:MM</p></li><li><p>YYYY-MM-DDTHH:MM:SS</p></li></ul>開始時刻と終了時刻の両方を指定する (または両方を省略する) 必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。 By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.|
|**Response**|JSON 配列|通知は、次のプロパティが指定された JSON オブジェクトで表されます。 <ul><li>**contentType**: コンテンツ タイプを示します。</li><li>**contentId**: コンテンツを一意に識別する、符号化文字列です。</li><li>**contentUri**: コンテンツを取得するときに使用する URL です。 </li><li>**contentCreated**: コンテンツが利用可能になった日付/時刻です。</li><li>**contentExpiration**: コンテンツ取得の締切となる日付/時刻です。</li><li>**notificationSent**: 通知が送信された日付/時刻です。</li><li>**notificationStatus**: 通知の試行の成功または失敗を示します。</li></ul>|

#### <a name="sample-request"></a>要求のサンプル

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>応答のサンプル

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z",
        "notificationSent": "2015-05-23T17:36:00.000Z",
        "notificationStatus": "success"

    },
    ...
]

```


### <a name="pagination"></a>改ページ

ある時間範囲の通知履歴のリストを作成する場合、返される結果の数は、応答のタイムアウトを防ぐために制限されます。指定の時間範囲内に 1 つの応答で返せるよりもより多くの結果がある場合、結果は切り捨てられ、次ページの結果を取得するために使用する URL を示すヘッダーが応答に追加されます。この URL には、元の要求に指定されているのと同じ _startTime_ および _endTime_ パラメーターと、次ページの内部 ID を示すパラメーターが含まれます。元の要求で _startTime_ と _endTime_ が指定されていなかった場合、それらは元の要求が出された時点に先行する 24 時間間隔を反映するように設定されます。

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

指定の時間の範囲にある利用可能なすべてのコンテンツのリストを作成するために、**NextPageUrl** ヘッダーがない応答を受信するまで、複数のページを取得することが必要になる場合があります。

## <a name="retrieve-resource-friendly-names"></a>リソースのフレンドリ名を取得します。

この操作は、GUID で識別されるデータ フィード内のオブジェクトのフレンドリ名を取得します。 現時点でサポートされているオブジェクトは "DlpSensitiveType" のみです。 


||サブスクリプション|説明|
|:-----|:-----|:-----|
|**パス**| `/resources/dlpSensitiveTypes`||
|**パラメーター**|PublisherIdentifier|API に対するコードを作成するベンダーのテナント GUID。 これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。 このパラメーターは、要求率の調整に使用します。 専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。 このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。|
|**ヘッダー**|Accept-Language|Header to specify the desired language for localized names. For example, use "en-US" for English or "es" for Spanish. The default language (en-US) will be returned if this header is not present.|
|**Body**|(空)||
|**応答**|JSON 配列|利用可能なコンテンツは、次のプロパティが指定された JSON オブジェクトで表されます。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>id</b>: Indicates the guid of the sensitive information type.</p></li><li><p><b>name</b>: The friendly name of the sensitive information type.</p></li></ul>|

#### <a name="sample-request"></a>要求のサンプル

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a>応答のサンプル

```json
HTTP/1.1 200 OK

[
    {
        "id": "50842eb7-edc8-4019-85dd-5a5c1f2bb085",
        "name": "CreditCardNumber"
    }, 
    {
        "id": "0e9b3178-9678-47dd-a509-37222ca96b42",
        "name": "EUDebitCardNumber"
    }, 
    ...
    {
    }
]

```

## <a name="api-throttling"></a>API 調整

API に対するコードを作成する各ベンダーには、1 分当たり 60K の要求調整のために専用クオータが割り当てられています。 専用クオータを取得するには、すべての要求でパラメーター PublisherIdentifier を指定します。 PublisherIdentifier が同じ要求は、同一のクオータを共有します。 PublisherIdentifier が指定されていないすべての要求は、GUID 00000000-0000-0000-0000-000000000000 と同じクオータを共有するようになります。

特定の問題で Office 365 がユーザーへの逆エスカレートを必要としている場合は、PublisherIdentifier として使用されている GUID を持つテナントのサブスクリプションが現行であり、正しい連絡先情報で更新されていることを確認してください。 このテナントに対するサブスクリプション要件はありません。

この API を使用して独自のソリューションを開発するユーザーは、制限のある共有クオータによる競合を回避するために独自のテナント GUID を使用してください。

> [!NOTE] 
> それぞれのパブリッシャーが最大 1 分あたり 60k の要求を送信できますが、Microsoft は応答速度を保証できません。 応答速度は、クライアント システムのパフォーマンス、ネットワーク容量、ネットワーク速度など、さまざまな要因によって決まります。  パブリッシャーは最大 1 分当たり 60K の要求を送信できますが、60k の要求に対するすべての応答が同時 (同じ分内) に受信できると期待してはいけません。 パブリッシャーがクライアント アプリケーションをベンチマークする必要がある場合は、そのクライアント アプリケーションの稼働を予定している各種環境でベンチマークを実行する必要があります。これは、環境ごとに結果が異なるためです。

## <a name="errors"></a>エラー

サービスでエラーが検出されると、標準の HTTP エラー コードの構文を使用して、エラー応答コードが呼び出し元に報告されます。失敗した呼び出しの本体には、追加情報が単一の JSON オブジェクトとして含められます。完全な JSON エラー本体の例を以下に示します。 

```json

{ 
    "error":{ 
        "code":"AF50000",
        "message": "An internal server error occurred. Retry the request."
    } 
}

```


|||
|:-----|:-----|
|コード|メッセージ|
|AF10001|要求で送信されたアクセス許可セット ({0}) に、必要なアクセス許可 **ActivityFeed.Read** が含まれていませんでした。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = the permission set in the access token.</p></li></ul>|
|AF20001|Missing parameter: {0}. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = 不足しているパラメーターの名前。</p></li></ul>|
|AF20002|無効なパラメーターの種類です: {0}。 予期される種類: {1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = the name of the invalid parameter.</p></li><li><p>{1} = the expected type (int, datetime, guid).</p></li></ul>|
|AF20003|指定した有効期限 {0} は、過去の日付と時刻に設定されています。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = API 呼び出しに渡される有効期限。</p></li></ul>|
|AF20010|URL ({0}) で渡されたテナント ID が、アクセス トークン ({1}) で渡されたテナント ID と一致しません。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = tenant ID passed in the URL</p></li><li><p>{1} = tenant ID passed in the access token</p></li></ul>|
|AF20011|指定したテナント ID ({0}) は、システムに存在しないか、削除されています。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   {0} = tenant ID passed in the URL</p></li></ul>|
|AF20012|指定したテナント ID ({0}) が、システムで正しく構成されていません。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    {0} = tenant ID passed in the URL</p></li></ul>|
|AF20013|URL ({0}) で渡されたテナント ID は、有効な GUID ではありません。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> {0} = tenant ID passed in the URL</p></li></ul>|
|AF20020|指定したコンテンツ タイプが無効です。|
|AF20021|The webhook endpoint {{0}) could not be validated. {1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = webhook address.</p></li><li><p>{1} = "The endpoint did not return HTTP 200." or "The address must begin with HTTPS."</p></li></ul>|
|AF20022|指定したコンテンツ タイプのサブスクリプションがありません。|
|AF20023|The subscription was disabled by {0}.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = "テナント管理" または "サービス管理"</p></li></ul>|
|AF20030|開始時刻と終了時刻の両方を指定する (または両方を省略する) 必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。|
|AF20031|Invalid nextPage Input: {0}.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = URL に渡された次ページ インジケーター</p></li></ul>|
|AF20050|指定された ID が存在しません。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = リソース ID またはリソース URL。</p></li></ul>|
|AF20051|Content requested with the key {0} has already expired. Content older than 7 days cannot be retrieved.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>•    {0} = resource id or resource URL</p></li></ul>|
|AF20052|URL 内のコンテンツの ID {0} は無効です。<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = リソース ID またはリソース URL。</p></li></ul>|
|AF20053|Accept-Language ヘッダーには、1 つの言語のみ表示可能です。|
|AF20054|Accept-Language ヘッダーに無効な構文があります。|
|AF429|要求数が多すぎます。 メソッド={0}, PublisherId={1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = HTTP メソッド</p></li><li><p>{1} = PublisherIdentifier として使用されたテナント GUID</p></li></ul>|
|AF50000|内部エラーが発生しました。要求を再試行してください。|
