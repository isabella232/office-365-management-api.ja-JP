---
ms.TocTitle: Office 365 Management Activity API reference
title: Office 365 管理アクティビティ API リファレンス
description: Office 365 管理アクティビティ API は、Office 365 と Azure AD のアクティビティ ログから、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を取得するために使用します。
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: 01/10/2018
localization_priority: Priority
ms.openlocfilehash: e6675628a384ab4b2dac3342875332b50586526f
ms.sourcegitcommit: 95a3313d95b79a2164008d32c4a4f03bf873a23c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "30379182"
---
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="3dd75-103">Office 365 管理アクティビティ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="3dd75-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="3dd75-104">Office 365 管理アクティビティ API は、Office 365 と Azure AD のアクティビティ ログから、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="3dd75-105">Office 365 と Microsoft Azure Active Directory の監査ログとアクティビティ ログに記録されたアクションとイベントを使用して、監視、分析、およびデータ可視化を提供するソリューションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="3dd75-106">このソリューションにより、企業はそのコンテンツに対して実行されたアクションの可視性を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="3dd75-107">これらのアクションとイベントは、Office 365 アクティビティ レポートからも入手できます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="3dd75-108">詳細については、「[Office 365 セキュリティ/コンプライアンス センターで監査ログを検索する](https://support.office.com/ja-JP/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/ja-JP/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="3dd75-p102">Office 365 管理アクティビティ API は、REAT Web サービスの 1 つであり、任意の言語と、HTTPS および X.509 証明書をサポートするホスト環境を用いて、ソリューションの開発に使用できます。この API は、認証と承認に Azure AD と OAuth2 プロトコルを使用します。アプリケーションからこの API にアクセスする場合は、まず Azure AD で登録し、適切なアクセス許可で設定する必要があります。これにより、アプリケーションで、API を呼び出すために必要な OAuth2 アクセス トークンを要求できます。詳細については、「[Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p102">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates. The API relies on Azure AD and the OAuth2 protocol for authentication and authorization. To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions. This will enable your application to request the OAuth2 access tokens it needs to call the API. For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="3dd75-114">Office 365 管理アクティビティ API で返されるデータのスキーマについては、「[Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-114">For information about the schema of the data that the Office 365 Management Activity API returns, including known issues and upcoming changes, that might affect your implementation, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="3dd75-115">Office 365 管理アクティビティ API の操作</span><span class="sxs-lookup"><span data-stu-id="3dd75-115">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="3dd75-p103">Office 365 管理アクティビティ API は、アクションとイベントを、タイプ別およびコンテンツのソース別に分類されたテナント固有コンテンツ blob に集約します。現時点では、次のコンテンツ タイプがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p103">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain. Currently, these content types are supported:</span></span>

- <span data-ttu-id="3dd75-118">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="3dd75-118">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="3dd75-119">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="3dd75-119">Audit.Exchange</span></span>
    
- <span data-ttu-id="3dd75-120">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="3dd75-120">Audit.SharePoint</span></span>
    
- <span data-ttu-id="3dd75-121">Audit.General (上記のコンテンツ タイプに含まれない、その他すべてのワーク ロードが含まれます)</span><span class="sxs-lookup"><span data-stu-id="3dd75-121">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="3dd75-122">DLP.All (すべてのワークロードの DLP イベントのみ)</span><span class="sxs-lookup"><span data-stu-id="3dd75-122">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="3dd75-123">イベントおよびこれらのコンテンツ タイプに関連付けられているプロパティの詳細については、「[Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-123">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="3dd75-p104">テナントのコンテンツ blob の取得を開始するには、まず目的のコンテンツ タイプのサブスクリプションを作成します。複数のテナントのコンテンツ blob を取得する場合は、テナントごとに 1 つずつ、目的の各コンテンツ タイプの複数のサブスクリプションを作成します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p104">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types. If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="3dd75-126">サブスクリプションを作成したら、ダウンロードできる新しいコンテンツ blob を発見するために定期的にポーリングできます。または Webhook エンドポイントをサブスクリプションに登録して、新しいコンテンツ blob が入手可能になったときにそのエンドポイントで通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-126">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="3dd75-127">サブスクリプションを作成した場合、最初のコンテンツ BLOB がそのサブスクリプションで利用可能になるには、最大で 12 時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-127">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="3dd75-128">blob コンテンツは、複数のサーバーとデータセンターにまたがってアクションとイベントを収集および集約することで作成されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-128">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="3dd75-129">この分散プロセスの結果として、コンテンツ blob に入れられたイベントとアクションは、必ずしも発生した順序で表示されるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-129">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="3dd75-130">コンテンツ blob によっては、それよりも前のコンテンツ blob に入っているものよりも前に発生したアクションとイベントが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-130">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="3dd75-131">アクションとイベントの発生時からそれらをコンテンツ blob 内で参照できるようになるまでの遅延時間は短縮が図られていますが、発生順での表示は保証できません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-131">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="3dd75-132">DLP 機密データは、「DLP 機密データの読み取り」アクセス許可が付与されたユーザーが、アクティビティ フィード API でのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-132">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="3dd75-133">データ損失防止 (DLP) の詳細については、「[データ損失防止ポリシーの概要](https://support.office.com/ja-JP/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-133">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/ja-JP/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="3dd75-134">アクティビティ API の操作</span><span class="sxs-lookup"><span data-stu-id="3dd75-134">Activity API operations</span></span>

<span data-ttu-id="3dd75-p107">すべての API 操作のスコープは単一のテナントであり、API のルート URL にはテナント コンテキストを示すテナント ID が含まれています。テナント ID は、GUID です。GUID を取得する方法の詳細については、「[Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p107">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context. The tenant ID is a GUID. For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="3dd75-138">Webhook に送信される通知には**テナント ID** が含まれるため、同じ Webhook を使用してすべてのテナントの通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-138">Because the notifications we send to your webhook include the **tenant ID**, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="3dd75-p108">すべての API 操作には、Azure AD から取得したアクセス トークンを使用する認証 HTTP ヘッダーが必要です。アクセス トークンのテナント ID は、API のルート URL 内のテナント ID と一致する必要があり、アクセス トークンには、ActivityFeed.Read 要求 (Azure AD でアプリケーションに対して設定したアクセス許可 [組織のアクティビティ データの読み取り] に相当) が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p108">All API operations require an Authorization HTTP header with an access token obtained from Azure AD. The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="3dd75-141">アクティビティ API は、次の操作をサポートします。</span><span class="sxs-lookup"><span data-stu-id="3dd75-141">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="3dd75-142">**サブスクリプションの開始**。テナントの通知の受け取りとアクティビティ データの取得を開始します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-142">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="3dd75-143">**サブスクリプションの停止**。テナントのデータの取得を中止します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-143">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="3dd75-144">**現在のサブスクリプションのリストの作成**</span><span class="sxs-lookup"><span data-stu-id="3dd75-144">**List current subscriptions**</span></span>
    
- <span data-ttu-id="3dd75-145">**利用可能なコンテンツのリストの作成**。これには対応するコンテンツの URL も含まれます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-145">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="3dd75-146">**通知の受け取り**。この通知は新しいコンテンツが利用可能になったときに Webhook により送信されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-146">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="3dd75-147">**コンテンツの取得**。コンテンツ URL を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-147">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="3dd75-148">**通知のリストを作成**。この通知は Webhook によって送信されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-148">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="3dd75-149">**リソースのフレンドリ名の取得**。GUID で識別されるデータ フィード内のオブジェクトに関して実行します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-149">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="3dd75-150">サブスクリプションの開始</span><span class="sxs-lookup"><span data-stu-id="3dd75-150">Start a subscription</span></span>

<span data-ttu-id="3dd75-p109">この操作は、指定したコンテンツ タイプのサブスクリプションを開始します。指定したコンテンツ タイプのサブスクリプションが既に存在する場合、この操作は次の目的で実行します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p109">This operation starts a subscription to the specified content type. If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="3dd75-153">アクティブな Webhook のプロパティを更新します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-153">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="3dd75-154">失敗通知数の超過により無効になった Webhook を有効にします。</span><span class="sxs-lookup"><span data-stu-id="3dd75-154">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="3dd75-155">新しい (または null の) 有効期限日を指定することで、有効期限切れの Webhook を再度有効にします。</span><span class="sxs-lookup"><span data-stu-id="3dd75-155">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="3dd75-156">Webhook を削除します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-156">Remove a webhook.</span></span>
    
||<span data-ttu-id="3dd75-157">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="3dd75-157">Subscription</span></span>|<span data-ttu-id="3dd75-158">説明</span><span class="sxs-lookup"><span data-stu-id="3dd75-158">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3dd75-159">**パス**</span><span class="sxs-lookup"><span data-stu-id="3dd75-159">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="3dd75-160">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="3dd75-160">**Parameters**</span></span>|<span data-ttu-id="3dd75-161">contentType</span><span class="sxs-lookup"><span data-stu-id="3dd75-161">contentType</span></span>|<span data-ttu-id="3dd75-162">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-162">Must be a valid content type.</span></span>|
||<span data-ttu-id="3dd75-163">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="3dd75-163">PublisherIdentifier</span></span>|<span data-ttu-id="3dd75-164">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="3dd75-164">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="3dd75-165">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-165">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="3dd75-166">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-166">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="3dd75-167">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-167">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="3dd75-168">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-168">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="3dd75-169">**Body**</span><span class="sxs-lookup"><span data-stu-id="3dd75-169">**Body**</span></span>|<span data-ttu-id="3dd75-170">webhook</span><span class="sxs-lookup"><span data-stu-id="3dd75-170">webhook</span></span>|<span data-ttu-id="3dd75-171">次の 3 つのプロパティが指定された、オプションの JSON オブジェクト:</span><span class="sxs-lookup"><span data-stu-id="3dd75-171">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-172"><b>address</b>: 通知を受け取ることができる、必須 HTTPS エンドポイントです。</span><span class="sxs-lookup"><span data-stu-id="3dd75-172"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="3dd75-173">サブスクリプションを作成する前に、Webhook を検証するために、テスト メッセージが Webhook に送信されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-173">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="3dd75-174"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span><span class="sxs-lookup"><span data-stu-id="3dd75-174"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="3dd75-175"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span><span class="sxs-lookup"><span data-stu-id="3dd75-175"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-176">**Response**</span><span class="sxs-lookup"><span data-stu-id="3dd75-176">**Response**</span></span>|<span data-ttu-id="3dd75-177">contentType</span><span class="sxs-lookup"><span data-stu-id="3dd75-177">contentType</span></span>|<span data-ttu-id="3dd75-178">呼び出しで指定するコンテンツ タイプ。</span><span class="sxs-lookup"><span data-stu-id="3dd75-178">The content type specified in the call.</span></span>|
||<span data-ttu-id="3dd75-179">status</span><span class="sxs-lookup"><span data-stu-id="3dd75-179">status</span></span>|<span data-ttu-id="3dd75-p112">サブスクリプションの状態。サブスクリプションが無効の場合、コンテンツを取得したりそのリストを作成したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p112">The status of the subscription. If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="3dd75-182">webhook</span><span class="sxs-lookup"><span data-stu-id="3dd75-182">webhook</span></span>|<span data-ttu-id="3dd75-p113">Webhook の状態と一緒に、呼び出しに指定される Webhook のプロパティ。Webhook が無効である場合、通知は受け取りませんが、サブスクリプションが有効であれば、コンテンツを取得したりそのリストを作成したりできます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p113">The webhook properties specified in the call together with the status of the webhook. If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="3dd75-185">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-185">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="3dd75-186">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-186">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="3dd75-187">Webhook の検証</span><span class="sxs-lookup"><span data-stu-id="3dd75-187">Webhook validation</span></span>

<span data-ttu-id="3dd75-p114">/Start 操作が呼び出され、Webhook が指定されると、アクティブ リスナーが通知を受け入れて処理できることを検証するために、指定された Webhook アドレスに検証通知が送信されます。HTTP 200 OK 応答が返信されない場合は、サブスクリプションは作成されません。または、Webhook を既存のサブスクリプションに追加するために /start が呼び出されているものの、HTTP 200 OK の応答が返信されない場合は、Webhook は追加されず、サブスクリプションは変更されません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p114">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications. If we do not receive an HTTP 200 OK response, the subscription will not be created. Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="3dd75-191">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-191">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId) if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="3dd75-192">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-192">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="3dd75-193">サブスクリプションの停止</span><span class="sxs-lookup"><span data-stu-id="3dd75-193">Stop a subscription</span></span>

<span data-ttu-id="3dd75-194">この操作は、指定したコンテンツ タイプのサブスクリプションを停止します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-194">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="3dd75-p115">サブスクリプションを停止すると、通知を受け取ることはなくなり、利用可能なコンテンツを取得することはできません。サブスクリプションを後で再開すると、その時点から新しいコンテンツにアクセスできるようになります。サブスクリプションが停止して再開するまでの間に使用可能であったコンテンツは取得できません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p115">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content. If the subscription is later restarted, you will have access to new content from that point forward. You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="3dd75-198">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="3dd75-198">Subscription</span></span>|<span data-ttu-id="3dd75-199">説明</span><span class="sxs-lookup"><span data-stu-id="3dd75-199">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3dd75-200">**パス**</span><span class="sxs-lookup"><span data-stu-id="3dd75-200">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="3dd75-201">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="3dd75-201">**Parameters**</span></span>|<span data-ttu-id="3dd75-202">contentType</span><span class="sxs-lookup"><span data-stu-id="3dd75-202">contentType</span></span>|<span data-ttu-id="3dd75-203">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-203">Must be a valid content type.</span></span>|
||<span data-ttu-id="3dd75-204">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="3dd75-204">PublisherIdentifier</span></span>|<span data-ttu-id="3dd75-205">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="3dd75-205">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="3dd75-206">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-206">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="3dd75-207">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-207">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="3dd75-208">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-208">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="3dd75-209">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-209">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="3dd75-210">**Body**</span><span class="sxs-lookup"><span data-stu-id="3dd75-210">**Body**</span></span>|<span data-ttu-id="3dd75-211">(空)</span><span class="sxs-lookup"><span data-stu-id="3dd75-211">(empty)</span></span>||
|<span data-ttu-id="3dd75-212">**応答**</span><span class="sxs-lookup"><span data-stu-id="3dd75-212">**Response**</span></span>|<span data-ttu-id="3dd75-213">(空)</span><span class="sxs-lookup"><span data-stu-id="3dd75-213">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="3dd75-214">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-214">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="3dd75-215">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-215">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="3dd75-216">現在のサブスクリプションのリストの作成</span><span class="sxs-lookup"><span data-stu-id="3dd75-216">List current subscriptions</span></span>

<span data-ttu-id="3dd75-217">この操作は、現在のサブスクリプションのコレクションと、関連する Webhook を返します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-217">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="3dd75-218">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="3dd75-218">Subscription</span></span>|<span data-ttu-id="3dd75-219">説明</span><span class="sxs-lookup"><span data-stu-id="3dd75-219">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3dd75-220">**パス**</span><span class="sxs-lookup"><span data-stu-id="3dd75-220">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="3dd75-221">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="3dd75-221">**Parameters**</span></span>|<span data-ttu-id="3dd75-222">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="3dd75-222">PublisherIdentifier</span></span>|<span data-ttu-id="3dd75-223">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="3dd75-223">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="3dd75-224">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-224">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="3dd75-225">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-225">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="3dd75-226">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-226">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="3dd75-227">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-227">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="3dd75-228">**Body**</span><span class="sxs-lookup"><span data-stu-id="3dd75-228">**Body**</span></span>|<span data-ttu-id="3dd75-229">(空)</span><span class="sxs-lookup"><span data-stu-id="3dd75-229">(empty)</span></span>||
|<span data-ttu-id="3dd75-230">**応答**</span><span class="sxs-lookup"><span data-stu-id="3dd75-230">**Response**</span></span>|<span data-ttu-id="3dd75-231">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="3dd75-231">JSON array</span></span>|<span data-ttu-id="3dd75-232">各サブスクリプションは、次の 3 つのプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-232">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-233"><b>contentType</b>:コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-233"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="3dd75-234"><b>status</b>: サブスクリプションの状態を示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-234"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="3dd75-235"><b>webhook</b>: 設定された Webhook と、Webhook の状態 (有効、無効、有効期限切れ) を示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-235"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="3dd75-236">サブスクリプションに Webhook がない場合、Webhook プロパティは存在しますが、null 値を持ちます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-236">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="3dd75-237">要求の例</span><span class="sxs-lookup"><span data-stu-id="3dd75-237">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="3dd75-238">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-238">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="3dd75-239">利用可能なコンテンツのリストの作成</span><span class="sxs-lookup"><span data-stu-id="3dd75-239">List available content</span></span>

<span data-ttu-id="3dd75-p119">この操作は、指定したコンテンツ タイプの、現在取得可能なコンテンツのリストを作成します。コンテンツは、複数のデータセンターにある複数のサーバーから収集されたアクションとイベントの集約です。コンテンツは、集約が利用可能になった順にリストされされますが、集約内のイベントとアクションは必ずしも連続的にはなりません。サブスクリプションの状態が無効である場合は、エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p119">This operation lists the content currently available for retrieval for the specified content type. The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters. The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential. An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="3dd75-244">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="3dd75-244">Subscription</span></span>|<span data-ttu-id="3dd75-245">説明</span><span class="sxs-lookup"><span data-stu-id="3dd75-245">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3dd75-246">**パス**</span><span class="sxs-lookup"><span data-stu-id="3dd75-246">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="3dd75-247">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="3dd75-247">**Parameters**</span></span>|<span data-ttu-id="3dd75-248">contentType</span><span class="sxs-lookup"><span data-stu-id="3dd75-248">contentType</span></span>|<span data-ttu-id="3dd75-249">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-249">Must be a valid content type.</span></span>|
||<span data-ttu-id="3dd75-250">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="3dd75-250">PublisherIdentifier</span></span>|<span data-ttu-id="3dd75-251">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="3dd75-251">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="3dd75-252">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-252">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="3dd75-253">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-253">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="3dd75-254">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-254">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="3dd75-255">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-255">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="3dd75-256">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="3dd75-256">startTime endTime</span></span>|<span data-ttu-id="3dd75-257">コンテンツが利用可能になったときを基点として、コンテンツが返される時間の範囲を示す、オプションの日付/時刻 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="3dd75-257">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="3dd75-258">この時刻範囲には、startTime (startTime <= contentCreated) は含まれ、endTime (contentCreated < endTime) は除外されます。これにより、利用可能なコンテンツのページングに、重なりがない増分の時間間隔を使用できます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-258">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-259">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="3dd75-259">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="3dd75-260">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="3dd75-260">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="3dd75-261">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="3dd75-261">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="3dd75-262">両方を指定するか、両方を省略する必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-262">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="3dd75-263">既定では、startTime と endTime を省略した場合、過去 24 時間以内に利用可能であったコンテンツが返されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-263">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="3dd75-264">**注**: 24 時間よりも長い間隔になる startTime と endTime を指定することもできますが、そのような設定はお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-264">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="3dd75-265">さらに、24 時間よりも長い間隔の要求に対する応答で結果が得られたとしても、部分的な結果になっている可能性があり、結果と見なすべきではありません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-265">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="3dd75-266">要求の発行の際には、間隔が 24 時間以内になる startTime と endTime を指定してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-266">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="3dd75-267">**Response**</span><span class="sxs-lookup"><span data-stu-id="3dd75-267">**Response**</span></span>|<span data-ttu-id="3dd75-268">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="3dd75-268">JSON array</span></span>|<span data-ttu-id="3dd75-269">利用可能なコンテンツは、次のプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-269">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-270"><b>contentType</b>:コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-270"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="3dd75-271"><b>contentId</b>:コンテンツを一意に識別する、符号化文字列です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-271"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="3dd75-272"><b>contentUri</b>:コンテンツを取得するときに使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-272"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="3dd75-273"><b>contentCreated</b>:コンテンツが利用可能になった日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-273"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="3dd75-274"><b>contentExpiration</b>:コンテンツ取得の締切となる日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-274"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="3dd75-275">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-275">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="3dd75-276">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-276">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="3dd75-277">改ページ</span><span class="sxs-lookup"><span data-stu-id="3dd75-277">Pagination</span></span>

<span data-ttu-id="3dd75-p124">ある時間範囲の利用可能なコンテンツのリストを作成する場合、返される結果の数は、応答のタイムアウトを防ぐために制限されます。指定の時間範囲内に 1 つの応答で返せるよりもより多くの結果がある場合、結果は切り捨てられ、次ページの結果を取得するために使用する URL を示すヘッダーが応答に追加されます。この URL には、元の要求に指定されているのと同じ _startTime_ および _endTime_ パラメーターと、次ページの内部 ID を示すパラメーターが含まれます。元の要求で _startTime_ と _endTime_ が指定されていなかった場合、それらは元の要求が出された時点に先行する 24 時間間隔を反映するように設定されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p124">When listing available content for a time range, the number of results returned is limited to prevent response timeouts. If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results. The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page. If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="3dd75-282">指定の時間の範囲にある利用可能なすべてのコンテンツのリストを作成するために、**NextPageUri** ヘッダーがない応答を受信するまで、複数のページを取得することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-282">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="3dd75-283">通知の受け取り</span><span class="sxs-lookup"><span data-stu-id="3dd75-283">Receiving notifications</span></span>

<span data-ttu-id="3dd75-p125">新しいコンテンツが利用可能になると、サブスクリプションの設定済み Webhook に通知が送信されます。通知にはテナント ID が含まれるので、同じ Webhook を使用して、サブスクリプションがあるすべてのテナントの通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p125">Notifications are sent to the configured webhook for a subscription as new content becomes available. Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="3dd75-286">通知は、指定の Webhook アドレスに HTTP POST over TLS (TLS 1.0 以降のバージョン) として行われます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-286">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="3dd75-287">Webhook 構成に認証 ID が含まれている場合、HTTP ヘッダー Webhook-AuthID として送信されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-287">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="3dd75-288">HTTP 200 OK 以外の応答はエラーと見なされ、通知が再試行されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-288">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="3dd75-289">クライアント証明書ベースの認証を要求するように Webhook を設定することもでき、manage.office.com 証明書を使用して認証されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-289">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="3dd75-p127">要求の本文には、利用可能なコンテンツ blob を表す、1 つ以上の JSON オブジェクトの配列が含まれます。通知を比較的小さいサイズにしておくために、各通知内のコンテンツ blob の数は制限されています。この制限は変更される場合があるので、実装では、固定サイズを前提とするのではなく、配列の長さを照会する必要があります。各オブジェクトには、/content 操作によって返されたのと同じプロパティ、データが属するテナントの GUID、およびサブスクリプションを作成したアプリケーションの GUID が含まれます。これにより、Webhook は、複数のテナントとアプリケーションでの使用中に、コンテキストを確立することができます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p127">The body of the request will contain an array of one or more JSON objects that represent the available content blobs. The number of content blobs in each notification is limited to keep the size of the notification relatively small. Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size. Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions. This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="3dd75-295">**tenantId**:コンテンツが属するテナントの GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-295">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="3dd75-296">**clientId**:サブスクリプションを作成したアプリケーションの GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-296">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="3dd75-297">**contentType**:コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-297">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="3dd75-298">**contentId**:コンテンツを一意に識別する、符号化文字列です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-298">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="3dd75-299">**contentUri**:コンテンツを取得するときに使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-299">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="3dd75-300">**contentCreated**:コンテンツが利用可能になった日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-300">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="3dd75-301">**contentExpiration**:コンテンツ取得の締切となる日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-301">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="3dd75-302">通知の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-302">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="3dd75-303">通知の失敗および再試行</span><span class="sxs-lookup"><span data-stu-id="3dd75-303">Notification failure and retry</span></span>

<span data-ttu-id="3dd75-304">通知システムは、新しいコンテンツが利用可能になったときに通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-304">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="3dd75-305">通知の送信時に何度も障害が発生した場合は、再試行メカニズムによって再試行の間隔が指数関数的に長くなります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-305">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="3dd75-306">障害が継続的に発生する場合、Webhook が無効にされ、通知の送信が完全に停止されることがあります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-306">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="3dd75-307">/start 操作を実行すると、無効にされた Webhook を再度有効にできます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-307">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="3dd75-308">コンテンツの取得</span><span class="sxs-lookup"><span data-stu-id="3dd75-308">Retrieving content</span></span>

<span data-ttu-id="3dd75-p129">コンテンツ blob を取得するには、利用可能なコンテンツのリストと Webhook に送信された通知に含まれている、対応するコンテンツ URI に対して GET 要求を行います。返されるコンテンツは、JSON 形式の、1 つ以上のアクションまたはイベントのコレクションになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p129">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook. The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="3dd75-311">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-311">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="3dd75-312">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-312">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="3dd75-313">通知のリスト作成</span><span class="sxs-lookup"><span data-stu-id="3dd75-313">List notifications</span></span>

<span data-ttu-id="3dd75-314">この操作では、指定したコンテンツ タイプのすべての通知の試行についてのリストが作成されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-314">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="3dd75-315">コンテンツ タイプへのサブスクリプションを開始するときに Webhook を含めなかった場合は、取得される通知はありません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-315">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="3dd75-316">通知の再試行が障害発生時に行われるため、この操作では同じコンテンツ対する複数の通知が返される場合があり、通知が送信される順序は、コンテンツが利用可能になった順序と必ずしも一致しません (特に障害と再試行が複数回繰り返される場合はそうなります)。</span><span class="sxs-lookup"><span data-stu-id="3dd75-316">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="3dd75-317">この操作は、Webhook と通知に関連する問題の調査に使用できますが、どのコンテンツが現在取得可能であるかを特定するためには使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-317">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="3dd75-318">その場合は代わりに、/content 操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-318">Use the /content operation instead.</span></span> <span data-ttu-id="3dd75-319">サブスクリプションの状態が無効である場合は、エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-319">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="3dd75-320">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="3dd75-320">Subscription</span></span>|<span data-ttu-id="3dd75-321">説明</span><span class="sxs-lookup"><span data-stu-id="3dd75-321">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3dd75-322">**パス**</span><span class="sxs-lookup"><span data-stu-id="3dd75-322">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="3dd75-323">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="3dd75-323">**Parameters**</span></span>|<span data-ttu-id="3dd75-324">contentType</span><span class="sxs-lookup"><span data-stu-id="3dd75-324">contentType</span></span>|<span data-ttu-id="3dd75-325">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-325">Must be a valid content type.</span></span>|
||<span data-ttu-id="3dd75-326">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="3dd75-326">PublisherIdentifier</span></span>|<span data-ttu-id="3dd75-327">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="3dd75-327">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="3dd75-328">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-328">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="3dd75-329">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-329">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="3dd75-330">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-330">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="3dd75-331">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-331">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="3dd75-332">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="3dd75-332">startTime endTime</span></span>|<span data-ttu-id="3dd75-333">コンテンツが利用可能になったときを基点として、コンテンツが返される時間の範囲を示す、オプションの日付/時刻 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="3dd75-333">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="3dd75-334">この時間の範囲には、_startTime_ (_startTime_ <= contentCreated) は含まれ、_endTime_ (_contentCreated_ < endTime) は含まれません。これにより、利用可能なコンテンツのページングに、重複することのない増分の時間間隔を使用できます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-334">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-335">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="3dd75-335">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="3dd75-336">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="3dd75-336">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="3dd75-337">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="3dd75-337">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="3dd75-338">両方を指定するか、両方を省略する必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-338">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="3dd75-339">既定では、_startTime_ と _endTime_ を省略した場合、過去 24 時間以内に利用可能であったコンテンツが返されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-339">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="3dd75-340">**応答**</span><span class="sxs-lookup"><span data-stu-id="3dd75-340">**Response**</span></span>|<span data-ttu-id="3dd75-341">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="3dd75-341">JSON array</span></span>|<span data-ttu-id="3dd75-342">通知は、次のプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-342">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="3dd75-343">**contentType**: コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-343">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="3dd75-344">**contentId**: コンテンツを一意に識別する、符号化文字列です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-344">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="3dd75-345">**contentUri**: コンテンツを取得するときに使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-345">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="3dd75-346">**contentCreated**: コンテンツが利用可能になった日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-346">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="3dd75-347">**contentExpiration**: コンテンツ取得の締切となる日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-347">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="3dd75-348">**notificationSent**: 通知が送信された日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-348">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="3dd75-349">**notificationStatus**: 通知の試行の成功または失敗を示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-349">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="3dd75-350">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-350">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="3dd75-351">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-351">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="3dd75-352">改ページ</span><span class="sxs-lookup"><span data-stu-id="3dd75-352">Pagination</span></span>

<span data-ttu-id="3dd75-p135">ある時間範囲の通知履歴のリストを作成する場合、返される結果の数は、応答のタイムアウトを防ぐために制限されます。指定の時間範囲内に 1 つの応答で返せるよりもより多くの結果がある場合、結果は切り捨てられ、次ページの結果を取得するために使用する URL を示すヘッダーが応答に追加されます。この URL には、元の要求に指定されているのと同じ _startTime_ および _endTime_ パラメーターと、次ページの内部 ID を示すパラメーターが含まれます。元の要求で _startTime_ と _endTime_ が指定されていなかった場合、それらは元の要求が出された時点に先行する 24 時間間隔を反映するように設定されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p135">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts. If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results. The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page. If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="3dd75-357">指定の時間の範囲にある利用可能なすべてのコンテンツのリストを作成するために、**NextPageUrl** ヘッダーがない応答を受信するまで、複数のページを取得することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-357">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="3dd75-358">リソースのフレンドリ名を取得します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-358">Retrieve resource friendly names</span></span>

<span data-ttu-id="3dd75-359">この操作は、GUID で識別されるデータ フィード内のオブジェクトのフレンドリ名を取得します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-359">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="3dd75-360">現時点でサポートされているオブジェクトは "DlpSensitiveType" のみです。</span><span class="sxs-lookup"><span data-stu-id="3dd75-360">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="3dd75-361">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="3dd75-361">Subscription</span></span>|<span data-ttu-id="3dd75-362">説明</span><span class="sxs-lookup"><span data-stu-id="3dd75-362">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3dd75-363">**パス**</span><span class="sxs-lookup"><span data-stu-id="3dd75-363">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="3dd75-364">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="3dd75-364">**Parameters**</span></span>|<span data-ttu-id="3dd75-365">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="3dd75-365">PublisherIdentifier</span></span>|<span data-ttu-id="3dd75-366">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="3dd75-366">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="3dd75-367">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-367">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="3dd75-368">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-368">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="3dd75-369">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-369">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="3dd75-370">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-370">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="3dd75-371">**ヘッダー**</span><span class="sxs-lookup"><span data-stu-id="3dd75-371">**Headers**</span></span>|<span data-ttu-id="3dd75-372">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="3dd75-372">Accept-Language</span></span>|<span data-ttu-id="3dd75-373">ローカライズされた名前の表示言語を指定するためのヘッダー。</span><span class="sxs-lookup"><span data-stu-id="3dd75-373">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="3dd75-374">たとえば、英語には "en-US" を使用し、スペイン語には "es" を使用します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-374">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="3dd75-375">ヘッダーがない場合は、既定の言語 (en-US) が返されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-375">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="3dd75-376">**Body**</span><span class="sxs-lookup"><span data-stu-id="3dd75-376">**Body**</span></span>|<span data-ttu-id="3dd75-377">(空)</span><span class="sxs-lookup"><span data-stu-id="3dd75-377">(empty)</span></span>||
|<span data-ttu-id="3dd75-378">**応答**</span><span class="sxs-lookup"><span data-stu-id="3dd75-378">**Response**</span></span>|<span data-ttu-id="3dd75-379">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="3dd75-379">JSON array</span></span>|<span data-ttu-id="3dd75-380">利用可能なコンテンツは、次のプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-380">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-381"><b>id</b>: Indicates the guid of the sensitive information type.</span><span class="sxs-lookup"><span data-stu-id="3dd75-381"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="3dd75-382"><b>name</b>: The friendly name of the sensitive information type.</span><span class="sxs-lookup"><span data-stu-id="3dd75-382"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="3dd75-383">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-383">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="3dd75-384">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3dd75-384">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="3dd75-385">API 調整</span><span class="sxs-lookup"><span data-stu-id="3dd75-385">API throttling</span></span>

<span data-ttu-id="3dd75-386">API に対するコードを作成する各ベンダーには、1 分当たり 60K の要求調整のために専用クオータが割り当てられています。</span><span class="sxs-lookup"><span data-stu-id="3dd75-386">Each vendor coding against the API has a dedicated quota for request throttling at 60K per minute.</span></span> <span data-ttu-id="3dd75-387">専用クオータを取得するには、すべての要求でパラメーター PublisherIdentifier を指定します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-387">To get the dedicated quota, specify the parameter PublisherIdentifier in all your requests.</span></span> <span data-ttu-id="3dd75-388">PublisherIdentifier が同じ要求は、同一のクオータを共有します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-388">Requests with the same PublisherIdentifier will share the same quota.</span></span> <span data-ttu-id="3dd75-389">PublisherIdentifier が指定されていないすべての要求は、GUID 00000000-0000-0000-0000-000000000000 と同じクオータを共有するようになります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-389">All requests without the PublisherIdentifier specified will share the same quota as GUID 00000000-0000-0000-0000-000000000000.</span></span>

<span data-ttu-id="3dd75-390">特定の問題で Office 365 がユーザーへの逆エスカレートを必要としている場合は、PublisherIdentifier として使用されている GUID を持つテナントのサブスクリプションが現行であり、正しい連絡先情報で更新されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-390">If Office 365 needs to reverse escalate to you in certain issues, make sure the subscription for the tenant whose GUID is used as your PublisherIdentifier is current and updated with the correct contact information.</span></span> <span data-ttu-id="3dd75-391">このテナントに対するサブスクリプション要件はありません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-391">There is no subscription requirement for this tenant.</span></span>

<span data-ttu-id="3dd75-392">この API を使用して独自のソリューションを開発するユーザーは、制限のある共有クオータによる競合を回避するために独自のテナント GUID を使用してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-392">For customers who are developing their own solutions using this API, we recommend using your own tenant GUID to avoid competition caused by a limited shared quota.</span></span>

> [!NOTE] 
> <span data-ttu-id="3dd75-393">それぞれのパブリッシャーが最大 1 分あたり 60k の要求を送信できますが、Microsoft は応答速度を保証できません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-393">Even though each publisher can submit up to 60K requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="3dd75-394">応答速度は、クライアント システムのパフォーマンス、ネットワーク容量、ネットワーク速度など、さまざまな要因によって決まります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-394">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span>  <span data-ttu-id="3dd75-395">パブリッシャーは最大 1 分当たり 60K の要求を送信できますが、60k の要求に対するすべての応答が同時 (同じ分内) に受信できると期待してはいけません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-395">A publisher can submit up to 60K requests per minute, but should not expect to receive responses for all 60K requests within that same minute.</span></span> <span data-ttu-id="3dd75-396">パブリッシャーがクライアント アプリケーションをベンチマークする必要がある場合は、そのクライアント アプリケーションの稼働を予定している各種環境でベンチマークを実行する必要があります。これは、環境ごとに結果が異なるためです。</span><span class="sxs-lookup"><span data-stu-id="3dd75-396">If anything, should a publisher want to benchmark a client application, they should do so in each different environment that they are planning on running the client application in because results will vary from environment to environment.</span></span>

## <a name="errors"></a><span data-ttu-id="3dd75-397">エラー</span><span class="sxs-lookup"><span data-stu-id="3dd75-397">Errors</span></span>

<span data-ttu-id="3dd75-p142">サービスでエラーが検出されると、標準の HTTP エラー コードの構文を使用して、エラー応答コードが呼び出し元に報告されます。失敗した呼び出しの本体には、追加情報が単一の JSON オブジェクトとして含められます。完全な JSON エラー本体の例を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p142">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax. . Additional information is included in the body of the failed call as a single JSON object. An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="3dd75-402">コード</span><span class="sxs-lookup"><span data-stu-id="3dd75-402">Code</span></span>|<span data-ttu-id="3dd75-403">メッセージ</span><span class="sxs-lookup"><span data-stu-id="3dd75-403">Message</span></span>|
|<span data-ttu-id="3dd75-404">AF10001</span><span class="sxs-lookup"><span data-stu-id="3dd75-404">AF10001</span></span>|<span data-ttu-id="3dd75-405">要求で送信されたアクセス許可セット ({0}) に、必要なアクセス許可 **ActivityFeed.Read** が含まれていませんでした。</span><span class="sxs-lookup"><span data-stu-id="3dd75-405">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-406">{0} = the permission set in the access token.</span><span class="sxs-lookup"><span data-stu-id="3dd75-406">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-407">AF20001</span><span class="sxs-lookup"><span data-stu-id="3dd75-407">AF20001</span></span>|<span data-ttu-id="3dd75-408">Missing parameter: {0}.</span><span class="sxs-lookup"><span data-stu-id="3dd75-408">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-409">{0} = 不足しているパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="3dd75-409">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-410">AF20002</span><span class="sxs-lookup"><span data-stu-id="3dd75-410">AF20002</span></span>|<span data-ttu-id="3dd75-411">無効なパラメーターの種類です: {0}。</span><span class="sxs-lookup"><span data-stu-id="3dd75-411">Invalid parameter type: {0}.</span></span> <span data-ttu-id="3dd75-412">予期される種類: {1}</span><span class="sxs-lookup"><span data-stu-id="3dd75-412">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-413">{0} = 無効なパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="3dd75-413">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="3dd75-414">{1} = the expected type (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="3dd75-414">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-415">AF20003</span><span class="sxs-lookup"><span data-stu-id="3dd75-415">AF20003</span></span>|<span data-ttu-id="3dd75-416">指定した有効期限 {0} は、過去の日付と時刻に設定されています。</span><span class="sxs-lookup"><span data-stu-id="3dd75-416">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-417">{0} = API 呼び出しに渡される有効期限。</span><span class="sxs-lookup"><span data-stu-id="3dd75-417">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-418">AF20010</span><span class="sxs-lookup"><span data-stu-id="3dd75-418">AF20010</span></span>|<span data-ttu-id="3dd75-419">URL ({0}) で渡されたテナント ID が、アクセス トークン ({1}) で渡されたテナント ID と一致しません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-419">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-420">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="3dd75-420">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="3dd75-421">{1} = tenant ID passed in the access token</span><span class="sxs-lookup"><span data-stu-id="3dd75-421">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-422">AF20011</span><span class="sxs-lookup"><span data-stu-id="3dd75-422">AF20011</span></span>|<span data-ttu-id="3dd75-423">指定したテナント ID ({0}) は、システムに存在しないか、削除されています。</span><span class="sxs-lookup"><span data-stu-id="3dd75-423">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="3dd75-424">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="3dd75-424">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-425">AF20012</span><span class="sxs-lookup"><span data-stu-id="3dd75-425">AF20012</span></span>|<span data-ttu-id="3dd75-426">指定したテナント ID ({0}) が、システムで正しく構成されていません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-426">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="3dd75-427">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="3dd75-427">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-428">AF20013</span><span class="sxs-lookup"><span data-stu-id="3dd75-428">AF20013</span></span>|<span data-ttu-id="3dd75-429">URL ({0}) で渡されたテナント ID は、有効な GUID ではありません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-429">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="3dd75-430">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="3dd75-430">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-431">AF20020</span><span class="sxs-lookup"><span data-stu-id="3dd75-431">AF20020</span></span>|<span data-ttu-id="3dd75-432">指定したコンテンツ タイプが無効です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-432">The specified content type is not valid.</span></span>|
|<span data-ttu-id="3dd75-433">AF20021</span><span class="sxs-lookup"><span data-stu-id="3dd75-433">AF20021</span></span>|<span data-ttu-id="3dd75-434">Webhook エンドポイント ({0}) を検証できませんでした。</span><span class="sxs-lookup"><span data-stu-id="3dd75-434">The webhook endpoint {{0}) could not be validated.</span></span> <span data-ttu-id="3dd75-435">{1}</span><span class="sxs-lookup"><span data-stu-id="3dd75-435">{1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-436">{0} = Webhook アドレス。</span><span class="sxs-lookup"><span data-stu-id="3dd75-436">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="3dd75-437">{1} = "エンドポイントは HTTP 200 を返しませんでした。"</span><span class="sxs-lookup"><span data-stu-id="3dd75-437">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="3dd75-438">または "アドレスの先頭は HTTPS である必要があります。"</span><span class="sxs-lookup"><span data-stu-id="3dd75-438">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-439">AF20022</span><span class="sxs-lookup"><span data-stu-id="3dd75-439">AF20022</span></span>|<span data-ttu-id="3dd75-440">指定したコンテンツ タイプのサブスクリプションがありません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-440">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="3dd75-441">AF20023</span><span class="sxs-lookup"><span data-stu-id="3dd75-441">AF20023</span></span>|<span data-ttu-id="3dd75-442">The subscription was disabled by {0}.</span><span class="sxs-lookup"><span data-stu-id="3dd75-442">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-443">{0} = "テナント管理" または "サービス管理"</span><span class="sxs-lookup"><span data-stu-id="3dd75-443">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-444">AF20030</span><span class="sxs-lookup"><span data-stu-id="3dd75-444">AF20030</span></span>|<span data-ttu-id="3dd75-445">開始時刻と終了時刻の両方を指定する (または両方を省略する) 必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-445">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="3dd75-446">AF20031</span><span class="sxs-lookup"><span data-stu-id="3dd75-446">AF20031</span></span>|<span data-ttu-id="3dd75-447">Invalid nextPage Input: {0}.</span><span class="sxs-lookup"><span data-stu-id="3dd75-447">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-448">{0} = URL に渡された次ページ インジケーター</span><span class="sxs-lookup"><span data-stu-id="3dd75-448">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-449">AF20050</span><span class="sxs-lookup"><span data-stu-id="3dd75-449">AF20050</span></span>|<span data-ttu-id="3dd75-450">指定された ID が存在しません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-450">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-451">{0} = リソース ID またはリソース URL。</span><span class="sxs-lookup"><span data-stu-id="3dd75-451">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-452">AF20051</span><span class="sxs-lookup"><span data-stu-id="3dd75-452">AF20051</span></span>|<span data-ttu-id="3dd75-453">キー {0} で要求されたコンテンツは、既に有効期限切れです。</span><span class="sxs-lookup"><span data-stu-id="3dd75-453">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="3dd75-454">7 日を超過したコンテンツは取得できません。</span><span class="sxs-lookup"><span data-stu-id="3dd75-454">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-455">•    {0} = resource id or resource URL</span><span class="sxs-lookup"><span data-stu-id="3dd75-455">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-456">AF20052</span><span class="sxs-lookup"><span data-stu-id="3dd75-456">AF20052</span></span>|<span data-ttu-id="3dd75-457">URL 内のコンテンツの ID {0} は無効です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-457">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-458">{0} = リソース ID またはリソース URL。</span><span class="sxs-lookup"><span data-stu-id="3dd75-458">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-459">AF20053</span><span class="sxs-lookup"><span data-stu-id="3dd75-459">AF20053</span></span>|<span data-ttu-id="3dd75-460">Accept-Language ヘッダーには、1 つの言語のみ表示可能です。</span><span class="sxs-lookup"><span data-stu-id="3dd75-460">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="3dd75-461">AF20054</span><span class="sxs-lookup"><span data-stu-id="3dd75-461">AF20054</span></span>|<span data-ttu-id="3dd75-462">Accept-Language ヘッダーに無効な構文があります。</span><span class="sxs-lookup"><span data-stu-id="3dd75-462">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="3dd75-463">AF429</span><span class="sxs-lookup"><span data-stu-id="3dd75-463">AF429</span></span>|<span data-ttu-id="3dd75-464">要求数が多すぎます。</span><span class="sxs-lookup"><span data-stu-id="3dd75-464">Too many requests.</span></span> <span data-ttu-id="3dd75-465">メソッド={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="3dd75-465">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="3dd75-466">{0} = HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="3dd75-466">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="3dd75-467">{1} = PublisherIdentifier として使用されたテナント GUID</span><span class="sxs-lookup"><span data-stu-id="3dd75-467">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="3dd75-468">AF50000</span><span class="sxs-lookup"><span data-stu-id="3dd75-468">AF50000</span></span>|<span data-ttu-id="3dd75-p148">内部エラーが発生しました。要求を再試行してください。</span><span class="sxs-lookup"><span data-stu-id="3dd75-p148">An internal error occurred. Retry the request.</span></span>|
