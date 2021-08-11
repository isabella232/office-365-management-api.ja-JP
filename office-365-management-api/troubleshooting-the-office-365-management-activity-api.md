---
ms.technology: o365-service-communications
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Office 365 マネージメント アクティビティ API のトラブルシューティング
description: Office 365 マネージメント アクティビティ API のサポートについて Microsoft サポートに最も多く寄せられる質問のまとめです。
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 086b40d0207fba761db66d918d74dc872ae66c9471ceced91d2b4b6dfe73ac1e
ms.sourcegitcommit: 88ef5f75a9e2a25760a2caa2cef1f51f9afba90c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2021
ms.locfileid: "54274351"
---
# <a name="office-365-management-activity-api-faqs-and-troubleshooting"></a>Office 365 マネージメント アクティビティ API の FAQ とトラブルシューティング

Office 365 マネージメント アクティビティ API （*統合監査 API* とも呼ばれます） は、Office 365 のセキュリティおよびコンプライアンス製品の一部です:

- 複数の監査パイプライン ワークロード (SharePoint や Exchange など) にプログラムでアクセスできます

- 監査データの集計およびインデックス作成のために、広範なサード パーティ ベンダーによって使用されるメイン インターフェイスです

マネージメント アクティビティ API を Office 365 サービス コミュニケーション API と混同しないでください。 マネージメント アクティビティ API は、各種のワークローでのエンド ユーザーのアクティビティを監査するためのものです。 サービス コミュニケーション API は、Office 365 で利用可能なサービス (Dynamics CRM や ID サービスなど) によって送信される状態やメッセージを監査するためのものです。
 
> [!NOTE]
> 2020 年 10 月 22 日から 2020 年 11 月 6 日までの間に、Audit.AzureActiveDirectory コンテンツ タイプに属するイベントがOffice 365 マネージメント アクティビティ API を介して利用できないという問題がありました。 Azure AD サインイン イベントは、この問題の影響を受けませんでした。 影響期間中の不足しているイベントは、今後数日間で利用可能になり、2020 年 11 月 20 日までに完了すると予想されます。 場合によっては、2020 年 10 月 26 日から 2020 年 11 月 5 日までの間に生成されたイベントの重複イベントデータが発生することがあります。

## <a name="frequently-asked-questions-about-the-office-365-management-activity-api"></a>Office 365 マネージメント アクティビティ API についてよく寄せられる質問

**どのようにすればマネージメント アクティビティ API の使用を開始できますか?**

Office 365 マネージメント アクティビティ API の使用を開始する方法については、「[Office 365マネジメントAPI の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。

**Office 365 組織の監査を無効にするとどうなりますか? マネージメント アクティビティ API を介してイベントを引き続き取得できますか?**

いいえ。 管理アクティビティ API を介してレコードを取得するには、組織の Office 365 統合監査を有効にする必要があります。 手順については、[監査ログの検索を有効または無効にする](https://docs.microsoft.com/microsoft-365/compliance/turn-audit-log-search-on-or-off)を参照してください。

**特定の Office 365 サービスについて、どのイベントが監査されますか?**

総合的なイベントの一覧は、Office 365 マネージメント アクティビティ API スキーマのドキュメントに記載されています。 詳細については、「Office 365 マネージメント アクティビティ API のスキーマ」を参照してください。 また、監査されているほとんどの Office 365 サービスのイベント・リストについては、[セキュリティ/コンプライアンス センターで監査ログを検索する](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#audited-activities)も参照してください。

**マネージメント アクティビティ API でフェッチされたレコードと、Microsoft 365 コンプライアンス センターの監査ログの検索ツールを使用して返されたレコードに違いはありますか?**

どちらの方法でも、同じデータが返されます。 唯一の違いは、API の場合は、過去7日間しかデータを取得できないことです (以下の質問の詳細については、以下を参照してください)。 セキュリティ & コンプライアンスセンターで監査ログを検索する場合 (または、対応する **Search-UnifiedAuditLog** コマンドレットを Exchange Online PowerShell で使用する)、データが生成されたときに有効な保持期間の間データを取得することができます (たとえば、90日間や1年間)。

**特定の Office 365 イベントに関する通知が送信されるまでに必要な最長の待ち時間はどれくらいですか?**

通知の配信について最長の待機時間に対する確証はありません (つまり、SLA はありません)。 通常、ほとんどの通知は1時間以内に送信されます。 多くの場合、遅延時間は大幅に短くなりますが、この期間はワークロード間で異なるので、長くなる場合もあります。

**webhook 通知のほうが早くないですか?**

いいえ。 最近では、Webhook の使用時の通知の待機時間は、`/content`操作で API を直接クエリするよりも長くなっています。

**コンテンツはいつまでAPI を使用して取得し、利用可能ですか?**

コンテンツは、コンテンツが使用可能であることを通知してから 7 日間は、API を使用して取得できます。通知が非常に長い期間遅延した場合でも (サービスの中断などの場合)、元のイベントに関連するコンテンツ BLOB をダウンロードする通知が最初に利用可能になってから 7 日間の期間があります。

**コンテンツ BLOB 内の特定のイベント ID や RecordType などのプロパティについてマネージメント アクティビティ API を照会できますか?**

いいえ。 マネジメントアクティビティ API は、特定のログのすべてのイベントの詳細を提供します。 詳細すべてをダウンロードするために使用できます。それから、ダウンロードしたデータに独自のクエリロジックを実装することもできます。たとえば、カスタムアプリケーションやサードパーティ製のツールを使用できます。

**マネージメント アクティビティ API からデータを収集する既存の監査アプリケーションのデータが正確で完全であることを確認する方法はありますか?**

簡潔に答えると、Microsoft は特定のアプリケーションやサード パーティ (ISV) のアプリケーションをクロスチェックできるようなログは提供していません。 同じパイプラインからデータを取り出す Microsoft セキュリティ製品もありますが、そうした製品についての説明は、この記事の範囲外であり、マネージメント アクティビティ API を直接クロスチェックするために使用することはできません。 既存のソリューションが提供する内容と予測した内容の矛盾について懸念している場合は、前述の操作を実装する必要があります。 ただし、既存のツールやソリューションがデータをリストする方法とデータにインデックスを作成する方法によっては、これは困難なことになります。 既存のソリューションが実際のイベントの作成時刻で並べ替えたデータを表示するだけならば、結果セットを比較できるようにイベントの作成時刻で API を照会する方法は存在しません。 このシナリオでは、通知されたコンテンツ BLOB を数日間にわたって収集し、手動でインデックスを作成するか並べ替えてから、手動で比較を実行する必要があります。

**マネージメント アクティビティ API の調整制限とは何ですか?**

すべての組織には、最初に 1 分あたり 2,000 件の要求のベースラインが割り当てられます。 調整制限は、組織の座席数などの要因の組み合わせに基づいて調整されます。 Office 365 E5 およびMicrosoft 365 E5組織は、E5 以外の組織の約 2 倍の帯域幅を利用できます。 また、サービスの正常性を保護するために、最大帯域幅の上限も設定されます。

> [!NOTE]
> それぞれのテナントは最初に最大 1 分あたり 2,000 の要求を送信できますが、Microsoft は応答速度を保証できません。 応答速度は、クライアント システムのパフォーマンス、ネットワーク容量、ネットワーク速度など、さまざまな要因によって決まります。

**マネージメント アクティビティ API で調整エラーが発生しました。何をすべきですか?**

Microsoft サポートでチケットを開いて、新しい調整制限を要求してください。また、制限の引き上げに対する業務上の正当な理由を含めてください。 要求を審査し承諾されると、調整制限が引き上げられます。

**Azure Active Directory アクティビティの監査ログで TargetUpdatedProperties が ExtendedProperties に含まれなくなったのはなぜですか?**

TargetUpdatedProperties は ExtendedProperties に表示されていました。これが ExtendedProperties から削除され、現在では ModifiedProperties に表示されるようになりました。

**マネージメント アクティビティ API を介して Active Directory (Azure AD) サインイン アクティビティの UserAccountNotFound「LogonError」の監査ログを利用できないのはなぜですか?**

2020 年 11 月以降、Azure AD サインイン アクティビティの監査ログは、Azure AD Event Hubs から統合監査ログに取り込まれます。 この変更の結果、「LogonError」プロパティに UserAccountNotFound 値を入力することはできません。 2021 年 2 月の第 1 週から、[Azure AD ログオン監査スキーマの ErrorCode プロパティ](https://docs.microsoft.com/office/office-365-management-api/office-365-management-activity-api-schema#azure-active-directory-secure-token-service-sts-logon-schema)が [AADSTS エラー コード](https://docs.microsoft.com/azure/active-directory/develop/reference-aadsts-error-codes#lookup-current-error-code-information)と一致するようになりました。 また、UserAccountNotFound エラーのログイン試行時のユーザー名は、組織の Azure AD ディレクトリに存在しないため、UserId パラメーターに入力されません。

## <a name="troubleshooting-the-office-365-management-activity-api"></a>Office 365 マネージメント アクティビティ API のトラブルシューティング

Office 365 マネージメント アクティビティ API の入門者が明確にしておく必要のあることの 1 つは、イベントが発生した日付、イベントの発生元になる可能性のあるサイト コレクション、イベントの種類などのイベントの詳細によってクエリを実行するという概念がないことです。その代りに、特定のワークロード (SharePoint や Azure AD など) に対するサブスクリプションを作成します。また、それぞれのサブスクリプションはテナント単位にします。

以下のセクションでは、Office 365 マネージメント アクティビティ API を使用する際にお客様が抱く最も一般的な質問をまとめています。

- [サード パーティ製のツールとクライアントに関する質問](#questions-about-third-party-tools-and-clients)

- [Office 365 で統合監査ログを有効にする](#enabling-unified-audit-logging-in-office-365)

- [API への接続](#connecting-to-the-api)

- [サブスクリプションの確認](#checking-your-subscriptions)

- [新しいサブスクリプションの作成](#creating-a-new-subscription)

- [Webhook の使用](#using-webhooks)

- [コンテンツ BLOB の要求と調整](#requesting-content-blobs-and-throttling)

ここでは、選りすぐりのシンプルな PowerShell スクリプトを示します。これらのスクリプトにより、ユーザーから最も多く寄せられる質問への回答を示すことができます。また、主な操作の用例が示されているためカスタム ソリューションの実装を開始する際に役立てることもできます。 これらのセクションでは説明されていない操作もありますが、「Office 365 マネージメント アクティビティ API リファレンス」には、すべての操作が示されています。

### <a name="questions-about-third-party-tools-and-clients"></a>サード パーティ製のツールとクライアントに関する質問

最も一般的な質問のカテゴリは、監査データのダウンロードおよび集計にサード パーティ製の製品を使用しているユーザーからのものです。 サード パーティ製の製品によっては、セットアップで問題が発生することや、該当する製品で公開されるデータに中断や矛盾が発生することがあります。 そのような場合は、まず、ベンダーのサポート組織に問い合せてください。 通常、テナント固有のベンダー構成またはサービスの問題が、お客様の不満の原因です。

### <a name="enabling-unified-audit-logging-in-office-365"></a>Office 365 で統合監査ログを有効にする

管理アクティビティ API を使用するためにアプリをセットアップしたのに、それが動作しない場合は、Office 365 組織の統合監査ログが有効になっていることをご確認ください。 これを実行するには、Office 365 監査ログをオンにします。 手順については、「[Office 365 監査ログの検索を有効または無効にする](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)」を参照してください。

統合監査が有効になっていない場合は、通常、次の文字列を含むエラーが表示されます。`Microsoft.Office.Compliance.Audit``.DataServiceException: Tenant <tenantID> does not exist.`

### <a name="connecting-to-the-api"></a>API への接続

ほとんどのアプリケーションは、簡単なクライアント資格情報の OAuth2 フローを使用して API に接続します。 そのため、最初の手順では、マネージメント アクティビティ API のデータへのアクセスに必要なアクセス許可を持つ Azure AD アプリケーションを作成します。 Azure AD アプリの登録を作成する手順に関する説明は、この記事の範囲外になります。 詳細については、「[クイック スタート: Azure Active Directory v1.0 エンドポイントを使用してアプリを登録する](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)」を参照してください。

#### <a name="azure-application-permissions"></a>Azure アプリケーションのアクセス許可

現在、Office 365 マネージメント アクティビティ API に使用されている 3 つのアクセス許可は次のとおりです。

1. 組織のアクティビティ データの読み取り

2. 組織のサービス正常性情報の読み取り

3. データ損失防止 (DLP) ポリシー イベントの読み取り (機密情報の検出を含む)

> [!NOTE]
> 上記のアクセス許可セットの少なくとも最初の 2 つには、「アプリケーションのアクセス許可」と「デリゲートされたアクセス許可」の両方を有効にする必要があります。 DLP ポリシー イベントの読み取りは、DLP ワークロードに注目する場合にのみ必要になります。

#### <a name="getting-an-access-token"></a>アクセス トークンの取得

次に示す PowerShell スクリプトでは、アプリ ID とクライアント シークレットを使用して、マネージメント アクティビティ API 認証エンドポイントから OAuth2 トークンを取得します。 その後で、HTTP 要求に添付する `$headerParams` 配列変数にアクセス トークンを格納します。 API エンドポイントの値 ($resource 変数内) には、組織の Microsoft 365 または Office 365 サブスクリプション プランに基づいて、次の値のいずれかを使用します。

- Enterprise プラン: `manage.office.com`

- GCC 政府機関向けプラン: `manage-gcc.office.com`

- GCC High 政府機関向けプラン: `manage.office365.us`

- DoD 政府機関向けプラン: `manage.protection.apps.mil`

```powershell
# Create app of type Web app / API in Azure AD, generate a Client Secret, and update the client id and client secret here
$ClientID = "<YOUR_APPLICATION_ID"
$ClientSecret = "<YOUR_CLIENT_SECRET>"
$loginURL = "https://login.microsoftonline.com/"
$tenantdomain = "<YOUR_DOMAIN>.onmicrosoft.com"
# Get the tenant GUID from Properties | Directory ID under the Azure Active Directory section. For $resource, use one of these endpoint values based on your subscription plan: Enterprise - manage.office.com; GCC - manage-gcc.office.com; GCC High: manage.office365.us; DoD: manage.protection.apps.mil
$TenantGUID = "<YOUR_TENANT_GUID>"
$resource = "https://<YOUR_API_ENDPOINT>"
# auth
$body = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
$headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"} 
```

`$oauth` 変数には、応答オブジェクトを格納します。このオブジェクトには、アクセス トークンなど複数のプロパティが含まれています。 次に、応答例を示します:

```json
token_type     : Bearer
expires_in     : 3599
ext_expires_in : 0
expires_on     : 1508285860
not_before     : 1508281960
resource       : https://manage.office.com
access_token   : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyIsImtpZCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyJ9.eyJhdWQiOiJodHRwczov…
```

### <a name="checking-your-subscriptions"></a>サブスクリプションの確認

既存のマネージメント アクティビティ API クライアントまたはソリューションへのデータ フローに中断が発生したときには、サブスクリプションに何らかの問題が発生しているのではないかと疑われることがあります。アクティブなサブスクリプションを確認するために、前述のスクリプトに次のコードを追加します。

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
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

### <a name="creating-a-new-subscription"></a>新しいサブスクリプションの作成

新規サブスクリプションを作成するには、/start 操作を使用します。 API エンドポイントには、サブスクリプション プランに基づいて、次の値のいずれかを使用します。

- Enterprise プラン: `manage.office.com`

- GCC 政府機関向けプラン: `manage-gcc.office.com`

- GCC High 政府機関向けプラン: `manage.office365.us`

- DoD 政府機関向けプラン: `manage.protection.apps.mil`

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://<YOUR_API_ENDPOINT>/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"
```

> [!NOTE]
> `$headerParams` のデータは、この記事の「[API への接続](#connecting-to-the-api)」に示したスクリプトの最初の部分で設定されています。

前述のコードにより、Audit.AzureActiveDirectory コンテンツ タイプに対する新しいサブスクリプションが作成されます (Webhook は Null になっています)。 その後で、この記事の「[サブスクリプションの確認](#checking-your-subscriptions)」セクションで示したコードを使用すると、サブスクリプションを確認できます。

## <a name="checking-content-availability"></a>コンテンツの利用の可否の確認

特定の期間中に、どのコンテンツ BLOB が作成されたかを確認するために、「API への接続」セクションで示したスクリプトに、次の行を追加することができます。

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

上記の例では、本日 (午前 12 時 00 分 UTC から現在の時刻までに) 利用可能になったすべてのコンテンツの通知を取得しています。 別の期間を指定する場合は、URI に *starttime* パラメーターと *endtime* パラメーターを追加します (照会可能な最長の期間は 24 時間である点に注意してください)。次に例を示します。

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE]
> *starttime* パラメーターと *endtime* パラメーターは、「両方とも使用する」または「両方とも使用しない」のどちらかにする必要があります。

```json
[{      "contentUri" : "https://<your_API_endpoint>/api/v1.0/<your_tenant_guid>/activity/feed/audit/20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentId" : "20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentType" : "Audit.SharePoint",
        "contentCreated" : "2017-10-13T18:00:51.748Z",
        "contentExpiration" : "2017-10-20T18:00:51.748Z",
}]
```

> [!IMPORTANT]
>
> - *contentUri* プロパティは、コンテンツ BLOB を取得できる URI です。 イベントの詳細は BLOB 自体に格納されていて、1 ～ N 件のイベントに関する詳細が格納されています。 コレクションには 30 件の JSON オブジェクトが存在している可能性があり、それらの 30 件のコンテンツ URI には、さらに多くのイベントの詳細が存在している可能性があります。
>
> - *contentCreated* プロパティは、通知されるイベントが作成された日付ではありません。 通知が作成された日付です。 その BLOB で詳細が示されるイベントは、コンテンツ BLOB が作成されたときよりも相当前に作成されている可能性があります。 そのため、特定の期間内に発生したイベントについて API を直接照会することはできません。

#### <a name="paging-contents-for-busy-tenants"></a>ビジー状態のテナントに対するコンテンツのページング

多くの大規模な Office 365 テナントでは、1 時間に数千ものイベントが生成されています。 これに該当する組織で、前述の例のように期間が 24 時間のクエリを実行すると、1 つの応答では返しきれないほどの通知の取得が必要になることがあります。 この場合、ある種の論理的なループの実装が必要になります。そのループでは、毎回、**NextPageUrl:** ヘッダー値について応答ヘッダーを調べます。 詳細については、Office 365 マネージメント アクティビティ API リファレンスの「改ページ」セクションを参照してください。

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

このループ コードのテストは、極度に活発なテナントが存在していないと難しくなります。 スクリプトで数千回の更新操作を実行してテストしてみましたが、**NextPageUrl** ヘッダーの送信が必要になるほどの数の通知を生成することができませんでした。

### <a name="using-webhooks"></a>Webhook の使用

コンテンツ BLOB が作成されたことを通知する方法は 2 つあります。 *プッシュ* アプローチは、Webhook エンドポイントによって実装されます。このエンドポイントは、ユーザーが作成する Web アプリケーションで、ユーザー自身またはクラウド プラットフォームでホストします。 Webhook は、監査対象のコンテンツ タイプに対するサブスクリプションを作成するときに登録します。 また、後述するアプローチを使用して、既存のサブスクリプションに Webhook の登録を追加することもできます。 *プル* アプローチでは、/content 操作を使用して、特定の期間 (24 時間以内) についてのクエリを実行する必要があります。 その応答によって、指定した期間中に作成されたコンテンツ BLOB が知らされます。

Webhook を追加する前に、次の 2 つの問題について注意してください。

1. Webhook は、デバッグやトラブルシューティングに難点があるため Microsoft では重要視されなくなっています。 通常、着信要求に応答する WebAPI エンドポイントはユーザーがホストすることになります。 多くのユーザーは、ホスティング環境 (ユーザーが完全には制御できない環境) またはオンプレミス環境 (着信 HTTP 要求の許可が困難な環境) のどちらかを使用します。 サポートでは、Office 365 監査パイプラインからの着信要求がファイアウォールやルーターによってブロックされるという多くの問題を確認しています。 この場合、API ではバックオフ アルゴリズムを実装することになりますが、このアルゴリズムは複雑になることがあり、サブスクリプションで Webhook が無効になる可能性があります。

2. Webhook は、開始操作の実行後に、検証要求に即座に応答できるように準備が整っている必要があります。 Webhook アプリケーションにバグがあると、検証に失敗して Webhook は無効になります。 検証要求スキーマの詳細については、Office 365 マネージメント アクティビティ API リファレンスの「Webhook 検証」セクションを参照してください。 マネージメント アクティビティ API の通知に応答する実稼働可能な Webhook を作成する際の問題点について慎重に検討する必要があります。

Webhook を実装する場合は、最初に呼び出される Webhook エンドポイントを指定する /start 操作の前に、そのエンドポイントが検証要求と通常の通知要求の両方に HTTP 200 応答で応答する準備ができていることを検証するためのテストが必要です。 通常、この準備状況をテストするには、API からの疑似要求を使用します。 Office 365 マネージメント アクティビティ API リファレンスの「Webhook 検証」セクションと「コンテンツの取得」セクションの両方を慎重に読んで確認して、この 2 種類の要求のスキーマについて理解してください。

Webhook エンドポイントでサブスクリプションを追加する場合は、body パラメーターを /start エンドポイントへの POST に追加します。次に例を示します:

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

この呼出しの直後に、検証要求が `https://webhook.myapp.com/o365/ …` に送信されます。Office 365 マネージメント アクティビティ API リファレンスの「Webhook 検証」セクションで説明されているように、この要求に応答できる状態のリスナーが存在している必要があります。 リスナーは、HTTP 200 で応答する必要があります。 この時点で即座に /list 操作を実行すると、検証が正常に返されるまで null として示される以外の Webhook は表示されません。

#### <a name="checking-notifications-to-webhooks"></a>webhook への通知の確認

/notifications 操作と /content 操作は区別することが重要です。 通知の確認は、Webhook エンドポイントでサブスクライブした場合にのみ重要になります。 この操作により、Webhook への通知が成功したかどうかを確認できます。 この操作は、利用可能なコンテンツをリストするために使用しないでください。 すでに Webhook で受信している可能性のあるコンテンツが利用できるかどうかをクロスチェックする場合は、/content 操作を使用します。 ただし、/notifications 操作を使用して、失敗した通知について最初に確認しておく必要があります。

### <a name="requesting-content-blobs-and-throttling"></a>コンテンツ BLOB の要求と調整

コンテンツ URI のリストを取得したら、その URI で指定される BLOB を要求する必要があります。 PowerShell を使用して (Enterprise 組織の場合には manage.office.com API エンドポイントを使用して) コンテンツ BLOB を要求する例を次に示します。 この例は、この記事の「[アクセス トークンの取得](#getting-an-access-token)」セクションに示した例を使用してアクセス トークンを取得していることと、`$headerParams` 変数に適切な値が設定されていることを前提としています。

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

```json
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

前述の例は、*$response* 変数が /content エンドポイントに対する要求の応答で設定されていることと、*$headerParams* 変数に有効なアクセス トークンが含まれていることを前提としています。 このスクリプトでは、応答からのコンテンツ URI の配列内で最初の項目を取得し、その BLOB をダウンロードするために GET を呼び出して、*$contents* 変数に格納します。 ユーザーのコードでは、*contentUri* ごとに GET を発行して、contentUri コレクション全体をループ処理することになります。
