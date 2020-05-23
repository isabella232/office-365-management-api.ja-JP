---
ms.TocTitle: Office 365 Management Activity API reference
title: Office 365 管理アクティビティ API リファレンス
description: Office 365 管理アクティビティ API は、Office 365 と Azure AD のアクティビティ ログから、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を取得するために使用します。
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 48065e1770e485ffa04778d662a170ae14916354
ms.sourcegitcommit: d55928a0d535090fa2dbe94f38c7316d0e52e9a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "44173142"
---
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="6dee1-103">Office 365 管理アクティビティ API リファレンス</span><span class="sxs-lookup"><span data-stu-id="6dee1-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="6dee1-104">Office 365 管理アクティビティ API は、Office 365 と Azure AD のアクティビティ ログから、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を取得するために使用します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="6dee1-105">Office 365 と Microsoft Azure Active Directory の監査ログとアクティビティ ログに記録されたアクションとイベントを使用して、監視、分析、およびデータ可視化を提供するソリューションを作成できます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="6dee1-106">このソリューションにより、企業はそのコンテンツに対して実行されたアクションの可視性を向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="6dee1-107">これらのアクションとイベントは、Office 365 アクティビティ レポートからも入手できます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="6dee1-108">詳細については、「[Office 365 セキュリティ/コンプライアンス センターで監査ログを検索する](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="6dee1-p102">Office 365 管理アクティビティ API は、REAT Web サービスの 1 つであり、任意の言語と、HTTPS および X.509 証明書をサポートするホスト環境を用いて、ソリューションの開発に使用できます。この API は、認証と承認に Azure AD と OAuth2 プロトコルを使用します。アプリケーションからこの API にアクセスする場合は、まず Azure AD で登録し、適切なアクセス許可で設定する必要があります。これにより、アプリケーションで、API を呼び出すために必要な OAuth2 アクセス トークンを要求できます。詳細については、「[Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p102">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates. The API relies on Azure AD and the OAuth2 protocol for authentication and authorization. To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions. This will enable your application to request the OAuth2 access tokens it needs to call the API. For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="6dee1-114">Office 365 管理アクティビティ API で返されるデータの詳細情報については、「[Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-114">For information about the data that the Office 365 Management Activity API returns, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dee1-115">Office 365 管理アクティビティ API を介してデータにアクセスする前に、Office 365 組織の統合監査ログを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-115">Before you can access data through the Office 365 Management Activity API, you must enable unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="6dee1-116">これを実行するには、Office 365 監査ログをオンにします。</span><span class="sxs-lookup"><span data-stu-id="6dee1-116">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="6dee1-117">手順については、「[Office 365 監査ログの検索を有効または無効にする](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-117">For instructions, see [Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="6dee1-118">Office 365 管理アクティビティ API の操作</span><span class="sxs-lookup"><span data-stu-id="6dee1-118">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="6dee1-p104">Office 365 管理アクティビティ API は、アクションとイベントを、タイプ別およびコンテンツのソース別に分類されたテナント固有コンテンツ blob に集約します。現時点では、次のコンテンツ タイプがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p104">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain. Currently, these content types are supported:</span></span>

- <span data-ttu-id="6dee1-121">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="6dee1-121">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="6dee1-122">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="6dee1-122">Audit.Exchange</span></span>
    
- <span data-ttu-id="6dee1-123">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="6dee1-123">Audit.SharePoint</span></span>
    
- <span data-ttu-id="6dee1-124">Audit.General (上記のコンテンツ タイプに含まれない、その他すべてのワーク ロードが含まれます)</span><span class="sxs-lookup"><span data-stu-id="6dee1-124">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="6dee1-125">DLP.All (すべてのワークロードの DLP イベントのみ)</span><span class="sxs-lookup"><span data-stu-id="6dee1-125">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="6dee1-126">イベントおよびこれらのコンテンツ タイプに関連付けられているプロパティの詳細については、「[Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-126">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="6dee1-p105">テナントのコンテンツ blob の取得を開始するには、まず目的のコンテンツ タイプのサブスクリプションを作成します。複数のテナントのコンテンツ blob を取得する場合は、テナントごとに 1 つずつ、目的の各コンテンツ タイプの複数のサブスクリプションを作成します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p105">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types. If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="6dee1-129">サブスクリプションを作成したら、ダウンロードできる新しいコンテンツ blob を発見するために定期的にポーリングできます。または Webhook エンドポイントをサブスクリプションに登録して、新しいコンテンツ blob が入手可能になったときにそのエンドポイントで通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-129">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="6dee1-130">サブスクリプションを作成した場合、最初のコンテンツ BLOB がそのサブスクリプションで利用可能になるには、最大で 12 時間かかることがあります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-130">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="6dee1-131">blob コンテンツは、複数のサーバーとデータセンターにまたがってアクションとイベントを収集および集約することで作成されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-131">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="6dee1-132">この分散プロセスの結果として、コンテンツ blob に入れられたイベントとアクションは、必ずしも発生した順序で表示されるとは限りません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-132">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="6dee1-133">コンテンツ blob によっては、それよりも前のコンテンツ blob に入っているものよりも前に発生したアクションとイベントが含まれる場合があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-133">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="6dee1-134">アクションとイベントの発生時からそれらをコンテンツ blob 内で参照できるようになるまでの遅延時間は短縮が図られていますが、発生順での表示は保証できません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-134">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="6dee1-135">DLP 機密データは、「DLP 機密データの読み取り」アクセス許可が付与されたユーザーが、アクティビティ フィード API でのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-135">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="6dee1-136">データ損失防止 (DLP) の詳細については、「[データ損失防止ポリシーの概要](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-136">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="6dee1-137">アクティビティ API の操作</span><span class="sxs-lookup"><span data-stu-id="6dee1-137">Activity API operations</span></span>

<span data-ttu-id="6dee1-p108">すべての API 操作のスコープは単一のテナントであり、API のルート URL にはテナント コンテキストを示すテナント ID が含まれています。テナント ID は、GUID です。GUID を取得する方法の詳細については、「[Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p108">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context. The tenant ID is a GUID. For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span> 

<span data-ttu-id="6dee1-141">Webhook に送信される通知にはテナント ID が含まれるため、同じ Webhook を使用してすべてのテナントの通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-141">Because the notifications we send to your webhook include the tenant ID, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="6dee1-142">使用する API エンドポイントの URL は、組織の Microsoft 365 または Office 365 のサブスクリプション プランの種類に基づいています。</span><span class="sxs-lookup"><span data-stu-id="6dee1-142">The URL for the API endpoint that you use is based on the type of Microsoft 365 or Office 365 subscription plan for your organization.</span></span>

<span data-ttu-id="6dee1-143">**エンタープライズ プランと GCC 政府機関向けプラン**</span><span class="sxs-lookup"><span data-stu-id="6dee1-143">**Enterprise plan and GCC government plan**</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="6dee1-144">**GCC High 政府機関向けプラン**</span><span class="sxs-lookup"><span data-stu-id="6dee1-144">**GCC High government plan**</span></span>

```http
https://manage.office365.us/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="6dee1-145">**DoD 政府機関向けプラン**</span><span class="sxs-lookup"><span data-stu-id="6dee1-145">**DoD government plan**</span></span>

```http
https://manage.protection.apps.mil/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="6dee1-p109">すべての API 操作には、Azure AD から取得したアクセス トークンを使用する認証 HTTP ヘッダーが必要です。アクセス トークンのテナント ID は、API のルート URL 内のテナント ID と一致する必要があり、アクセス トークンには、ActivityFeed.Read 要求 (Azure AD でアプリケーションに対して設定したアクセス許可 [組織のアクティビティ データの読み取り] に相当) が含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p109">All API operations require an Authorization HTTP header with an access token obtained from Azure AD. The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="6dee1-148">アクティビティ API は、次の操作をサポートします。</span><span class="sxs-lookup"><span data-stu-id="6dee1-148">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="6dee1-149">**サブスクリプションの開始**。テナントの通知の受け取りとアクティビティ データの取得を開始します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-149">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="6dee1-150">**サブスクリプションの停止**。テナントのデータの取得を中止します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-150">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="6dee1-151">**現在のサブスクリプションのリストの作成**</span><span class="sxs-lookup"><span data-stu-id="6dee1-151">**List current subscriptions**</span></span>
    
- <span data-ttu-id="6dee1-152">**利用可能なコンテンツのリストの作成**。これには対応するコンテンツの URL も含まれます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-152">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="6dee1-153">**通知の受け取り**。この通知は新しいコンテンツが利用可能になったときに Webhook により送信されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-153">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="6dee1-154">**コンテンツの取得**。コンテンツ URL を使用して実行します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-154">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="6dee1-155">**通知のリストを作成**。この通知は Webhook によって送信されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-155">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="6dee1-156">**リソースのフレンドリ名の取得**。GUID で識別されるデータ フィード内のオブジェクトに関して実行します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-156">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="6dee1-157">サブスクリプションの開始</span><span class="sxs-lookup"><span data-stu-id="6dee1-157">Start a subscription</span></span>

<span data-ttu-id="6dee1-p110">この操作は、指定したコンテンツ タイプのサブスクリプションを開始します。指定したコンテンツ タイプのサブスクリプションが既に存在する場合、この操作は次の目的で実行します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p110">This operation starts a subscription to the specified content type. If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="6dee1-160">アクティブな Webhook のプロパティを更新します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-160">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="6dee1-161">失敗通知数の超過により無効になった Webhook を有効にします。</span><span class="sxs-lookup"><span data-stu-id="6dee1-161">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="6dee1-162">新しい (または null の) 有効期限日を指定することで、有効期限切れの Webhook を再度有効にします。</span><span class="sxs-lookup"><span data-stu-id="6dee1-162">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="6dee1-163">Webhook を削除します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-163">Remove a webhook.</span></span>
    
||<span data-ttu-id="6dee1-164">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="6dee1-164">Subscription</span></span>|<span data-ttu-id="6dee1-165">説明</span><span class="sxs-lookup"><span data-stu-id="6dee1-165">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6dee1-166">**パス**</span><span class="sxs-lookup"><span data-stu-id="6dee1-166">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="6dee1-167">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="6dee1-167">**Parameters**</span></span>|<span data-ttu-id="6dee1-168">contentType</span><span class="sxs-lookup"><span data-stu-id="6dee1-168">contentType</span></span>|<span data-ttu-id="6dee1-169">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-169">Must be a valid content type.</span></span>|
||<span data-ttu-id="6dee1-170">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="6dee1-170">PublisherIdentifier</span></span>|<span data-ttu-id="6dee1-171">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="6dee1-171">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="6dee1-172">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-172">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="6dee1-173">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-173">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="6dee1-174">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-174">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="6dee1-175">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-175">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="6dee1-176">**Body**</span><span class="sxs-lookup"><span data-stu-id="6dee1-176">**Body**</span></span>|<span data-ttu-id="6dee1-177">webhook</span><span class="sxs-lookup"><span data-stu-id="6dee1-177">webhook</span></span>|<span data-ttu-id="6dee1-178">次の 3 つのプロパティが指定された、オプションの JSON オブジェクト:</span><span class="sxs-lookup"><span data-stu-id="6dee1-178">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-p112"><b>address</b>: Required HTTPS endpoint that can receive notifications.  A test message will be sent to the webhook to validate the webhook before creating the subscription.</span><span class="sxs-lookup"><span data-stu-id="6dee1-p112"><b>address</b>: Required HTTPS endpoint that can receive notifications.  A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="6dee1-181"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span><span class="sxs-lookup"><span data-stu-id="6dee1-181"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="6dee1-182"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span><span class="sxs-lookup"><span data-stu-id="6dee1-182"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-183">**Response**</span><span class="sxs-lookup"><span data-stu-id="6dee1-183">**Response**</span></span>|<span data-ttu-id="6dee1-184">contentType</span><span class="sxs-lookup"><span data-stu-id="6dee1-184">contentType</span></span>|<span data-ttu-id="6dee1-185">呼び出しで指定するコンテンツ タイプ。</span><span class="sxs-lookup"><span data-stu-id="6dee1-185">The content type specified in the call.</span></span>|
||<span data-ttu-id="6dee1-186">status</span><span class="sxs-lookup"><span data-stu-id="6dee1-186">status</span></span>|<span data-ttu-id="6dee1-p113">サブスクリプションの状態。サブスクリプションが無効の場合、コンテンツを取得したりそのリストを作成したりすることはできません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p113">The status of the subscription. If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="6dee1-189">webhook</span><span class="sxs-lookup"><span data-stu-id="6dee1-189">webhook</span></span>|<span data-ttu-id="6dee1-p114">Webhook の状態と一緒に、呼び出しに指定される Webhook のプロパティ。Webhook が無効である場合、通知は受け取りませんが、サブスクリプションが有効であれば、コンテンツを取得したりそのリストを作成したりできます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p114">The webhook properties specified in the call together with the status of the webhook. If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="6dee1-192">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-192">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="6dee1-193">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-193">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="6dee1-194">Webhook の検証</span><span class="sxs-lookup"><span data-stu-id="6dee1-194">Webhook validation</span></span>

<span data-ttu-id="6dee1-p115">/Start 操作が呼び出され、Webhook が指定されると、アクティブ リスナーが通知を受け入れて処理できることを検証するために、指定された Webhook アドレスに検証通知が送信されます。HTTP 200 OK 応答が返信されない場合は、サブスクリプションは作成されません。または、Webhook を既存のサブスクリプションに追加するために /start が呼び出されているものの、HTTP 200 OK の応答が返信されない場合は、Webhook は追加されず、サブスクリプションは変更されません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p115">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications. If we do not receive an HTTP 200 OK response, the subscription will not be created. Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="6dee1-198">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-198">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="6dee1-199">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-199">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="6dee1-200">サブスクリプションの停止</span><span class="sxs-lookup"><span data-stu-id="6dee1-200">Stop a subscription</span></span>

<span data-ttu-id="6dee1-201">この操作は、指定したコンテンツ タイプのサブスクリプションを停止します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-201">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="6dee1-p116">サブスクリプションを停止すると、通知を受け取ることはなくなり、利用可能なコンテンツを取得することはできません。サブスクリプションを後で再開すると、その時点から新しいコンテンツにアクセスできるようになります。サブスクリプションが停止して再開するまでの間に使用可能であったコンテンツは取得できません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p116">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content. If the subscription is later restarted, you will have access to new content from that point forward. You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="6dee1-205">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="6dee1-205">Subscription</span></span>|<span data-ttu-id="6dee1-206">説明</span><span class="sxs-lookup"><span data-stu-id="6dee1-206">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6dee1-207">**パス**</span><span class="sxs-lookup"><span data-stu-id="6dee1-207">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="6dee1-208">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="6dee1-208">**Parameters**</span></span>|<span data-ttu-id="6dee1-209">contentType</span><span class="sxs-lookup"><span data-stu-id="6dee1-209">contentType</span></span>|<span data-ttu-id="6dee1-210">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-210">Must be a valid content type.</span></span>|
||<span data-ttu-id="6dee1-211">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="6dee1-211">PublisherIdentifier</span></span>|<span data-ttu-id="6dee1-212">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="6dee1-212">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="6dee1-213">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-213">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="6dee1-214">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-214">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="6dee1-215">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-215">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="6dee1-216">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-216">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="6dee1-217">**Body**</span><span class="sxs-lookup"><span data-stu-id="6dee1-217">**Body**</span></span>|<span data-ttu-id="6dee1-218">(空)</span><span class="sxs-lookup"><span data-stu-id="6dee1-218">(empty)</span></span>||
|<span data-ttu-id="6dee1-219">**応答**</span><span class="sxs-lookup"><span data-stu-id="6dee1-219">**Response**</span></span>|<span data-ttu-id="6dee1-220">(空)</span><span class="sxs-lookup"><span data-stu-id="6dee1-220">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="6dee1-221">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-221">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="6dee1-222">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-222">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="6dee1-223">現在のサブスクリプションのリストの作成</span><span class="sxs-lookup"><span data-stu-id="6dee1-223">List current subscriptions</span></span>

<span data-ttu-id="6dee1-224">この操作は、現在のサブスクリプションのコレクションと、関連する Webhook を返します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-224">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="6dee1-225">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="6dee1-225">Subscription</span></span>|<span data-ttu-id="6dee1-226">説明</span><span class="sxs-lookup"><span data-stu-id="6dee1-226">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6dee1-227">**パス**</span><span class="sxs-lookup"><span data-stu-id="6dee1-227">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="6dee1-228">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="6dee1-228">**Parameters**</span></span>|<span data-ttu-id="6dee1-229">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="6dee1-229">PublisherIdentifier</span></span>|<span data-ttu-id="6dee1-230">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="6dee1-230">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="6dee1-231">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-231">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="6dee1-232">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-232">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="6dee1-233">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-233">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="6dee1-234">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-234">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="6dee1-235">**Body**</span><span class="sxs-lookup"><span data-stu-id="6dee1-235">**Body**</span></span>|<span data-ttu-id="6dee1-236">(空)</span><span class="sxs-lookup"><span data-stu-id="6dee1-236">(empty)</span></span>||
|<span data-ttu-id="6dee1-237">**応答**</span><span class="sxs-lookup"><span data-stu-id="6dee1-237">**Response**</span></span>|<span data-ttu-id="6dee1-238">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="6dee1-238">JSON array</span></span>|<span data-ttu-id="6dee1-239">各サブスクリプションは、次の 3 つのプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-239">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-240"><b>contentType</b>:コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-240"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="6dee1-241"><b>status</b>: Indicates the status of the subscription.</span><span class="sxs-lookup"><span data-stu-id="6dee1-241"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="6dee1-p119"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.  If a subscription does not have a webhook, the webhook property will be present but with null value.</span><span class="sxs-lookup"><span data-stu-id="6dee1-p119"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.  If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="6dee1-244">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-244">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="6dee1-245">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-245">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="6dee1-246">利用可能なコンテンツのリストの作成</span><span class="sxs-lookup"><span data-stu-id="6dee1-246">List available content</span></span>

<span data-ttu-id="6dee1-p120">この操作は、指定したコンテンツ タイプの、現在取得可能なコンテンツのリストを作成します。コンテンツは、複数のデータセンターにある複数のサーバーから収集されたアクションとイベントの集約です。コンテンツは、集約が利用可能になった順にリストされされますが、集約内のイベントとアクションは必ずしも連続的にはなりません。サブスクリプションの状態が無効である場合は、エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p120">This operation lists the content currently available for retrieval for the specified content type. The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters. The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential. An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="6dee1-251">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="6dee1-251">Subscription</span></span>|<span data-ttu-id="6dee1-252">説明</span><span class="sxs-lookup"><span data-stu-id="6dee1-252">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6dee1-253">**パス**</span><span class="sxs-lookup"><span data-stu-id="6dee1-253">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="6dee1-254">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="6dee1-254">**Parameters**</span></span>|<span data-ttu-id="6dee1-255">contentType</span><span class="sxs-lookup"><span data-stu-id="6dee1-255">contentType</span></span>|<span data-ttu-id="6dee1-256">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-256">Must be a valid content type.</span></span>|
||<span data-ttu-id="6dee1-257">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="6dee1-257">PublisherIdentifier</span></span>|<span data-ttu-id="6dee1-258">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="6dee1-258">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="6dee1-259">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-259">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="6dee1-260">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-260">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="6dee1-261">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-261">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="6dee1-262">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-262">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="6dee1-263">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="6dee1-263">startTime endTime</span></span>|<span data-ttu-id="6dee1-p122">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available. The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span><span class="sxs-lookup"><span data-stu-id="6dee1-p122">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available. The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-266">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="6dee1-266">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="6dee1-267">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="6dee1-267">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="6dee1-268">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="6dee1-268">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="6dee1-p123">開始時刻と終了時刻の両方を指定する (または両方を省略する) 必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。 By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span><span class="sxs-lookup"><span data-stu-id="6dee1-p123">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past. By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="6dee1-271">**注**: 24 時間よりも長い間隔になる startTime と endTime を指定することもできますが、そのような設定はお勧めできません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-271">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="6dee1-272">さらに、24 時間よりも長い間隔の要求に対する応答で結果が得られたとしても、部分的な結果になっている可能性があり、結果と見なすべきではありません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-272">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="6dee1-273">要求の発行の際には、間隔が 24 時間以内になる startTime と endTime を指定してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-273">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="6dee1-274">**Response**</span><span class="sxs-lookup"><span data-stu-id="6dee1-274">**Response**</span></span>|<span data-ttu-id="6dee1-275">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="6dee1-275">JSON array</span></span>|<span data-ttu-id="6dee1-276">利用可能なコンテンツは、次のプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-276">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-277"><b>contentType</b>:コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-277"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="6dee1-278"><b>contentId</b>:コンテンツを一意に識別する、符号化文字列です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-278"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="6dee1-279"><b>contentUri</b>:コンテンツを取得するときに使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-279"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="6dee1-280"><b>contentCreated</b>:コンテンツが利用可能になった日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-280"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="6dee1-281"><b>contentExpiration</b>:コンテンツ取得の締切となる日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-281"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="6dee1-282">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-282">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="6dee1-283">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-283">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="6dee1-284">改ページ</span><span class="sxs-lookup"><span data-stu-id="6dee1-284">Pagination</span></span>

<span data-ttu-id="6dee1-p125">ある時間範囲の利用可能なコンテンツのリストを作成する場合、返される結果の数は、応答のタイムアウトを防ぐために制限されます。指定の時間範囲内に 1 つの応答で返せるよりもより多くの結果がある場合、結果は切り捨てられ、次ページの結果を取得するために使用する URL を示すヘッダーが応答に追加されます。この URL には、元の要求に指定されているのと同じ _startTime_ および _endTime_ パラメーターと、次ページの内部 ID を示すパラメーターが含まれます。元の要求で _startTime_ と _endTime_ が指定されていなかった場合、それらは元の要求が出された時点に先行する 24 時間間隔を反映するように設定されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p125">When listing available content for a time range, the number of results returned is limited to prevent response timeouts. If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results. The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page. If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="6dee1-289">指定の時間の範囲にある利用可能なすべてのコンテンツのリストを作成するために、**NextPageUri** ヘッダーがない応答を受信するまで、複数のページを取得することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-289">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="6dee1-290">通知の受け取り</span><span class="sxs-lookup"><span data-stu-id="6dee1-290">Receiving notifications</span></span>

<span data-ttu-id="6dee1-p126">新しいコンテンツが利用可能になると、サブスクリプションの設定済み Webhook に通知が送信されます。通知にはテナント ID が含まれるので、同じ Webhook を使用して、サブスクリプションがあるすべてのテナントの通知を受け取ることができます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p126">Notifications are sent to the configured webhook for a subscription as new content becomes available. Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="6dee1-293">通知は、指定の Webhook アドレスに HTTP POST over TLS (TLS 1.0 以降のバージョン) として行われます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-293">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="6dee1-294">Webhook 構成に認証 ID が含まれている場合、HTTP ヘッダー Webhook-AuthID として送信されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-294">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="6dee1-295">HTTP 200 OK 以外の応答はエラーと見なされ、通知が再試行されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-295">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="6dee1-296">クライアント証明書ベースの認証を要求するように Webhook を設定することもでき、manage.office.com 証明書を使用して認証されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-296">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="6dee1-p128">要求の本文には、利用可能なコンテンツ blob を表す、1 つ以上の JSON オブジェクトの配列が含まれます。通知を比較的小さいサイズにしておくために、各通知内のコンテンツ blob の数は制限されています。この制限は変更される場合があるので、実装では、固定サイズを前提とするのではなく、配列の長さを照会する必要があります。各オブジェクトには、/content 操作によって返されたのと同じプロパティ、データが属するテナントの GUID、およびサブスクリプションを作成したアプリケーションの GUID が含まれます。これにより、Webhook は、複数のテナントとアプリケーションでの使用中に、コンテキストを確立することができます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p128">The body of the request will contain an array of one or more JSON objects that represent the available content blobs. The number of content blobs in each notification is limited to keep the size of the notification relatively small. Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size. Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions. This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="6dee1-302">**tenantId**:コンテンツが属するテナントの GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-302">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="6dee1-303">**clientId**:サブスクリプションを作成したアプリケーションの GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-303">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="6dee1-304">**contentType**:コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-304">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="6dee1-305">**contentId**:コンテンツを一意に識別する、符号化文字列です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-305">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="6dee1-306">**contentUri**:コンテンツを取得するときに使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-306">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="6dee1-307">**contentCreated**:コンテンツが利用可能になった日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-307">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="6dee1-308">**contentExpiration**:コンテンツ取得の締切となる日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-308">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="6dee1-309">通知の例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-309">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="6dee1-310">通知の失敗および再試行</span><span class="sxs-lookup"><span data-stu-id="6dee1-310">Notification failure and retry</span></span>

<span data-ttu-id="6dee1-311">通知システムは、新しいコンテンツが利用可能になったときに通知を送信します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-311">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="6dee1-312">通知の送信時に何度も障害が発生した場合は、再試行メカニズムによって再試行の間隔が指数関数的に長くなります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-312">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="6dee1-313">障害が継続的に発生する場合、Webhook が無効にされ、通知の送信が完全に停止されることがあります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-313">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="6dee1-314">/start 操作を実行すると、無効にされた Webhook を再度有効にできます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-314">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="6dee1-315">コンテンツの取得</span><span class="sxs-lookup"><span data-stu-id="6dee1-315">Retrieving content</span></span>

<span data-ttu-id="6dee1-p130">コンテンツ blob を取得するには、利用可能なコンテンツのリストと Webhook に送信された通知に含まれている、対応するコンテンツ URI に対して GET 要求を行います。返されるコンテンツは、JSON 形式の、1 つ以上のアクションまたはイベントのコレクションになります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p130">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook. The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="6dee1-318">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-318">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="6dee1-319">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-319">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="6dee1-320">通知のリスト作成</span><span class="sxs-lookup"><span data-stu-id="6dee1-320">List notifications</span></span>

<span data-ttu-id="6dee1-321">この操作では、指定したコンテンツ タイプのすべての通知の試行についてのリストが作成されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-321">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="6dee1-322">コンテンツ タイプへのサブスクリプションを開始するときに Webhook を含めなかった場合は、取得される通知はありません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-322">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="6dee1-323">通知の再試行が障害発生時に行われるため、この操作では同じコンテンツ対する複数の通知が返される場合があり、通知が送信される順序は、コンテンツが利用可能になった順序と必ずしも一致しません (特に障害と再試行が複数回繰り返される場合はそうなります)。</span><span class="sxs-lookup"><span data-stu-id="6dee1-323">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="6dee1-324">この操作は、Webhook と通知に関連する問題の調査に使用できますが、どのコンテンツが現在取得可能であるかを特定するためには使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-324">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="6dee1-325">その場合は代わりに、/content 操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-325">Use the /content operation instead.</span></span> <span data-ttu-id="6dee1-326">サブスクリプションの状態が無効である場合は、エラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-326">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="6dee1-327">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="6dee1-327">Subscription</span></span>|<span data-ttu-id="6dee1-328">説明</span><span class="sxs-lookup"><span data-stu-id="6dee1-328">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6dee1-329">**パス**</span><span class="sxs-lookup"><span data-stu-id="6dee1-329">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="6dee1-330">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="6dee1-330">**Parameters**</span></span>|<span data-ttu-id="6dee1-331">contentType</span><span class="sxs-lookup"><span data-stu-id="6dee1-331">contentType</span></span>|<span data-ttu-id="6dee1-332">有効なコンテンツ タイプである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-332">Must be a valid content type.</span></span>|
||<span data-ttu-id="6dee1-333">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="6dee1-333">PublisherIdentifier</span></span>|<span data-ttu-id="6dee1-334">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="6dee1-334">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="6dee1-335">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-335">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="6dee1-336">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-336">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="6dee1-337">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-337">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="6dee1-338">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-338">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="6dee1-339">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="6dee1-339">startTime endTime</span></span>|<span data-ttu-id="6dee1-340">コンテンツが利用可能になったときを基点として、コンテンツが返される時間の範囲を示す、オプションの日付/時刻 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="6dee1-340">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="6dee1-341">この時間の範囲には、_startTime_ (_startTime_ <= contentCreated) は含まれ、_endTime_ (_contentCreated_ < endTime) は含まれません。これにより、利用可能なコンテンツのページングに、重複することのない増分の時間間隔を使用できます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-341">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-342">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="6dee1-342">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="6dee1-343">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="6dee1-343">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="6dee1-344">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="6dee1-344">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="6dee1-p135">開始時刻と終了時刻の両方を指定する (または両方を省略する) 必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。 By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span><span class="sxs-lookup"><span data-stu-id="6dee1-p135">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past. By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="6dee1-347">**Response**</span><span class="sxs-lookup"><span data-stu-id="6dee1-347">**Response**</span></span>|<span data-ttu-id="6dee1-348">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="6dee1-348">JSON array</span></span>|<span data-ttu-id="6dee1-349">通知は、次のプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-349">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="6dee1-350">**contentType**: コンテンツ タイプを示します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-350">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="6dee1-351">**contentId**: コンテンツを一意に識別する、符号化文字列です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-351">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="6dee1-352">**contentUri**: コンテンツを取得するときに使用する URL です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-352">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="6dee1-353">**contentCreated**: コンテンツが利用可能になった日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-353">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="6dee1-354">**contentExpiration**: コンテンツ取得の締切となる日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-354">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="6dee1-355">**notificationSent**: 通知が送信された日付/時刻です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-355">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="6dee1-356">**notificationStatus**: 通知の試行の成功または失敗を示します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-356">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="6dee1-357">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-357">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="6dee1-358">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-358">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="6dee1-359">改ページ</span><span class="sxs-lookup"><span data-stu-id="6dee1-359">Pagination</span></span>

<span data-ttu-id="6dee1-p136">ある時間範囲の通知履歴のリストを作成する場合、返される結果の数は、応答のタイムアウトを防ぐために制限されます。指定の時間範囲内に 1 つの応答で返せるよりもより多くの結果がある場合、結果は切り捨てられ、次ページの結果を取得するために使用する URL を示すヘッダーが応答に追加されます。この URL には、元の要求に指定されているのと同じ _startTime_ および _endTime_ パラメーターと、次ページの内部 ID を示すパラメーターが含まれます。元の要求で _startTime_ と _endTime_ が指定されていなかった場合、それらは元の要求が出された時点に先行する 24 時間間隔を反映するように設定されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p136">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts. If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results. The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page. If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="6dee1-364">指定の時間の範囲にある利用可能なすべてのコンテンツのリストを作成するために、**NextPageUrl** ヘッダーがない応答を受信するまで、複数のページを取得することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-364">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="6dee1-365">リソースのフレンドリ名を取得します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-365">Retrieve resource friendly names</span></span>

<span data-ttu-id="6dee1-366">この操作は、GUID で識別されるデータ フィード内のオブジェクトのフレンドリ名を取得します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-366">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="6dee1-367">現時点でサポートされているオブジェクトは "DlpSensitiveType" のみです。</span><span class="sxs-lookup"><span data-stu-id="6dee1-367">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="6dee1-368">サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="6dee1-368">Subscription</span></span>|<span data-ttu-id="6dee1-369">説明</span><span class="sxs-lookup"><span data-stu-id="6dee1-369">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6dee1-370">**パス**</span><span class="sxs-lookup"><span data-stu-id="6dee1-370">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="6dee1-371">**パラメーター**</span><span class="sxs-lookup"><span data-stu-id="6dee1-371">**Parameters**</span></span>|<span data-ttu-id="6dee1-372">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="6dee1-372">PublisherIdentifier</span></span>|<span data-ttu-id="6dee1-373">API に対するコードを作成するベンダーのテナント GUID。</span><span class="sxs-lookup"><span data-stu-id="6dee1-373">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="6dee1-374">これは、アプリケーション GUID またはアプリケーションを使用する顧客の GUID では**ありません**。コードを記述した会社の GUID です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-374">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="6dee1-375">このパラメーターは、要求率の調整に使用します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-375">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="6dee1-376">専用のクオータを取得する場合は、このパラメーターが発行されるすべての要求で指定されていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-376">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="6dee1-377">このパラメーターの指定なしで受信したすべての要求は、同一のクオータを共有することになります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-377">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="6dee1-378">**ヘッダー**</span><span class="sxs-lookup"><span data-stu-id="6dee1-378">**Headers**</span></span>|<span data-ttu-id="6dee1-379">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="6dee1-379">Accept-Language</span></span>|<span data-ttu-id="6dee1-p139">Header to specify the desired language for localized names. For example, use "en-US" for English or "es" for Spanish. The default language (en-US) will be returned if this header is not present.</span><span class="sxs-lookup"><span data-stu-id="6dee1-p139">Header to specify the desired language for localized names. For example, use "en-US" for English or "es" for Spanish. The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="6dee1-383">**Body**</span><span class="sxs-lookup"><span data-stu-id="6dee1-383">**Body**</span></span>|<span data-ttu-id="6dee1-384">(空)</span><span class="sxs-lookup"><span data-stu-id="6dee1-384">(empty)</span></span>||
|<span data-ttu-id="6dee1-385">**応答**</span><span class="sxs-lookup"><span data-stu-id="6dee1-385">**Response**</span></span>|<span data-ttu-id="6dee1-386">JSON 配列</span><span class="sxs-lookup"><span data-stu-id="6dee1-386">JSON array</span></span>|<span data-ttu-id="6dee1-387">利用可能なコンテンツは、次のプロパティが指定された JSON オブジェクトで表されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-387">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-388"><b>id</b>: Indicates the guid of the sensitive information type.</span><span class="sxs-lookup"><span data-stu-id="6dee1-388"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="6dee1-389"><b>name</b>: The friendly name of the sensitive information type.</span><span class="sxs-lookup"><span data-stu-id="6dee1-389"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="6dee1-390">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-390">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="6dee1-391">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6dee1-391">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="6dee1-392">API 調整</span><span class="sxs-lookup"><span data-stu-id="6dee1-392">API throttling</span></span>

<span data-ttu-id="6dee1-393">Office 365 管理アクティビティ API を使用して監査ログにアクセスする組織は、発行者レベルの調整制限により制限されていました。</span><span class="sxs-lookup"><span data-stu-id="6dee1-393">Organizations that access auditing logs through the Office 365 Management Activity API were restricted by throttling limits at the publisher level.</span></span> <span data-ttu-id="6dee1-394">つまり、発行者が複数のお客様に代わってデータをプルする場合、制限はそれらすべてのお客様で共有されていました。</span><span class="sxs-lookup"><span data-stu-id="6dee1-394">This means that for a publisher pulling data on behalf of multiple customers, the limit was shared by all those customers.</span></span>

<span data-ttu-id="6dee1-395">発行者レベルの制限からテナント レベルの制限に移行しています。</span><span class="sxs-lookup"><span data-stu-id="6dee1-395">We're moving from a publisher-level limit to a tenant-level limit.</span></span> <span data-ttu-id="6dee1-396">その結果、各組織は、監査データにアクセスするために独自に完全に割り当てられた帯域幅を取得します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-396">The result is that each organization will get their own fully allocated bandwidth quota to access their auditing data.</span></span> <span data-ttu-id="6dee1-397">すべての組織には、最初に 1 分あたり 2,000 件の要求のベースラインが割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-397">All organizations are initially allocated a baseline of 2,000 requests per minute.</span></span> <span data-ttu-id="6dee1-398">これは静的な定義済みの制限ではありませんが、組織内のシート数などの要因の組み合わせでモデル化され、Office 365 および Microsoft 365 E5 組織は非 E5 組織の約 2 倍の帯域幅を取得します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-398">This is not a static, predefined limit but is modeled on a combination of factors including the number of seats in the organization and that Office 365 and Microsoft 365 E5 organizations will get approximately twice as much bandwidth as non-E5 organizations.</span></span> <span data-ttu-id="6dee1-399">また、サービスの正常性を保護するために、最大帯域幅の上限も設定されます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-399">There will also be cap on the maximum bandwidth to protect the health of the service.</span></span>

<span data-ttu-id="6dee1-400">詳細については、「Microsoft 365 での高度な監査」の「[Office 365 管理アクティビティ API への高帯域幅アクセス](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-400">For more information, see the "High-bandwidth access to the Office 365 Management Activity API" section in [Advanced audit in Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).</span></span>

> [!NOTE] 
> <span data-ttu-id="6dee1-401">それぞれのテナントは最初に最大 1 分あたり 2,000 の要求を送信できますが、Microsoft は応答速度を保証できません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-401">Even though each tenant can initially submit up to 2,000 requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="6dee1-402">応答速度は、クライアント システムのパフォーマンス、ネットワーク容量、ネットワーク速度など、さまざまな要因によって決まります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-402">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span> 

## <a name="errors"></a><span data-ttu-id="6dee1-403">エラー</span><span class="sxs-lookup"><span data-stu-id="6dee1-403">Errors</span></span>

<span data-ttu-id="6dee1-p143">サービスでエラーが検出されると、標準の HTTP エラー コードの構文を使用して、エラー応答コードが呼び出し元に報告されます。失敗した呼び出しの本体には、追加情報が単一の JSON オブジェクトとして含められます。完全な JSON エラー本体の例を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p143">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax. . Additional information is included in the body of the failed call as a single JSON object. An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="6dee1-408">コード</span><span class="sxs-lookup"><span data-stu-id="6dee1-408">Code</span></span>|<span data-ttu-id="6dee1-409">メッセージ</span><span class="sxs-lookup"><span data-stu-id="6dee1-409">Message</span></span>|
|<span data-ttu-id="6dee1-410">AF10001</span><span class="sxs-lookup"><span data-stu-id="6dee1-410">AF10001</span></span>|<span data-ttu-id="6dee1-411">要求で送信されたアクセス許可セット ({0}) に、必要なアクセス許可 **ActivityFeed.Read** が含まれていませんでした。</span><span class="sxs-lookup"><span data-stu-id="6dee1-411">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-412">{0} = the permission set in the access token.</span><span class="sxs-lookup"><span data-stu-id="6dee1-412">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-413">AF20001</span><span class="sxs-lookup"><span data-stu-id="6dee1-413">AF20001</span></span>|<span data-ttu-id="6dee1-414">Missing parameter: {0}.</span><span class="sxs-lookup"><span data-stu-id="6dee1-414">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-415">{0} = 不足しているパラメーターの名前。</span><span class="sxs-lookup"><span data-stu-id="6dee1-415">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-416">AF20002</span><span class="sxs-lookup"><span data-stu-id="6dee1-416">AF20002</span></span>|<span data-ttu-id="6dee1-p144">無効なパラメーターの種類です: {0}。 予期される種類: {1}</span><span class="sxs-lookup"><span data-stu-id="6dee1-p144">Invalid parameter type: {0}. Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-419">{0} = the name of the invalid parameter.</span><span class="sxs-lookup"><span data-stu-id="6dee1-419">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="6dee1-420">{1} = the expected type (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="6dee1-420">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-421">AF20003</span><span class="sxs-lookup"><span data-stu-id="6dee1-421">AF20003</span></span>|<span data-ttu-id="6dee1-422">指定した有効期限 {0} は、過去の日付と時刻に設定されています。</span><span class="sxs-lookup"><span data-stu-id="6dee1-422">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-423">{0} = API 呼び出しに渡される有効期限。</span><span class="sxs-lookup"><span data-stu-id="6dee1-423">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-424">AF20010</span><span class="sxs-lookup"><span data-stu-id="6dee1-424">AF20010</span></span>|<span data-ttu-id="6dee1-425">URL ({0}) で渡されたテナント ID が、アクセス トークン ({1}) で渡されたテナント ID と一致しません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-425">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-426">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="6dee1-426">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="6dee1-427">{1} = tenant ID passed in the access token</span><span class="sxs-lookup"><span data-stu-id="6dee1-427">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-428">AF20011</span><span class="sxs-lookup"><span data-stu-id="6dee1-428">AF20011</span></span>|<span data-ttu-id="6dee1-429">指定したテナント ID ({0}) は、システムに存在しないか、削除されています。</span><span class="sxs-lookup"><span data-stu-id="6dee1-429">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="6dee1-430">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="6dee1-430">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-431">AF20012</span><span class="sxs-lookup"><span data-stu-id="6dee1-431">AF20012</span></span>|<span data-ttu-id="6dee1-432">指定したテナント ID ({0}) が、システムで正しく構成されていません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-432">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="6dee1-433">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="6dee1-433">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-434">AF20013</span><span class="sxs-lookup"><span data-stu-id="6dee1-434">AF20013</span></span>|<span data-ttu-id="6dee1-435">URL ({0}) で渡されたテナント ID は、有効な GUID ではありません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-435">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="6dee1-436">{0} = tenant ID passed in the URL</span><span class="sxs-lookup"><span data-stu-id="6dee1-436">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-437">AF20020</span><span class="sxs-lookup"><span data-stu-id="6dee1-437">AF20020</span></span>|<span data-ttu-id="6dee1-438">指定したコンテンツ タイプが無効です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-438">The specified content type is not valid.</span></span>|
|<span data-ttu-id="6dee1-439">AF20021</span><span class="sxs-lookup"><span data-stu-id="6dee1-439">AF20021</span></span>|<span data-ttu-id="6dee1-p145">The webhook endpoint {{0}) could not be validated. {1}</span><span class="sxs-lookup"><span data-stu-id="6dee1-p145">The webhook endpoint {{0}) could not be validated. {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-442">{0} = webhook address.</span><span class="sxs-lookup"><span data-stu-id="6dee1-442">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="6dee1-p146">{1} = "The endpoint did not return HTTP 200." or "The address must begin with HTTPS."</span><span class="sxs-lookup"><span data-stu-id="6dee1-p146">{1} = "The endpoint did not return HTTP 200." or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-445">AF20022</span><span class="sxs-lookup"><span data-stu-id="6dee1-445">AF20022</span></span>|<span data-ttu-id="6dee1-446">指定したコンテンツ タイプのサブスクリプションがありません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-446">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="6dee1-447">AF20023</span><span class="sxs-lookup"><span data-stu-id="6dee1-447">AF20023</span></span>|<span data-ttu-id="6dee1-448">The subscription was disabled by {0}.</span><span class="sxs-lookup"><span data-stu-id="6dee1-448">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-449">{0} = "テナント管理" または "サービス管理"</span><span class="sxs-lookup"><span data-stu-id="6dee1-449">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-450">AF20030</span><span class="sxs-lookup"><span data-stu-id="6dee1-450">AF20030</span></span>|<span data-ttu-id="6dee1-451">開始時刻と終了時刻の両方を指定する (または両方を省略する) 必要があります。その時間差は 24 時間を超えてはならず、開始時刻は過去 7 日以内でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-451">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="6dee1-452">AF20031</span><span class="sxs-lookup"><span data-stu-id="6dee1-452">AF20031</span></span>|<span data-ttu-id="6dee1-453">Invalid nextPage Input: {0}.</span><span class="sxs-lookup"><span data-stu-id="6dee1-453">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-454">{0} = URL に渡された次ページ インジケーター</span><span class="sxs-lookup"><span data-stu-id="6dee1-454">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-455">AF20050</span><span class="sxs-lookup"><span data-stu-id="6dee1-455">AF20050</span></span>|<span data-ttu-id="6dee1-456">指定された ID が存在しません。</span><span class="sxs-lookup"><span data-stu-id="6dee1-456">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-457">{0} = リソース ID またはリソース URL。</span><span class="sxs-lookup"><span data-stu-id="6dee1-457">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-458">AF20051</span><span class="sxs-lookup"><span data-stu-id="6dee1-458">AF20051</span></span>|<span data-ttu-id="6dee1-p147">Content requested with the key {0} has already expired. Content older than 7 days cannot be retrieved.</span><span class="sxs-lookup"><span data-stu-id="6dee1-p147">Content requested with the key {0} has already expired. Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-461">•    {0} = resource id or resource URL</span><span class="sxs-lookup"><span data-stu-id="6dee1-461">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-462">AF20052</span><span class="sxs-lookup"><span data-stu-id="6dee1-462">AF20052</span></span>|<span data-ttu-id="6dee1-463">URL 内のコンテンツの ID {0} は無効です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-463">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-464">{0} = リソース ID またはリソース URL。</span><span class="sxs-lookup"><span data-stu-id="6dee1-464">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-465">AF20053</span><span class="sxs-lookup"><span data-stu-id="6dee1-465">AF20053</span></span>|<span data-ttu-id="6dee1-466">Accept-Language ヘッダーには、1 つの言語のみ表示可能です。</span><span class="sxs-lookup"><span data-stu-id="6dee1-466">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="6dee1-467">AF20054</span><span class="sxs-lookup"><span data-stu-id="6dee1-467">AF20054</span></span>|<span data-ttu-id="6dee1-468">Accept-Language ヘッダーに無効な構文があります。</span><span class="sxs-lookup"><span data-stu-id="6dee1-468">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="6dee1-469">AF429</span><span class="sxs-lookup"><span data-stu-id="6dee1-469">AF429</span></span>|<span data-ttu-id="6dee1-470">要求数が多すぎます。</span><span class="sxs-lookup"><span data-stu-id="6dee1-470">Too many requests.</span></span> <span data-ttu-id="6dee1-471">メソッド={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="6dee1-471">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6dee1-472">{0} = HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="6dee1-472">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="6dee1-473">{1} = PublisherIdentifier として使用されたテナント GUID</span><span class="sxs-lookup"><span data-stu-id="6dee1-473">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="6dee1-474">AF50000</span><span class="sxs-lookup"><span data-stu-id="6dee1-474">AF50000</span></span>|<span data-ttu-id="6dee1-p149">内部エラーが発生しました。要求を再試行してください。</span><span class="sxs-lookup"><span data-stu-id="6dee1-p149">An internal error occurred. Retry the request.</span></span>|
