---
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Office 365 マネージメント アクティビティ API のトラブルシューティング
description: この API のサポートについて Microsoft サポートに最も多く寄せられる質問のまとめです。
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: 09/05/2018
localization_priority: Priority
ms.openlocfilehash: 35d90859056225a5ebcf547d88c05640699c5295
ms.sourcegitcommit: 784b581a699c6d0ab7939ea621d5ecbea71925ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2019
ms.locfileid: "35924820"
---
# <a name="troubleshooting-the-office-365-management-activity-api"></a><span data-ttu-id="0de94-103">Office 365 マネージメント アクティビティ API のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="0de94-103">Troubleshooting the Office 365 Management Activity API</span></span>

<span data-ttu-id="0de94-104">Office 365 マネージメント アクティビティ API (別名、*統合監査 API*) は、Office 365 のセキュリティおよびコンプライアンス機能の一部でしかありませんが、次の理由から大きな注目を集めています。</span><span class="sxs-lookup"><span data-stu-id="0de94-104">The Office 365 Management Activity API (also known as the *Unified Auditing API*) is just one part of Office 365 security and compliance offerings, but it gets a lot of attention because it:</span></span>

- <span data-ttu-id="0de94-105">複数の監査パイプライン ワークロード (SharePoint や Exchange など) にプログラムでアクセスできます</span><span class="sxs-lookup"><span data-stu-id="0de94-105">Allows programmatic access to multiple auditing pipeline workloads (such as SharePoint and Exchange)</span></span>
- <span data-ttu-id="0de94-106">監査データの集計およびインデックス作成のために、広範なサード パーティ ベンダーによって使用されるメイン インターフェイスです</span><span class="sxs-lookup"><span data-stu-id="0de94-106">Is the main interface used by a variety of third-party vendor products to aggregate and index auditing data</span></span>

<span data-ttu-id="0de94-107">マネージメント アクティビティ API と Office 365 サービス コミュニケーション API を混同しないでください。</span><span class="sxs-lookup"><span data-stu-id="0de94-107">The Management Activity API shouldn’t be confused with the Office 365 Service Communications API.</span></span> <span data-ttu-id="0de94-108">マネージメント アクティビティ API は、各種のワークローでのエンド ユーザーのアクティビティを監査するためのものです。</span><span class="sxs-lookup"><span data-stu-id="0de94-108">The Management Activity API is for auditing end user activities in the various workloads.</span></span>  <span data-ttu-id="0de94-109">サービス コミュニケーション API は、Office 365 で利用可能なサービス (Dynamics CRM や ID サービスなど) によって送信される状態やメッセージを監査するためのものです。</span><span class="sxs-lookup"><span data-stu-id="0de94-109">The Service Communications API is for auditing status and messages that are sent by the services that are available in Office 365 (such as Dynamics CRM or Identity Service).</span></span>

<span data-ttu-id="0de94-110">比較的に少数の操作を備えたシンプルな REST インターフェイスになっているにもかかわらず、マネージメント アクティビティ API の使用方法とデータ取得の正確なしくみについて多くの誤解があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-110">Despite having a relatively few operations and a simple REST interface, there’s a lot of confusion about how to use the Management Activity API and the details of exactly how the data is retrieved.</span></span>  <span data-ttu-id="0de94-111">マネージメント アクティビティ API の入門者が明確にしておく必要のあることの 1 つは、イベントが発生した日付、イベントの発生元になる可能性のあるサイト コレクション、イベントの種類などのイベントの詳細によってクエリを実行するという概念がないことです。</span><span class="sxs-lookup"><span data-stu-id="0de94-111">One thing that should be made clear for anyone who’s getting started with the Management Activity API is that there is no concept of querying by event specifics, such as date that the event occurred, which site collection an event might have been fired from, or the type of event.</span></span>  <span data-ttu-id="0de94-112">その代りに、特定のワークロード (SharePoint や Azure AD など) に対するサブスクリプションを作成します。また、それぞれのサブスクリプションはテナント単位にします。</span><span class="sxs-lookup"><span data-stu-id="0de94-112">Instead, you create subscriptions to specific workloads (for example, SharePoint or Azure AD) and each subscription is per tenant.</span></span>

<span data-ttu-id="0de94-113">この記事は、この API のサポートについて Microsoft サポートに最も多く寄せられる質問をまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="0de94-113">This article summarizes the most common questions Microsoft Support receives in supporting this API.</span></span>  <span data-ttu-id="0de94-114">ここでは、選りすぐりのシンプルな PowerShell スクリプトを示します。これらのスクリプトにより、ユーザーから最も多く寄せられる質問への回答を示すことができます。また、主な操作の用例が示されているためカスタム ソリューションの実装を開始する際に役立てることもできます。</span><span class="sxs-lookup"><span data-stu-id="0de94-114">We’ll show a selection of simple PowerShell scripts that can help you answer the most common questions asked by customers or get you started implementing a custom solution by demonstrating the main operations.</span></span>  <span data-ttu-id="0de94-115">この記事では説明されていない操作もありますが、「[Office 365 マネージメント アクティビティ API リファレンス](office-365-management-activity-api-reference.md)」には、すべての操作が示されています。</span><span class="sxs-lookup"><span data-stu-id="0de94-115">Not all the operations are explained in this article, but they are all listed in [Office 365 Management Activity API reference](office-365-management-activity-api-reference.md).</span></span>

## <a name="enabling-unified-audit-logging-in-office-365"></a><span data-ttu-id="0de94-116">Office 365 で統合監査ログを有効にする</span><span class="sxs-lookup"><span data-stu-id="0de94-116">Enabling unified audit logging in Office 365</span></span>

<span data-ttu-id="0de94-117">管理アクティビティ API を使用するためにアプリをセットアップしたのに、それが動作しない場合は、Office 365 組織の統合監査ログが有効になっていることをご確認ください。</span><span class="sxs-lookup"><span data-stu-id="0de94-117">If you've just set up an app that's trying to use the Management Activity API and it's not working, be sure that you've enabled unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="0de94-118">これを実行するには、Office 365 監査ログをオンにします。</span><span class="sxs-lookup"><span data-stu-id="0de94-118">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="0de94-119">手順については、「[Office 365 監査ログの検索を有効または無効にする](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0de94-119">[Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)</span></span>

## <a name="questions-about-third-party-tools-and-clients"></a><span data-ttu-id="0de94-120">サード パーティ製のツールとクライアントに関する質問</span><span class="sxs-lookup"><span data-stu-id="0de94-120">Questions about third-party tools and clients</span></span>

<span data-ttu-id="0de94-121">現時点でサポートの対象になっている質問のうち最も共通するカテゴリは、監査データのダウンロードおよび集計にサード パーティ製の製品を使用しているユーザーからのものです。</span><span class="sxs-lookup"><span data-stu-id="0de94-121">The most common category of questions we’re currently fielding in support come from customers using third-party products to download and aggregate auditing data.</span></span> <span data-ttu-id="0de94-122">サード パーティ製の製品によっては、セットアップで問題が発生することや、該当する製品で公開されるデータに中断や矛盾が発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="0de94-122">Depending on the third-party product, customers may encounter difficulty with the setup or experience an interruption or an inconsistency in the data exposed in those products.</span></span> <span data-ttu-id="0de94-123">そのような場合は、まず、ベンダーのサポート組織に問い合せてください。</span><span class="sxs-lookup"><span data-stu-id="0de94-123">Here it should be stated that the first action such customers should take is to contact their vendor’s support organization.</span></span> <span data-ttu-id="0de94-124">サポートに寄せられたすべてのサービス要求についてエンジニアが調べたところ、テナント固有のサービスの問題が原因になっていたケースは 1 つしかありませんでした。</span><span class="sxs-lookup"><span data-stu-id="0de94-124">In all the service requests that have come to Support, engineers have seen only a single case where a tenant-specific service problem was the cause.</span></span>

<span data-ttu-id="0de94-125">それにもかかわらず、こうしたユーザーの問題が解決されていないことがあります。</span><span class="sxs-lookup"><span data-stu-id="0de94-125">Nevertheless, these customers may still have some unanswered questions.</span></span> <span data-ttu-id="0de94-126">ベンダーが問題はサービスにあると主張している可能性もありますが、ベンダーに問い合せる前にユーザーが最初の確認をしようとしているだけだとも考えられます。</span><span class="sxs-lookup"><span data-stu-id="0de94-126">Their vendors may be insisting that it is a service issue, or they may just want to do some initial checking before contacting their vendor.</span></span> 

## <a name="connecting-to-the-api"></a><span data-ttu-id="0de94-127">API への接続</span><span class="sxs-lookup"><span data-stu-id="0de94-127">Connecting to the API</span></span>

<span data-ttu-id="0de94-128">ほとんどのアプリケーションは、簡単なクライアント資格情報の OAuth2 フローを使用して API に接続します。</span><span class="sxs-lookup"><span data-stu-id="0de94-128">Most applications connect to the API using a straightforward Client Credentials OAuth2 flow.</span></span> <span data-ttu-id="0de94-129">そのため、最初の手順では、マネージメント アクティビティ API のデータへのアクセスに必要なアクセス許可を持つ Azure AD アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="0de94-129">Therefore, the first step is to create an Azure AD application that has the permissions needed to access the Management Activity API data.</span></span> <span data-ttu-id="0de94-130">Azure AD アプリの登録を作成する手順に関する説明は、この記事の範囲外になります。</span><span class="sxs-lookup"><span data-stu-id="0de94-130">It’s outside the scope of this article to explain the steps to create an Azure AD App registration.</span></span> <span data-ttu-id="0de94-131">詳細については、「[クイック スタート: Azure Active Directory v1.0 エンドポイントを使用してアプリを登録する](https://docs.microsoft.com/ja-JP/azure/active-directory/develop/active-directory-integrating-applications)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0de94-131">For more information, see [Register your application with your Azure Active Directory tenant](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications).</span></span>

### <a name="azure-application-permissions"></a><span data-ttu-id="0de94-132">Azure アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="0de94-132">Azure application permissions</span></span>

<span data-ttu-id="0de94-133">現在、Office 365 マネージメント アクティビティ API に使用されている 3 つのアクセス許可は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="0de94-133">The three permissions currently used for the Office 365 Management Activity API are:</span></span>
1. <span data-ttu-id="0de94-134">組織のアクティビティ データの読み取り</span><span class="sxs-lookup"><span data-stu-id="0de94-134">Read activity data for your organization</span></span>
2. <span data-ttu-id="0de94-135">組織のサービス正常性情報の読み取り</span><span class="sxs-lookup"><span data-stu-id="0de94-135">Read service health information for your organization</span></span>
3. <span data-ttu-id="0de94-136">データ損失防止 (DLP) ポリシー イベントの読み取り (機密情報の検出を含む)</span><span class="sxs-lookup"><span data-stu-id="0de94-136">Read Data Loss Prevention (DLP) policy events, including detected sensitive information</span></span> 

> [!NOTE] 
> <span data-ttu-id="0de94-137">上記のアクセス許可セットの少なくとも最初の 2 つには、「アプリケーションのアクセス許可」と「デリゲートされたアクセス許可」の両方を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-137">You should enable both the Application Permissions and the Delegated Permissions for at least the first two of the above permission sets.</span></span> <span data-ttu-id="0de94-138">DLP ポリシー イベントの読み取りは、DLP ワークロードに注目する場合にのみ必要になります。</span><span class="sxs-lookup"><span data-stu-id="0de94-138">Read DLP policy events will only be necessary if you are interested in the DLP workloads.</span></span>

### <a name="getting-an-access-token"></a><span data-ttu-id="0de94-139">アクセス トークンの取得</span><span class="sxs-lookup"><span data-stu-id="0de94-139">Getting an access token</span></span>

<span data-ttu-id="0de94-140">次に示す PowerShell スクリプトでは、アプリ ID とクライアント シークレットを使用して、マネージメント アクティビティ API 認証エンドポイントから OAuth2 トークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="0de94-140">The following PowerShell script uses the App ID and a Client Secret to obtain the OAuth2 token from the Management Activity API authentication endpoint.</span></span> <span data-ttu-id="0de94-141">その後で、アクセス トークンを `$headerParams` 配列変数に格納します。HTTP 要求には、この配列変数を添付します。</span><span class="sxs-lookup"><span data-stu-id="0de94-141">It then places the access token into the `$headerParams` array variable, which you’ll attach to your HTTP request:</span></span> 

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

<span data-ttu-id="0de94-142">`$oauth` 変数には、応答オブジェクトを格納します。このオブジェクトには、アクセス トークンなど複数のプロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0de94-142">The `$oauth` variable will contain the response object, which has several properties including the access token.</span></span> <span data-ttu-id="0de94-143">次に、応答例を示します。</span><span class="sxs-lookup"><span data-stu-id="0de94-143">Here’s an example of a response:</span></span>

```json
token_type     : Bearer
expires_in     : 3599
ext_expires_in : 0
expires_on     : 1508285860
not_before     : 1508281960
resource       : https://manage.office.com
access_token   : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyIsImtpZCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyJ9.eyJhdWQiOiJodHRwczov…
```

## <a name="checking-your-subscriptions"></a><span data-ttu-id="0de94-144">サブスクリプションの確認</span><span class="sxs-lookup"><span data-stu-id="0de94-144">Checking your subscriptions</span></span>

<span data-ttu-id="0de94-145">既存のマネージメント アクティビティ API クライアントまたはソリューションへのデータ フローに中断が発生したときには、サブスクリプションに何らかの問題が発生しているのではないかと疑われることがあります。</span><span class="sxs-lookup"><span data-stu-id="0de94-145">If you’ve experienced an interruption in data flowing to an existing Management Activity API client or solution, you might wonder if something happened to your subscription.</span></span> <span data-ttu-id="0de94-146">アクティブなサブスクリプションを確認するために、前述のスクリプトに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="0de94-146">To check your active subscriptions, add the following to the previous script:</span></span>

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
```

#### <a name="sample-response"></a><span data-ttu-id="0de94-147">応答例</span><span class="sxs-lookup"><span data-stu-id="0de94-147">Sample response</span></span> 

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

<span data-ttu-id="0de94-148">これは、Audit.Exchange と Audit.SharePoint のサブスクリプションがテナントで有効になっていることを示しています。</span><span class="sxs-lookup"><span data-stu-id="0de94-148">This says that the tenant has both Audit.Exchange and Audit.SharePoint subscriptions enabled.</span></span> <span data-ttu-id="0de94-149">Exchange サブスクリプションには使用可能な Webhook がありません (null)。SharePoint サブスクリプションには使用可能な Webhook があります (登録されたエンドポイントのアドレスが示されています)。</span><span class="sxs-lookup"><span data-stu-id="0de94-149">The Exchange subscription has no webhook enabled (null) and the SharePoint subscription has a webhook enabled with the address of the registered endpoint shown.</span></span>

## <a name="creating-a-new-subscription"></a><span data-ttu-id="0de94-150">新しいサブスクリプションの作成</span><span class="sxs-lookup"><span data-stu-id="0de94-150">Creating a new subscription</span></span>

<span data-ttu-id="0de94-151">新しいサブスクリプションを作成するには、/start 操作を使用します。</span><span class="sxs-lookup"><span data-stu-id="0de94-151">To create a new subscription, you use the /start operation:</span></span>

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"
```

> [!NOTE] 
> <span data-ttu-id="0de94-152">`$headerParams` のデータは、この記事の「[API への接続](#connecting-to-the-api)」に示したスクリプトの最初の部分で設定されています。</span><span class="sxs-lookup"><span data-stu-id="0de94-152">Remember that `$headerParams` was populated in the first part of the script listed in the [Connecting to the API](#connecting-to-the-api) section in this article.</span></span>

<span data-ttu-id="0de94-153">前述のコードにより、Audit.AzureActiveDirectory コンテンツ タイプに対する新しいサブスクリプションが作成されます (Webhook は Null になっています)。</span><span class="sxs-lookup"><span data-stu-id="0de94-153">The previous code will create a new subscription to the Audit.AzureActiveDirectory content type, with a webhook that is null.</span></span> <span data-ttu-id="0de94-154">その後で、この記事の「[サブスクリプションの確認](#checking-your-subscriptions)」セクションで示したコードを使用すると、サブスクリプションを確認できます。</span><span class="sxs-lookup"><span data-stu-id="0de94-154">You can then check your subscriptions using the code in the [Checking your subscriptions](#checking-your-subscriptions) section in this article.</span></span>

## <a name="checking-content-availability"></a><span data-ttu-id="0de94-155">コンテンツの利用の可否の確認</span><span class="sxs-lookup"><span data-stu-id="0de94-155">Checking content availability</span></span>

<span data-ttu-id="0de94-156">特定の期間中に、どのコンテンツ BLOB が作成されたかを確認するために、「API への接続」セクションに示したスクリプトに次の行を追加できます。</span><span class="sxs-lookup"><span data-stu-id="0de94-156">To check what content blobs were created during a certain period, you can add the following line to the script in the "Connecting to the API" section:</span></span>

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

<span data-ttu-id="0de94-157">上記の例では、本日 (午前 12 時 00 分 UTC から現在の時刻までに) 利用可能になったすべてのコンテンツの通知を取得しています。</span><span class="sxs-lookup"><span data-stu-id="0de94-157">The previous example will get all the content notifications that became available today, which means from 12:00 AM UTC to the current time.</span></span> <span data-ttu-id="0de94-158">別の期間を指定する場合は、URI に *starttime* パラメーターと *endtime* パラメーターを追加します (照会可能な最長の期間は 24 時間である点に注意してください)。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0de94-158">If you want to specify a different time period (keeping in mind that the maximum period for which you can query is 24 hours), add the *starttime* and *endtime* parameters to the URI; for example:</span></span>

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE] 
> <span data-ttu-id="0de94-159">*starttime* パラメーターと *endtime* パラメーターは、「両方とも使用する」または「両方とも使用しない」のどちらかにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-159">You must use either both *starttime* and *endtime* parameters or neither.</span></span>

<span data-ttu-id="0de94-160">上記の要求により、指定した期間中に利用可能になった通知のコレクションを含む JSON オブジェクトが返されます。</span><span class="sxs-lookup"><span data-stu-id="0de94-160">The previous request will return a JSON object with a collection of notifications that became available during the time period you specify.</span></span> <span data-ttu-id="0de94-161">応答は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="0de94-161">The response will look like this:</span></span>

```json
[{      "contentUri" : "https://manage.office.com/api/v1.0/<<your_tenant_guid>>/activity/feed/audit/20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentId" : "20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentType" : "Audit.SharePoint",
        "contentCreated" : "2017-10-13T18:00:51.748Z",
        "contentExpiration" : "2017-10-20T18:00:51.748Z",
}]
```

> [!IMPORTANT] 
> - <span data-ttu-id="0de94-162">*contentUri* プロパティは、コンテンツ BLOB を取得できる URI です。</span><span class="sxs-lookup"><span data-stu-id="0de94-162">The *contentUri* property is the URI from which you can retrieve the content blob.</span></span> <span data-ttu-id="0de94-163">イベントの詳細は BLOB 自体に格納されていて、1 ～ N 件のイベントに関する詳細が格納されています。</span><span class="sxs-lookup"><span data-stu-id="0de94-163">The blob itself is what contains the event details; it will contain details about 1 – N events.</span></span> <span data-ttu-id="0de94-164">コレクションには 30 件の JSON オブジェクトが存在している可能性があり、それらの 30 件のコンテンツ URI には、さらに多くのイベントの詳細が存在している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-164">While there may be 30 JSON objects in the collection, there may be many more events detailed in those 30 content URIs.</span></span>
> - <span data-ttu-id="0de94-165">*contentCreated* プロパティは、通知されるイベントが作成された日付ではありません。</span><span class="sxs-lookup"><span data-stu-id="0de94-165">The *contentCreated* property is not the date that the event being notified was created.</span></span> <span data-ttu-id="0de94-166">通知が作成された日付です。</span><span class="sxs-lookup"><span data-stu-id="0de94-166">This is the date the notification was created.</span></span> <span data-ttu-id="0de94-167">その BLOB で詳細が示されるイベントは、コンテンツ BLOB が作成されたときよりも相当前に作成されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-167">The events detailed in that blob may have been created well before the content blob was created.</span></span> <span data-ttu-id="0de94-168">そのため、特定の期間内に発生したイベントについて API を直接照会することはできません。</span><span class="sxs-lookup"><span data-stu-id="0de94-168">Therefore, you can never query the API directly for events that occurred within any given period.</span></span>

### <a name="paging-contents-for-busy-tenants"></a><span data-ttu-id="0de94-169">ビジー状態のテナントに対するコンテンツのページング</span><span class="sxs-lookup"><span data-stu-id="0de94-169">Paging contents for busy tenants</span></span>

<span data-ttu-id="0de94-170">多くの大規模な Office 365 テナントでは、1 時間に数千ものイベントが生成されています。</span><span class="sxs-lookup"><span data-stu-id="0de94-170">Many larger Office 365 tenants have thousands of events being generated every hour.</span></span> <span data-ttu-id="0de94-171">これに該当する組織で、前述の例のように期間が 24 時間のクエリを実行すると、1 つの応答では返しきれないほどの通知の取得が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="0de94-171">If this is the case with your organization, and you try to execute a query for a 24-hour period like in the example above, you may need to retrieve more notifications than can be returned in one response.</span></span> <span data-ttu-id="0de94-172">この場合、ある種の論理的なループの実装が必要になります。そのループでは、毎回、**NextPageUrl:** ヘッダー値について応答ヘッダーを調べます。</span><span class="sxs-lookup"><span data-stu-id="0de94-172">In this case, you’ll need to implement a logical loop of some kind, each time checking the response headers for the **NextPageUrl:** header value.</span></span> <span data-ttu-id="0de94-173">詳細については、Office 365 マネージメント アクティビティ API リファレンスの「[改ページ](office-365-management-activity-api-reference.md#pagination)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0de94-173">See the [Pagination](office-365-management-activity-api-reference.md#pagination) section in the Office 365 Management Activity API reference for more details.</span></span> 

<span data-ttu-id="0de94-174">このループのロジックは、次のようなものになります。</span><span class="sxs-lookup"><span data-stu-id="0de94-174">The logic for this loop will be something like this:</span></span>

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

<span data-ttu-id="0de94-175">このループ コードのテストは、極度に活発なテナントが存在していないと難しくなります。</span><span class="sxs-lookup"><span data-stu-id="0de94-175">It will be difficult to test this looping code unless you have a very active tenant.</span></span> <span data-ttu-id="0de94-176">スクリプトで数千回の更新操作を実行してテストしてみましたが、**NextPageUrl** ヘッダーの送信が必要になるほどの数の通知を生成することができませんでした。</span><span class="sxs-lookup"><span data-stu-id="0de94-176">In our testing, we tried to execute several thousand update operations in a script and was unable to generate a large enough number of notifications to require the **NextPageUrl** header to be sent.</span></span>

## <a name="using-webhooks"></a><span data-ttu-id="0de94-177">Webhook の使用</span><span class="sxs-lookup"><span data-stu-id="0de94-177">Using webhooks</span></span>

<span data-ttu-id="0de94-178">コンテンツ BLOB が作成されたことを通知する方法は 2 つあります。</span><span class="sxs-lookup"><span data-stu-id="0de94-178">There two ways to get a notification that content blobs have been created.</span></span> <span data-ttu-id="0de94-179">*プッシュ* アプローチは、Webhook エンドポイントによって実装されます。このエンドポイントは、ユーザーが作成する Web アプリケーションで、ユーザー自身またはクラウド プラットフォームでホストします。</span><span class="sxs-lookup"><span data-stu-id="0de94-179">The *push* approach is implemented with a webhook endpoint, which is a web application that you create and host yourself or on a cloud platform.</span></span> <span data-ttu-id="0de94-180">Webhook は、監査対象のコンテンツ タイプに対するサブスクリプションを作成するときに登録します。</span><span class="sxs-lookup"><span data-stu-id="0de94-180">You register the webhook at the time you create a subscription to an audited content type.</span></span> <span data-ttu-id="0de94-181">また、後述するアプローチを使用して、既存のサブスクリプションに Webhook の登録を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="0de94-181">You may also add a webhook registration to an existing subscription using the approach shown below.</span></span> <span data-ttu-id="0de94-182">*プル* アプローチでは、[/content 操作](office-365-management-activity-api-reference.md#list-available-content)を使用して、特定の期間 (24 時間以内) についてのクエリを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-182">The *pull* approach requires you to query for a particular timespan (no more than 24 hours) using the [/content operation](office-365-management-activity-api-reference.md#list-available-content).</span></span> <span data-ttu-id="0de94-183">その応答によって、指定した期間中に作成されたコンテンツ BLOB が知らされます。</span><span class="sxs-lookup"><span data-stu-id="0de94-183">The response will tell you which content blobs were created during the period specified.</span></span>

<span data-ttu-id="0de94-184">Webhook を追加する前に、次の 2 つの問題について注意してください。</span><span class="sxs-lookup"><span data-stu-id="0de94-184">Before you add a webhook, be aware of the following two issues:</span></span>

1. <span data-ttu-id="0de94-185">Webhook は、デバッグやトラブルシューティングに難点があるため Microsoft では重要視されなくなっています。</span><span class="sxs-lookup"><span data-stu-id="0de94-185">Webhooks are being de-emphasized by Microsoft because of the difficulty in debugging and troubleshooting.</span></span> <span data-ttu-id="0de94-186">通常、着信要求に応答する WebAPI エンドポイントはユーザーがホストすることになります。</span><span class="sxs-lookup"><span data-stu-id="0de94-186">Typically, you would host a WebApi endpoint that responds to incoming requests.</span></span> <span data-ttu-id="0de94-187">多くのユーザーは、ホスティング環境 (ユーザーが完全には制御できない環境) またはオンプレミス環境 (着信 HTTP 要求の許可が困難な環境) のどちらかを使用します。</span><span class="sxs-lookup"><span data-stu-id="0de94-187">Many customers either use hosting environments (which they don’t have full control over) or on-premises environments (that have difficulty allowing incoming HTTP requests).</span></span> <span data-ttu-id="0de94-188">サポートでは、Office 365 監査パイプラインからの着信要求がファイアウォールやルーターによってブロックされるという多くの問題を確認しています。</span><span class="sxs-lookup"><span data-stu-id="0de94-188">Support has seen many problems where the incoming requests from the Office 365 auditing pipeline have been blocked by a firewall or router.</span></span> <span data-ttu-id="0de94-189">この場合、API ではバックオフ アルゴリズムを実装することになりますが、このアルゴリズムは複雑になることがあり、サブスクリプションで Webhook が無効になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-189">In this case, the API will implement a back-off algorithm, which can be confusing and may result in disabling the webhook in the subscription.</span></span>

2. <span data-ttu-id="0de94-190">Webhook は、開始操作の実行後に、検証要求に即座に応答できるように準備が整っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-190">The webhook must be ready to immediately respond to a validation request after the start operation is executed.</span></span> <span data-ttu-id="0de94-191">Webhook アプリケーションにバグがあると、検証に失敗して Webhook は無効になります。</span><span class="sxs-lookup"><span data-stu-id="0de94-191">If there is a bug in the webhook application, the validation will fail, and the webhook will not be enabled.</span></span> <span data-ttu-id="0de94-192">検証要求スキーマの詳細については、Office 365 マネージメント アクティビティ API リファレンスの「[Webhook 検証](office-365-management-activity-api-reference.md#webhook-validation)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0de94-192">For information about the validation request schema, see the [Webhook validation](office-365-management-activity-api-reference.md#webhook-validation) section in the Office 365 Management Activity API reference.</span></span> <span data-ttu-id="0de94-193">マネージメント アクティビティ API の通知に応答する実稼働可能な Webhook を作成する際の問題点について慎重に検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-193">You should seriously consider the challenges in producing a production-ready webhook to respond to Management Activity API notifications.</span></span>

<span data-ttu-id="0de94-194">Webhook を実装する場合は、最初に呼び出される Webhook エンドポイントを指定する /start 操作の前に、そのエンドポイントが検証要求と通常の通知要求の両方に HTTP 200 応答で応答する準備ができていることを検証するためのテストが必要です。</span><span class="sxs-lookup"><span data-stu-id="0de94-194">If you decide to implement a webhook, it should be tested to verify that the endpoint is prepared to respond with an HTTP 200 response to both the validation request and the normal notification requests before any /start operation that specifies a webhook endpoint is called for the first time.</span></span> <span data-ttu-id="0de94-195">通常、この準備状況をテストするには、API からの疑似要求を使用します。</span><span class="sxs-lookup"><span data-stu-id="0de94-195">Typically, you would use a mocked request from the API to test this readiness.</span></span> <span data-ttu-id="0de94-196">Office 365 マネージメント アクティビティ API リファレンスの「[Webhook 検証](office-365-management-activity-api-reference.md#webhook-validation)」セクションと「[コンテンツの取得](office-365-management-activity-api-reference.md#retrieving-content)」セクションの両方を慎重に読んで確認して、この 2 種類の要求のスキーマについて理解してください。</span><span class="sxs-lookup"><span data-stu-id="0de94-196">Carefully read and observe both the [Webhook validation](office-365-management-activity-api-reference.md#webhook-validation) and [Retrieving content](office-365-management-activity-api-reference.md#retrieving-content) sections in the Office 365 Management Activity API reference to understand the schema of these two types of requests.</span></span>

<span data-ttu-id="0de94-197">Webhook エンドポイントでサブスクリプションを追加する場合は、body パラメーターを /start エンドポイントへの POST に追加します。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0de94-197">To add a subscription with a webhook endpoint, add a body parameter to the POST to the /start endpoint; for example:</span></span>

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

<span data-ttu-id="0de94-198">この呼出しの直後に、検証要求が `https://webhook.myapp.com/o365/ …` に送信されます。Office 365 マネージメント アクティビティ API リファレンスの「[Webhook 検証](office-365-management-activity-api-reference.md#webhook-validation)」セクションで説明されているように、この要求に応答できる状態のリスナーが存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-198">Immediately following this call, a validation request will be sent out to `https://webhook.myapp.com/o365/ …` and there should be a listener ready to respond, as per the description in the [Webhook validation](office-365-management-activity-api-reference.md#webhook-validation) section in the Office 365 Management Activity API reference.</span></span> <span data-ttu-id="0de94-199">リスナーは、HTTP 200 で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-199">Your listener must respond with HTTP 200.</span></span> <span data-ttu-id="0de94-200">この時点で即座に /list 操作を実行すると、検証が正常に返されるまで null として示される以外の Webhook は表示されません。</span><span class="sxs-lookup"><span data-stu-id="0de94-200">If you immediately run the /list operation at this point, you will not see the webhook shown as other than null until the validation has returned successfully.</span></span>

### <a name="checking-notifications-to-webhooks"></a><span data-ttu-id="0de94-201">webhook への通知の確認</span><span class="sxs-lookup"><span data-stu-id="0de94-201">Checking notifications to webhooks</span></span>

<span data-ttu-id="0de94-202">/notifications 操作と /content 操作は区別することが重要です。</span><span class="sxs-lookup"><span data-stu-id="0de94-202">It’s important to distinguish between the /notifications operation and the /content operation.</span></span> <span data-ttu-id="0de94-203">通知の確認は、Webhook エンドポイントでサブスクライブした場合にのみ重要になります。</span><span class="sxs-lookup"><span data-stu-id="0de94-203">Checking notifications is only relevant if you have subscribed with a webhook endpoint.</span></span> <span data-ttu-id="0de94-204">この操作により、Webhook への通知が成功したかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="0de94-204">This operation will let you know if attempts to send notifications to your webhook have been successful or not.</span></span> <span data-ttu-id="0de94-205">この操作は、利用可能なコンテンツをリストするために使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="0de94-205">This operation should not be used to list available content.</span></span> <span data-ttu-id="0de94-206">すでに Webhook で受信している可能性のあるコンテンツが利用できるかどうかをクロスチェックする場合は、/content 操作を使用します。</span><span class="sxs-lookup"><span data-stu-id="0de94-206">To cross-check the availability of content against what you may have already received in your webhook, you would use the /content operation.</span></span> <span data-ttu-id="0de94-207">ただし、[/notifications 操作](office-365-management-activity-api-reference.md#list-notifications)を使用して、失敗した通知について最初に確認しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-207">But be sure to first check for failed notifications using the [/notifications operation](office-365-management-activity-api-reference.md#list-notifications).</span></span>

## <a name="requesting-content-blobs-and-throttling"></a><span data-ttu-id="0de94-208">コンテンツ BLOB の要求と調整</span><span class="sxs-lookup"><span data-stu-id="0de94-208">Requesting content blobs and throttling</span></span>

<span data-ttu-id="0de94-209">コンテンツ URI のリストを取得したら、その URI で指定される BLOB を要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-209">After you’ve obtained a list of content URIs, you must request the blobs specified by the URIs.</span></span> <span data-ttu-id="0de94-210">次に、PowerShell を使用してコンテンツ BLOB を要求する例を示します。</span><span class="sxs-lookup"><span data-stu-id="0de94-210">The following is an example of requesting a content blob using PowerShell.</span></span> <span data-ttu-id="0de94-211">この例は、この記事の「[アクセス トークンの取得](#getting-an-access-token)」セクションに示した例を使用してアクセス トークンを取得していることと、`$headerParams` 変数に適切な値が設定されていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="0de94-211">This example assumes you have already used the previous example in the [Getting an access token](#getting-an-access-token) section in this article to get an access token and have populated the `$headerParams` variable appropriately.</span></span>

```powershell
# Get a content blob
$uri = 'https://manage.office.com/api/v1.0/<<your-tenant-guid>>/activity/feed/audit/<<ContentID>$audit_sharepoint$Audit_SharePoint'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

<span data-ttu-id="0de94-212">前述の例の *$uri* 変数に関して、次の事項に注目してください。</span><span class="sxs-lookup"><span data-stu-id="0de94-212">Note the following things about the *$uri* variable in the previous example:</span></span>

- <span data-ttu-id="0de94-213">PowerShell で *$* 記号が変数として解釈されないように、単一引用符を使用しています。</span><span class="sxs-lookup"><span data-stu-id="0de94-213">We used single quotes so that the *$* symbols aren’t interpreted as variables in PowerShell</span></span>
- <span data-ttu-id="0de94-214">URI 全体は、前の /content エンドポイントへの呼出しに対する応答の *contentUri* プロパティで返されます。</span><span class="sxs-lookup"><span data-stu-id="0de94-214">The entire URI will be returned in the *contentUri* property of the response to your previous call to the /content endpoint.</span></span> <span data-ttu-id="0de94-215">プレースホルダーのトークンは、単に説明のために示したものです。</span><span class="sxs-lookup"><span data-stu-id="0de94-215">The placeholder tokens shown are just for illustration.</span></span>

<span data-ttu-id="0de94-216">利用可能なコンテンツ BLOB を取得しようとすると、多くのユーザー (ほとんどの場合は、ビジー状態のテナントを使用しているユーザー) に次のようなエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="0de94-216">When attempting to retrieve the available content blobs, many customers (mostly working with busy tenants) have experienced errors that look like this:</span></span>

```json
Response Code 403: {'error':{'code':'AF429','message':'Too many requests. Method=GetBlob, PublisherId=00000000-0000-0000-0000-000000000000'}}
```

<span data-ttu-id="0de94-217">これは、調整が原因になっていると考えられます。</span><span class="sxs-lookup"><span data-stu-id="0de94-217">This is likely due to throttling.</span></span> <span data-ttu-id="0de94-218">PublisherId パラメーターの値に注目してください。この値は、クライアントが要求で *PublisherIdentifier* を指定していない可能性があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="0de94-218">Note that the value of the PublisherId parameter likely indicates that the client didn’t specify the *PublisherIdentifier* in the request.</span></span> <span data-ttu-id="0de94-219">また、403 エラー応答に *PublisherId* と表示されていても、正しいパラメーター名は *PublisherIdentifier* である点にも注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="0de94-219">Also, keep in mind that the correct parameter name is *PublisherIdentifier* even though you see *PublisherId* listed in the 403 error responses.</span></span>

> [!NOTE] 
> <span data-ttu-id="0de94-220">API リファレンスでは、どの API 操作にも *PublisherIdentifier* パラメーターが示されていますが、このパラメーターはコンテンツ BLOB の取得時の contentUri URL に対する GET 要求にも含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-220">In the API reference, the *PublisherIdentifier* parameter is listed in every operation of the API, but it should also be included in the GET request to the contentUri URL when retrieving the content blob.</span></span>

<span data-ttu-id="0de94-221">問題のトラブルシューティングのために単純な API 呼び出しを実行する場合は (たとえば、サブスクリプションがアクティブかどうかを確認する場合)、*PublisherIdentifier* パラメーターを省略してもかまいませんが、最終的に実稼働用に使用するコードでは、すべての呼び出しに必ず *PublisherIdentifier* パラメーターを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-221">If you’re doing simple API calls to troubleshoot problems (for example, checking if a given subscription is active) you can safely omit the *PublisherIdentifier* parameter, but absolutely any code that is eventually meant for production use should include the *PublisherIdentifier* parameter on every call.</span></span>

<span data-ttu-id="0de94-222">会社のテナントに対応するクライアントを実装する場合、*PublisherIdentifier* はテナント GUID になります。</span><span class="sxs-lookup"><span data-stu-id="0de94-222">If you’re implementing a client for your company’s tenant, the *PublisherIdentifier* is the Tenant GUID.</span></span> <span data-ttu-id="0de94-223">複数の顧客に対応する ISV アプリケーションまたはアドインを作成する場合、*PublisherIdentifier* は ISV のテナント GUID にする必要があります (エンド ユーザーの会社のテナント GUID ではありません)。</span><span class="sxs-lookup"><span data-stu-id="0de94-223">If you are creating an ISV application or add-in for multiple customers, the *PublisherIdentifier* should be the ISV’s Tenant GUID, and not the tenant GUID of end user’s company.</span></span>

<span data-ttu-id="0de94-224">有効な *PublisherIdentifier* を含めると、テナントごとに 1 分あたり 60K の要求が割り当てられるプールに入れられます。</span><span class="sxs-lookup"><span data-stu-id="0de94-224">If you include the valid *PublisherIdentifier*, then you will be in a pool that is allotted 60K requests per minute per tenant.</span></span> <span data-ttu-id="0de94-225">これは、莫大な数の要求です。</span><span class="sxs-lookup"><span data-stu-id="0de94-225">This is an exceptionally large number of requests.</span></span> <span data-ttu-id="0de94-226">ただし、*PublisherIdentifier* パラメーターを含めていないと、すべてのテナントに対して 1 分あたり 60K の要求が割り当てられる汎用プールに入れられます。</span><span class="sxs-lookup"><span data-stu-id="0de94-226">However, if you don’t include the *PublisherIdentifier* parameter, you will be in the general pool allotted 60K requests per minute for all tenants.</span></span> <span data-ttu-id="0de94-227">この場合、呼び出しが調整される可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="0de94-227">In this case, you will more than likely find that your calls are getting throttled.</span></span> <span data-ttu-id="0de94-228">これを防止するために、*PublisherIdentifier* を使用してコンテンツ BLOB を要求する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="0de94-228">To prevent this, here’s how you would request a content blob using the *PublisherIdentifier*:</span></span>

```powershell
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

<span data-ttu-id="0de94-229">前述の例は、*$response* 変数が /content エンドポイントに対する要求の応答で設定されていることと、*$headerParams* 変数に有効なアクセス トークンが含まれていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="0de94-229">The previous example assumes that the *$response* variable was populated with the response to a request to the /content endpoint and that the *$headerParams* variable includes a valid access token.</span></span> <span data-ttu-id="0de94-230">このスクリプトでは、応答からのコンテンツ URI の配列内で最初の項目を取得し、その BLOB をダウンロードするために GET を呼び出して、*$contents* 変数に格納します。</span><span class="sxs-lookup"><span data-stu-id="0de94-230">The script grabs the first item in the array of content URIs from the response and then invokes the GET to download that blob and put it in the *$contents* variable.</span></span> <span data-ttu-id="0de94-231">ユーザーのコードでは、*contentUri* ごとに GET を発行して、contentUri コレクション全体をループ処理することになります。</span><span class="sxs-lookup"><span data-stu-id="0de94-231">Your code will likely loop through the contentUri collection, issuing the GET for each *contentUri*.</span></span>

## <a name="frequently-asked-questions-about-the-office-365-management-api"></a><span data-ttu-id="0de94-232">Office 365 マネージメント API についてよく寄せられる質問</span><span class="sxs-lookup"><span data-stu-id="0de94-232">Frequently asked questions about the Office 365 Management API</span></span>

#### <a name="what-is-the-maximum-time-i-will-have-to-wait-before-a-notification-is-sent-about-a-given-office-365-event"></a><span data-ttu-id="0de94-233">特定の Office 365 イベントに関する通知が送信されるまでに必要な最長の待ち時間はどれくらいですか?</span><span class="sxs-lookup"><span data-stu-id="0de94-233">What is the maximum time I will have to wait before a notification is sent about a given Office 365 event?</span></span>

<span data-ttu-id="0de94-234">通知の配信について最長の待機時間に対する保証はありません (つまり、SLA はありません)。</span><span class="sxs-lookup"><span data-stu-id="0de94-234">There is no guaranteed maximum latency for notification delivery (in other words, no SLA).</span></span> <span data-ttu-id="0de94-235">Microsoft サポートの認識では、ほとんどの通知がイベントの発生から 1 時間以内に送信されます。</span><span class="sxs-lookup"><span data-stu-id="0de94-235">Microsoft Support’s experience has been that most notifications are sent within one hour of the event.</span></span> <span data-ttu-id="0de94-236">この待機時間は大幅に短くなることも、長くなることもあります。</span><span class="sxs-lookup"><span data-stu-id="0de94-236">Often the latency is much shorter, but often it’s longer as well.</span></span> <span data-ttu-id="0de94-237">ワークロードごとに多少の違いはありますが、原則的に、ほとんどの通知はイベントの発生から 24 時間以内に配信されます。</span><span class="sxs-lookup"><span data-stu-id="0de94-237">This varies somewhat from workload to workload, but a general rule is that most notifications will be delivered within 24 hours of the originating event.</span></span>

#### <a name="arent-webhook-notifications-more-immediate-after-all-arent-they-are-event-driven"></a><span data-ttu-id="0de94-238">webhook 通知のほうが早くなりませんか?</span><span class="sxs-lookup"><span data-stu-id="0de94-238">Aren’t webhook notifications more immediate?</span></span> <span data-ttu-id="0de94-239">結局のところ、イベント駆動型ではないですか?</span><span class="sxs-lookup"><span data-stu-id="0de94-239">After all, aren’t they are event-driven?</span></span>

<span data-ttu-id="0de94-240">いいえ。</span><span class="sxs-lookup"><span data-stu-id="0de94-240">No.</span></span> <span data-ttu-id="0de94-241">Webhook 通知は、イベントによって通知がトリガーされるという意味ではイベント駆動ではありません。</span><span class="sxs-lookup"><span data-stu-id="0de94-241">Webhook notifications are not event-driven in the sense that the event triggers the notification.</span></span> <span data-ttu-id="0de94-242">コンテンツ BLOB の作成は依然として必要であり、コンテンツ BLOB の作成が通知の配信をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="0de94-242">The content blob still must be created and creating the content blob is what triggers the notification delivery.</span></span> <span data-ttu-id="0de94-243">最近では、webhook の使用時の通知の待機時間は、/content 操作で API を直接クエリするよりも長くなっています。</span><span class="sxs-lookup"><span data-stu-id="0de94-243">Recently, there have been longer wait times for notifications when using a webhook compared to querying the API directly with the /content operation.</span></span> <span data-ttu-id="0de94-244">そのため、マネージメント アクティビティ API は、リアルタイムのセキュリティ警告システムとして捉えることはできません。</span><span class="sxs-lookup"><span data-stu-id="0de94-244">Therefore, the Management Activity API shouldn’t be thought of as a real-time security alert system.</span></span> <span data-ttu-id="0de94-245">Microsoft は、その目的のための別の製品を用意しています。</span><span class="sxs-lookup"><span data-stu-id="0de94-245">Microsoft has other products for that.</span></span> <span data-ttu-id="0de94-246">セキュリティに関する限り、マネージメント アクティビティ API のイベント通知は、長期間にわたる使用パターンを判断するために使用するほうが適しています。</span><span class="sxs-lookup"><span data-stu-id="0de94-246">As far as security is concerned, Management Activity API event notifications can more appropriately be used to determine use patterns over extended periods of time.</span></span> 

#### <a name="can-i-query-the-management-activity-api-for-a-particular-event-id-or-recordtype-or-other-properties-in-the-content-blob"></a><span data-ttu-id="0de94-247">コンテンツ BLOB 内の特定のイベント ID や RecordType などのプロパティについてマネージメント アクティビティ API を照会できますか?</span><span class="sxs-lookup"><span data-stu-id="0de94-247">Can I query the Management Activity API for a particular event ID or RecordType or other properties in the content blob?</span></span>

<span data-ttu-id="0de94-248">いいえ。</span><span class="sxs-lookup"><span data-stu-id="0de94-248">No.</span></span> <span data-ttu-id="0de94-249">マネージメント アクティビティ API によって利用可能になるデータは、従来の意味での「ログ」と考えないでください。</span><span class="sxs-lookup"><span data-stu-id="0de94-249">Don’t think of the data available through the Management Activity API as being a “log” in the traditional sense.</span></span> <span data-ttu-id="0de94-250">それよりも、イベントの詳細についてのダンプと考えてください。</span><span class="sxs-lookup"><span data-stu-id="0de94-250">Rather, think of it as a dump of event details.</span></span> <span data-ttu-id="0de94-251">カスタムのアプリケーションやサード パーティ製のツールを使用して、これらのイベントの詳細をすべて収集し、ローカルに保存してインデックスを作成し、独自のクエリ ロジックを実装することは、ユーザーの裁量に任されています。</span><span class="sxs-lookup"><span data-stu-id="0de94-251">It’s up to you to gather all those event details, store and index them locally, and then implement your own query logic, by using either a custom application or a third-party tool.</span></span>

#### <a name="how-do-i-know-the-data-coming-from-my-existing-auditing-solution-which-collects-data-from-the-management-activity-api-is-accurate-and-complete"></a><span data-ttu-id="0de94-252">マネージメント アクティビティ API からデータを収集する既存の監査アプリケーションのデータが正確で完全であることを確認する方法はありますか?</span><span class="sxs-lookup"><span data-stu-id="0de94-252">How do I know the data coming from my existing auditing solution, which collects data from the Management Activity API, is accurate and complete?</span></span>

<span data-ttu-id="0de94-253">簡潔に答えると、Microsoft は特定のアプリケーションやサード パーティ (ISV) のアプリケーションをクロスチェックできるようなログは提供していません。</span><span class="sxs-lookup"><span data-stu-id="0de94-253">The short answer is that Microsoft doesn’t provide any kind of a log that will allow you to cross-check any given application or third-party (ISV) application.</span></span> <span data-ttu-id="0de94-254">同じパイプラインからデータを取り出す Microsoft セキュリティ製品もありますが、そうした製品についての説明は、この記事の範囲外であり、マネージメント アクティビティ API を直接クロスチェックするために使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="0de94-254">There are other Microsoft security products that draw their data from the same pipeline, but those products fall outside the scope of this discussion and  can’t be used to directly cross-check the Management Activity API.</span></span> <span data-ttu-id="0de94-255">既存のソリューションが提供する内容と予測した内容の矛盾について懸念している場合は、前述の操作を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-255">If you’re concerned about discrepancies between what your existing solution is providing and what you expect, you should implement the operations illustrated above.</span></span> <span data-ttu-id="0de94-256">ただし、既存のツールやソリューションがデータをリストする方法とデータにインデックスを作成する方法によっては、これは困難なことになります。</span><span class="sxs-lookup"><span data-stu-id="0de94-256">But this can be difficult, depending on how your existing tool or solution lists and indexes data.</span></span> <span data-ttu-id="0de94-257">既存のソリューションが実際のイベントの作成時刻で並べ替えたデータを表示するだけならば、結果セットを比較できるようにイベントの作成時刻で API を照会する方法は存在しません。</span><span class="sxs-lookup"><span data-stu-id="0de94-257">If your existing solution only presents data sorted by the creation time of the actual event, there’s no way to query the API by event creation time so that you could compare result sets.</span></span> <span data-ttu-id="0de94-258">このシナリオでは、通知されたコンテンツ BLOB を数日間にわたって収集し、手動でインデックスを作成するか並べ替えてから、大まかな比較を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-258">In this scenario, you’d have to collect the notified content blobs for several days, index or sort them manually, and then do a rough comparison.</span></span>

#### <a name="how-long-will-the-content-blobs-remain-available"></a><span data-ttu-id="0de94-259">コンテンツ BLOB の利用可能期間はどれくらいですか?</span><span class="sxs-lookup"><span data-stu-id="0de94-259">How long will the content blobs remain available?</span></span>

<span data-ttu-id="0de94-260">コンテンツ BLOB は、コンテンツ BLOB が利用可能になったことが通知されてから 7 日間利用できます。</span><span class="sxs-lookup"><span data-stu-id="0de94-260">Content blobs are available 7 days after the notification of the content blob’s availability.</span></span> <span data-ttu-id="0de94-261">そのため、コンテンツ BLOB の作成に大幅な遅延があった場合は、コンテンツ BLOB が利用できなくなるまで、実際のイベント作成日の後に、それよりも長い時間 (遅延 + 7 日) 利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="0de94-261">This means that if there is a significant delay in the creation of the content blob, you will have more time (the delay plus 7 days) after the actual event creation date before the content blob is no longer available.</span></span>

#### <a name="if-there-is-a-24-hour-delay-in-getting-a-notification-doesnt-that-mean-i-will-have-only-6-days-to-retrieve-the-content-blob"></a><span data-ttu-id="0de94-262">通知されるまでに 24 時間の遅延があった場合、コンテンツ BLOB を取得するための期間は 6 日間しかないことになりますか?</span><span class="sxs-lookup"><span data-stu-id="0de94-262">If there is a 24-hour delay in getting a notification, doesn’t that mean I will have only 6 days to retrieve the content blob?</span></span>

<span data-ttu-id="0de94-263">いいえ。</span><span class="sxs-lookup"><span data-stu-id="0de94-263">No.</span></span> <span data-ttu-id="0de94-264">通知が非常に長い期間遅延した場合でも (サービスの中断などの場合)、元のイベントに関連するコンテンツ BLOB をダウンロードする通知が最初に利用可能になってから 7 日間の期間があります。</span><span class="sxs-lookup"><span data-stu-id="0de94-264">Even if the notification is delayed for an unusually long period (for example, in the case of a service interruption), you would still have 7 days after the first availability of the notification to download the content blob related to the originating event.</span></span>












