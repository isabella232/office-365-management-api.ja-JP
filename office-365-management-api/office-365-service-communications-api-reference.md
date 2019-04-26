---
ms.TocTitle: Office 365 Service Communications API reference (preview)
title: Office 365 サービス通信 API リファレンス (プレビュー)
description: この API を使用して、Get Services、Get Current Status、Get Historical Status、Get Messages のデータにアクセスします。
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 9b38c4ee73f18bf10c7fa7cbb5b323740dfb5a7e
ms.sourcegitcommit: 5b1eaeb7f262b7b9f7ab30ccb9f10878814153ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "32223974"
---
# <a name="office-365-service-communications-api-reference-preview"></a><span data-ttu-id="071b1-103">Office 365 サービス通信 API リファレンス (プレビュー)</span><span class="sxs-lookup"><span data-stu-id="071b1-103">Office 365 Service Communications API reference (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="071b1-104">このドキュメントで取り上げる機能は、現時点ではプレビュー段階にあります。</span><span class="sxs-lookup"><span data-stu-id="071b1-104">This documentation covers features that are currently in preview.</span></span>

<span data-ttu-id="071b1-105">Office 365 サービス通信 API V2 を使用して、次のデータにアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="071b1-105">You can use the Office 365 Service Communications API V2 to access the following data:</span></span>

- <span data-ttu-id="071b1-106">**Get Services**:サブスクライブしているサービスのリストを取得します。</span><span class="sxs-lookup"><span data-stu-id="071b1-106">**Get Services**: Get the list of subscribed services.</span></span>
    
- <span data-ttu-id="071b1-107">**Get Current Status**:現在進行中のサービス インシデントやメンテナンス イベントのリアルタイム ビューを取得します。</span><span class="sxs-lookup"><span data-stu-id="071b1-107">**Get Current Status**: Get a real-time view of current and ongoing service incidents and maintenance events</span></span>
    
- <span data-ttu-id="071b1-108">**Get Historical Status**:サービス インシデントやメンテナンス イベントなどの、サービス正常性の履歴ビューを取得します。</span><span class="sxs-lookup"><span data-stu-id="071b1-108">**Get Historical Status**: Get a historical view of service health, including service incidents and maintenance events.</span></span>
    
- <span data-ttu-id="071b1-109">**Get Messages**:インシデント、計画済みメンテナンス、およびメッセージ センター通信を検索します。</span><span class="sxs-lookup"><span data-stu-id="071b1-109">**Get Messages**: Find Incident, Planned Maintenance, and Message Center communications.</span></span>
    
<span data-ttu-id="071b1-110">現時点では、Office 365 サービス通信 API には、以下のサービスについてのデータが含まれています。Dynamics CRM、Dynamics Marketing、Exchange Online、Exchange Online Protection、ID サービス、モバイル デバイス管理、Office 365 パートナー管理センター、OneDrive for Business、Parature、Power BI for Office 365、Rights Management Service、SharePoint Online、SHD Admin、Skype for Business、Social Engagement、および Yammer Enterprise。</span><span class="sxs-lookup"><span data-stu-id="071b1-110">Currently, the Office 365 Service Communications API contains data for the following services: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Identity Service, Mobile Device Management, Office 365 Partner Admin Center, OneDrive for Business, Parature, OneDrive for Business, Power BI for Office 365, Rights Management Service, SharePoint Online, SHD Admin, Skype for Business, Social Engagement, and Yammer Enterprise.</span></span>

## <a name="the-fundamentals"></a><span data-ttu-id="071b1-111">基本事項</span><span class="sxs-lookup"><span data-stu-id="071b1-111">The fundamentals</span></span>

<span data-ttu-id="071b1-112">API のルート URL には、操作の範囲を単一のテナントに限定するテナント ID が含まれています。</span><span class="sxs-lookup"><span data-stu-id="071b1-112">The root URL of the API includes a tenant identifier that scopes the operations to a single tenant:</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

<span data-ttu-id="071b1-113">**Office 365 サービス通信 API** は、任意の Web 言語と、HTTPS および X.509 証明書をサポートするホスト環境とを用いてソリューションを開発できる、REST サービスです。</span><span class="sxs-lookup"><span data-stu-id="071b1-113">The **Office 365 Service Communications API** is a REST service that allows you to develop solutions using any web language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="071b1-114">この API は、認証と承認に **Microsoft Azure Active Directory** および **OAuth2** プロトコルを使用します。</span><span class="sxs-lookup"><span data-stu-id="071b1-114">The API relies on **Microsoft Azure Active Directory** and the **OAuth2** protocol for authentication and authorization.</span></span> <span data-ttu-id="071b1-115">アプリケーションからこの API にアクセスする場合は、まず Azure AD で登録し、適切な範囲を指定したアクセス許可で設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="071b1-115">To access the API from your application, you'll need to first register it in Azure AD and configure it with permissions at the appropriate scope.</span></span> <span data-ttu-id="071b1-116">これにより、アプリケーションで、API を呼び出すために必要な OAuth2 アクセス トークンを要求できます。</span><span class="sxs-lookup"><span data-stu-id="071b1-116">This will enable your application to request OAuth2 access tokens necessary for calling the API.</span></span> <span data-ttu-id="071b1-117">Azure AD でのアプリケーションの登録および設定の詳細については、「[Office 365 管理 API の概要](get-started-with-office-365-management-apis.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="071b1-117">You can find more information about registering and configuring an application in Azure AD at [Office 365 Management APIs getting started](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="071b1-118">すべての API 要求は、**ServiceHealth.Read** 要求が含まれている Azure AD から取得した有効な OAuth2 JWT のアクセス トークンがある、承認 HTTP ヘッダーを必要とします。テナント ID は、ルート URL のテナント ID と一致していなければなりません。</span><span class="sxs-lookup"><span data-stu-id="071b1-118">All API requests require an Authorization HTTP header that has a valid OAuth2 JWT access token obtained from Azure AD that contains the **ServiceHealth.Read** claim; and the tenant identifier must match the tenant identifier in the root URL.</span></span>

```json
Authorization: Bearer {OAuth2 token}
```

<span data-ttu-id="071b1-119">**要求ヘッダー**</span><span class="sxs-lookup"><span data-stu-id="071b1-119">**Request headers**</span></span>

<span data-ttu-id="071b1-120">以下に示すのは、Office 365 サービス通信 API のすべての操作に対してサポートされている要求ヘッダーです。</span><span class="sxs-lookup"><span data-stu-id="071b1-120">These are the supported request headers for all Office 365 Service Communications API operations.</span></span>

|<span data-ttu-id="071b1-121">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="071b1-121">Header</span></span>|<span data-ttu-id="071b1-122">説明</span><span class="sxs-lookup"><span data-stu-id="071b1-122">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="071b1-123">**Accept (省略可能)**</span><span class="sxs-lookup"><span data-stu-id="071b1-123">**Accept (Optional)**</span></span>|<span data-ttu-id="071b1-124">以下が、受け入れられる応答の表記です。</span><span class="sxs-lookup"><span data-stu-id="071b1-124">The following are acceptable representations for the response:</span></span><br/><span data-ttu-id="071b1-125">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="071b1-125">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="071b1-126">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="071b1-126">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="071b1-127">[ヘッダーが指定されていない場合の既定値] **application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="071b1-127">[The default if header not specified] **application/json;odata.metadata=none**</span></span>|
|<span data-ttu-id="071b1-128">**Authorization (必須)**</span><span class="sxs-lookup"><span data-stu-id="071b1-128">**Authorization (Required)**</span></span>|<span data-ttu-id="071b1-129">要求の認証トークン (Bearer JWT Azure トークン)。</span><span class="sxs-lookup"><span data-stu-id="071b1-129">Authorization token (Bearer JWT Azure AD Token) for the request.</span></span>|


<br/>

<span data-ttu-id="071b1-130">**応答ヘッダー**</span><span class="sxs-lookup"><span data-stu-id="071b1-130">**Response headers**</span></span>

<span data-ttu-id="071b1-131">以下に示すのは、Office 365 サービス通信 API のすべての操作に対して返される応答ヘッダーです。</span><span class="sxs-lookup"><span data-stu-id="071b1-131">These are the response headers returned for all Office 365 Service Communications API operations:</span></span>

|<span data-ttu-id="071b1-132">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="071b1-132">Header</span></span>|<span data-ttu-id="071b1-133">説明</span><span class="sxs-lookup"><span data-stu-id="071b1-133">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="071b1-134">**コンテンツ長**</span><span class="sxs-lookup"><span data-stu-id="071b1-134">**Content-Length**</span></span>|<span data-ttu-id="071b1-135">応答本体の長さです。</span><span class="sxs-lookup"><span data-stu-id="071b1-135">The length of the response body.</span></span>|
|<span data-ttu-id="071b1-136">**コンテンツ タイプ**</span><span class="sxs-lookup"><span data-stu-id="071b1-136">**Content-Type**</span></span>|<span data-ttu-id="071b1-137">以下が応答の表記です。</span><span class="sxs-lookup"><span data-stu-id="071b1-137">Representation of the response:</span></span><br/><span data-ttu-id="071b1-138">**application/json**</span><span class="sxs-lookup"><span data-stu-id="071b1-138">**application/json**</span></span><br/><span data-ttu-id="071b1-139">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="071b1-139">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="071b1-140">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="071b1-140">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="071b1-141">**application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="071b1-141">**application/json;odata.metadata=none**</span></span><br/><span data-ttu-id="071b1-142">**odata.streaming=true**</span><span class="sxs-lookup"><span data-stu-id="071b1-142">**odata.streaming=true**</span></span>|
|<span data-ttu-id="071b1-143">**Cache-Control**</span><span class="sxs-lookup"><span data-stu-id="071b1-143">**Cache-Control**</span></span>|<span data-ttu-id="071b1-144">要求/応答チェーンに沿うすべてのキャッシュ機構が従う必要があるディレクティブを指定するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="071b1-144">Used to specify directives that all caching mechanisms along the request/response chain must obey.</span></span>|
|<span data-ttu-id="071b1-145">**Pragma**</span><span class="sxs-lookup"><span data-stu-id="071b1-145">**Pragma**</span></span>|<span data-ttu-id="071b1-146">実装固有の動作。</span><span class="sxs-lookup"><span data-stu-id="071b1-146">Implementation-specific behaviors.</span></span>|
|<span data-ttu-id="071b1-147">**Expires**</span><span class="sxs-lookup"><span data-stu-id="071b1-147">**Expires**</span></span>|<span data-ttu-id="071b1-148">クライアントがリソースを有効期限切れにする必要があるタイミング。</span><span class="sxs-lookup"><span data-stu-id="071b1-148">When the client should make the resource expire.</span></span>|
|<span data-ttu-id="071b1-149">**X-Activity-Id**</span><span class="sxs-lookup"><span data-stu-id="071b1-149">**X-Activity-Id**</span></span>|<span data-ttu-id="071b1-150">サーバー生成のアクティビティ ID。</span><span class="sxs-lookup"><span data-stu-id="071b1-150">The server-generated activity Id.</span></span>|
|<span data-ttu-id="071b1-151">**OData-Version**</span><span class="sxs-lookup"><span data-stu-id="071b1-151">**OData-Version**</span></span>|<span data-ttu-id="071b1-152">サポートされている OData のバージョン (4.0)。</span><span class="sxs-lookup"><span data-stu-id="071b1-152">The supported OData Version (4.0).</span></span>|
|<span data-ttu-id="071b1-153">**Date**</span><span class="sxs-lookup"><span data-stu-id="071b1-153">**Date**</span></span>|<span data-ttu-id="071b1-154">サーバーから応答が送信されたときの、UTC 形式の日付。</span><span class="sxs-lookup"><span data-stu-id="071b1-154">The date in UTC when the response was sent from the server.</span></span>|
|<span data-ttu-id="071b1-155">**X-Time-Taken**</span><span class="sxs-lookup"><span data-stu-id="071b1-155">**X-Time-Taken**</span></span>|<span data-ttu-id="071b1-156">応答の生成にかかった時間 (ミリ秒)。</span><span class="sxs-lookup"><span data-stu-id="071b1-156">The time it took to generate the response (ms).</span></span>|
|<span data-ttu-id="071b1-157">**X-Instance-Name**</span><span class="sxs-lookup"><span data-stu-id="071b1-157">**X-Instance-Name**</span></span>|<span data-ttu-id="071b1-158">(デバッグ目的で) 応答の生成に使用される Azure インスタンスの ID。</span><span class="sxs-lookup"><span data-stu-id="071b1-158">The identifier of the Azure instance used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="071b1-159">**Server**</span><span class="sxs-lookup"><span data-stu-id="071b1-159">**Server**</span></span>|<span data-ttu-id="071b1-160">(デバッグ目的で) 応答を生成するために使用されるサーバー。</span><span class="sxs-lookup"><span data-stu-id="071b1-160">The server used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="071b1-161">**X-ASPNET-Version**</span><span class="sxs-lookup"><span data-stu-id="071b1-161">**X-ASPNET-Version**</span></span>|<span data-ttu-id="071b1-162">(デバッグ目的で) 応答を生成したサーバーにより使用される ASP.Net のバージョン。</span><span class="sxs-lookup"><span data-stu-id="071b1-162">The version of ASP.Net used by the server that generated the response (for debugging purposes).</span></span>|
|<span data-ttu-id="071b1-163">**X-Powered-By**</span><span class="sxs-lookup"><span data-stu-id="071b1-163">**X-Powered-By**</span></span>|<span data-ttu-id="071b1-164">(デバッグ目的で) 応答を生成したサーバーで使用されるテクノロジ。</span><span class="sxs-lookup"><span data-stu-id="071b1-164">The technologies used in the server that generated the response (for debugging purposes).</span></span>|

<br/>

<span data-ttu-id="071b1-165">以下に示すのは、Office 365 サービス通信 API の操作です。</span><span class="sxs-lookup"><span data-stu-id="071b1-165">Following are the Office 365 Service Communications API operations.</span></span>


## <a name="get-services"></a><span data-ttu-id="071b1-166">Get Services</span><span class="sxs-lookup"><span data-stu-id="071b1-166">Get Services</span></span>

<span data-ttu-id="071b1-167">サブスクライブしているサービスのリストを返します。</span><span class="sxs-lookup"><span data-stu-id="071b1-167">Returns the list of subscribed services.</span></span>

||<span data-ttu-id="071b1-168">サービス</span><span class="sxs-lookup"><span data-stu-id="071b1-168">Service</span></span>|<span data-ttu-id="071b1-169">説明</span><span class="sxs-lookup"><span data-stu-id="071b1-169">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="071b1-170">**パス**</span><span class="sxs-lookup"><span data-stu-id="071b1-170">**Path**</span></span>| `/Services`||
|<span data-ttu-id="071b1-171">**クエリ オプション**</span><span class="sxs-lookup"><span data-stu-id="071b1-171">**Query-option**</span></span>|<span data-ttu-id="071b1-172">$select</span><span class="sxs-lookup"><span data-stu-id="071b1-172">$select</span></span>|<span data-ttu-id="071b1-173">プロパティのサブセットを選択します。</span><span class="sxs-lookup"><span data-stu-id="071b1-173">Pick a subset of properties.</span></span>|
|<span data-ttu-id="071b1-174">**応答**</span><span class="sxs-lookup"><span data-stu-id="071b1-174">**Response**</span></span>|<span data-ttu-id="071b1-175">"Service" エンティティのリスト</span><span class="sxs-lookup"><span data-stu-id="071b1-175">List of "Service" entities</span></span>|<span data-ttu-id="071b1-176">"Service" エンティティには、"Id" (文字列)、"DisplayName" (文字列)、および "FeatureNames" (文字列のリスト) が含まれています。</span><span class="sxs-lookup"><span data-stu-id="071b1-176">"Service" entity contains "Id" (String), "DisplayName" (String), and "FeatureNames" (list of Strings).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="071b1-177">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-177">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

#### <a name="sample-response"></a><span data-ttu-id="071b1-178">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-178">Sample response</span></span>

```json
{
    "value": [
        {
            "Id": "Exchange",
            "DisplayName": "Exchange Online",
            "FeatureNames": [
                "Sign-in",
                "E-Mail and calendar access",
                "E-Mail timely delivery",
                "Management and Provisioning",
                "Voice mail"
            ]
        },
        {
            "Id": "Lync",
            "DisplayName": "Lync Online",
            "FeatureNames": [
                "Audio and Video",
                "Federation",
                "Management and Provisioning",
                "Sign-In",
                "All Features",
                "Dial-In Conferencing",
                "Online Meetings",
                "Instant Messaging",
                "Presence",
                "Mobility"
            ]
        }
    ]
}

```


## <a name="get-current-status"></a><span data-ttu-id="071b1-179">現在の状態の取得</span><span class="sxs-lookup"><span data-stu-id="071b1-179">Get Current Status</span></span>

<span data-ttu-id="071b1-180">過去 24 時間のサービスの状態を返します。</span><span class="sxs-lookup"><span data-stu-id="071b1-180">Returns the status of the service over the previous 24 hours.</span></span>

||<span data-ttu-id="071b1-181">サービス</span><span class="sxs-lookup"><span data-stu-id="071b1-181">Service</span></span>|<span data-ttu-id="071b1-182">説明</span><span class="sxs-lookup"><span data-stu-id="071b1-182">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="071b1-183">**パス**</span><span class="sxs-lookup"><span data-stu-id="071b1-183">**Path**</span></span>| `/CurrentStatus`||
|<span data-ttu-id="071b1-184">**フィルター**</span><span class="sxs-lookup"><span data-stu-id="071b1-184">**Filter**</span></span>|<span data-ttu-id="071b1-185">ワークロード</span><span class="sxs-lookup"><span data-stu-id="071b1-185">Workload</span></span>|<span data-ttu-id="071b1-186">ワークロードでフィルター (文字列、既定値: all)。</span><span class="sxs-lookup"><span data-stu-id="071b1-186">Filter by workload (String, default: all).</span></span>|
|<span data-ttu-id="071b1-187">**クエリ オプション**</span><span class="sxs-lookup"><span data-stu-id="071b1-187">**Query-option**</span></span>|<span data-ttu-id="071b1-188">$select</span><span class="sxs-lookup"><span data-stu-id="071b1-188">$select</span></span>|<span data-ttu-id="071b1-189">プロパティのサブセットを選択します。</span><span class="sxs-lookup"><span data-stu-id="071b1-189">Pick a subset of properties.</span></span>|
|<span data-ttu-id="071b1-190">**応答**</span><span class="sxs-lookup"><span data-stu-id="071b1-190">**Response**</span></span>|<span data-ttu-id="071b1-191">"WorkloadStatus" エンティティのリスト。</span><span class="sxs-lookup"><span data-stu-id="071b1-191">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="071b1-192">"WorkloadStatus" エンティティには、"Id" (文字列)、"Workload" (文字列)、"StatusTime"(DateTimeOffset)、"WorkloadDisplayName" (文字列)、"Status" (文字列)、"IncidentIds" (文字列のリスト)、FeatureGroupStatusCollection ("FeatureStatus" のリスト) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="071b1-192">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="071b1-193">"FeatureStatus" エンティティには、"Feature" (文字列)、"FeatureGroupDisplayName" (文字列)、"FeatureStatus" (文字列) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="071b1-193">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="071b1-194">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-194">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="071b1-195">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-195">Sample response</span></span>

```json
{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Lync",
            "Workload": "Lync",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Lync Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "AudioVideo",
                    "FeatureGroupDisplayName": "Audio and Video",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Federation",
                    "FeatureGroupDisplayName": "Federation",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "ManagementandProvisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Sign-In",
                    "FeatureGroupDisplayName": "Sign-In",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "All",
                    "FeatureGroupDisplayName": "All Features",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "DialInConferencing",
                    "FeatureGroupDisplayName": "Dial-In Conferencing",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "OnlineMeetings",
                    "FeatureGroupDisplayName": "Online Meetings",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "InstantMessaging",
                    "FeatureGroupDisplayName": "Instant Messaging",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Presence",
                    "FeatureGroupDisplayName": "Presence",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Mobility",
                    "FeatureGroupDisplayName": "Mobility",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        }
    ]
}

```


## <a name="get-historical-status"></a><span data-ttu-id="071b1-196">Get Historical Status</span><span class="sxs-lookup"><span data-stu-id="071b1-196">Get Historical Status</span></span>

<span data-ttu-id="071b1-197">特定の時間範囲内のサービスの履歴状態を、日単位で返します。</span><span class="sxs-lookup"><span data-stu-id="071b1-197">Returns the historical status of the service, by day, over a certain time range.</span></span>

||<span data-ttu-id="071b1-198">サービス</span><span class="sxs-lookup"><span data-stu-id="071b1-198">Service</span></span>|<span data-ttu-id="071b1-199">説明</span><span class="sxs-lookup"><span data-stu-id="071b1-199">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="071b1-200">**パス**</span><span class="sxs-lookup"><span data-stu-id="071b1-200">**Path**</span></span>| `/HistoricalStatus`||
|<span data-ttu-id="071b1-201">**Filters**</span><span class="sxs-lookup"><span data-stu-id="071b1-201">**Filters**</span></span>|<span data-ttu-id="071b1-202">ワークロード</span><span class="sxs-lookup"><span data-stu-id="071b1-202">Workload</span></span>|<span data-ttu-id="071b1-203">ワークロードでフィルター (文字列、既定値: all)。</span><span class="sxs-lookup"><span data-stu-id="071b1-203">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="071b1-204">StatusTime</span><span class="sxs-lookup"><span data-stu-id="071b1-204">StatusTime</span></span>|<span data-ttu-id="071b1-205">StatusTime より後の日付でフィルター処理します (DateTimeOffset、既定値: ge CurrentTime - 7 日)。</span><span class="sxs-lookup"><span data-stu-id="071b1-205">Filter by days greater than StatusTime (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
|<span data-ttu-id="071b1-206">**クエリ オプション**</span><span class="sxs-lookup"><span data-stu-id="071b1-206">**Query-option**</span></span>|<span data-ttu-id="071b1-207">$select</span><span class="sxs-lookup"><span data-stu-id="071b1-207">$select</span></span>|<span data-ttu-id="071b1-208">プロパティのサブセットを選択します。</span><span class="sxs-lookup"><span data-stu-id="071b1-208">Pick a subset of properties.</span></span>|
|<span data-ttu-id="071b1-209">**応答**</span><span class="sxs-lookup"><span data-stu-id="071b1-209">**Response**</span></span>|<span data-ttu-id="071b1-210">"WorkloadStatus" エンティティのリスト。</span><span class="sxs-lookup"><span data-stu-id="071b1-210">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="071b1-211">"WorkloadStatus" エンティティには、"Id" (文字列)、"Workload" (文字列)、"StatusTime"(DateTimeOffset)、"WorkloadDisplayName" (文字列)、"Status" (文字列)、"IncidentIds" (文字列のリスト)、FeatureGroupStatusCollection ("FeatureStatus" のリスト) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="071b1-211">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="071b1-212">"FeatureStatus" エンティティには、"Feature" (文字列)、"FeatureGroupDisplayName" (文字列)、"FeatureStatus" (文字列) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="071b1-212">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="071b1-213">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-213">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="071b1-214">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-214">Sample response</span></span>

```json
{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-10T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "InformationAvailable",
            "IncidentIds": [
                "EX20870"
            ],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "InformationAvailable"
                }
            ]
        }
    ]
}


```


## <a name="get-messages"></a><span data-ttu-id="071b1-215">Get Messages</span><span class="sxs-lookup"><span data-stu-id="071b1-215">Get Messages</span></span>

<span data-ttu-id="071b1-p102">特定の時間範囲内のサービスに関するメッセージを返します。"サービス インシデント"、"計画済みメンテナンス"、または "メッセージ センター" メッセージをフィルター処理するためのタイプ フィルターを使用します。</span><span class="sxs-lookup"><span data-stu-id="071b1-p102">Returns the messages about the service over a certain time range. Use the type filter to filter for "Service Incident", "Planned Maintenance", or "Message Center" messages.</span></span>

||<span data-ttu-id="071b1-218">サービス</span><span class="sxs-lookup"><span data-stu-id="071b1-218">Service</span></span>|<span data-ttu-id="071b1-219">説明</span><span class="sxs-lookup"><span data-stu-id="071b1-219">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="071b1-220">**パス**</span><span class="sxs-lookup"><span data-stu-id="071b1-220">**Path**</span></span>| `/Messages`||
|<span data-ttu-id="071b1-221">**Filters**</span><span class="sxs-lookup"><span data-stu-id="071b1-221">**Filters**</span></span>|<span data-ttu-id="071b1-222">ワークロード</span><span class="sxs-lookup"><span data-stu-id="071b1-222">Workload</span></span>|<span data-ttu-id="071b1-223">ワークロードでフィルター (文字列、既定値: all)。</span><span class="sxs-lookup"><span data-stu-id="071b1-223">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="071b1-224">StartTime</span><span class="sxs-lookup"><span data-stu-id="071b1-224">StartTime</span></span>|<span data-ttu-id="071b1-225">開始時刻でフィルター処理します (DateTimeOffset、既定値: ge CurrentTime - 7 日)。</span><span class="sxs-lookup"><span data-stu-id="071b1-225">Filter by Start Time (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
||<span data-ttu-id="071b1-226">EndTime</span><span class="sxs-lookup"><span data-stu-id="071b1-226">EndTime</span></span>|<span data-ttu-id="071b1-227">終了時刻でフィルター処理します (DateTimeOffset、既定値: le CurrentTime)。</span><span class="sxs-lookup"><span data-stu-id="071b1-227">Filter by End Time (DateTimeOffset, default: le CurrentTime).</span></span>|
||<span data-ttu-id="071b1-228">MessageType</span><span class="sxs-lookup"><span data-stu-id="071b1-228">MessageType</span></span>|<span data-ttu-id="071b1-229">メッセージの種類でフィルター処理します (文字列、既定値: all)。</span><span class="sxs-lookup"><span data-stu-id="071b1-229">Filter by MessageType (String, default: all).</span></span>|
||<span data-ttu-id="071b1-230">ID</span><span class="sxs-lookup"><span data-stu-id="071b1-230">ID</span></span>|<span data-ttu-id="071b1-231">ID でフィルター処理します (文字列、既定値: all)。</span><span class="sxs-lookup"><span data-stu-id="071b1-231">Filter by ID (String, default: all).</span></span>|
|<span data-ttu-id="071b1-232">**クエリ オプション**</span><span class="sxs-lookup"><span data-stu-id="071b1-232">**Query-option**</span></span>|<span data-ttu-id="071b1-233">$select</span><span class="sxs-lookup"><span data-stu-id="071b1-233">$select</span></span>|<span data-ttu-id="071b1-234">プロパティのサブセットを選択します。</span><span class="sxs-lookup"><span data-stu-id="071b1-234">Pick a subset of properties.</span></span>|
||<span data-ttu-id="071b1-235">$top</span><span class="sxs-lookup"><span data-stu-id="071b1-235">$top</span></span>|<span data-ttu-id="071b1-236">結果の最上位数を選択します (既定値および最大値 $top = 100)。</span><span class="sxs-lookup"><span data-stu-id="071b1-236">Pick the top number of results (default and max $top=100).</span></span>|
||<span data-ttu-id="071b1-237">$skip</span><span class="sxs-lookup"><span data-stu-id="071b1-237">$skip</span></span>|<span data-ttu-id="071b1-238">結果の数をスキップします (既定値: $skip = 0)。</span><span class="sxs-lookup"><span data-stu-id="071b1-238">Skip number of results (default: $skip=0).</span></span>|
|<span data-ttu-id="071b1-239">**応答**</span><span class="sxs-lookup"><span data-stu-id="071b1-239">**Response**</span></span>|<span data-ttu-id="071b1-240">"Message" エンティティのリスト。</span><span class="sxs-lookup"><span data-stu-id="071b1-240">List of "Message" entities.</span></span>|<span data-ttu-id="071b1-241">"Message" エンティティには、"Id" (文字列)、"StartTime" (DateTimeOffset)、"EndTime" (DateTimeOffset)、"Status" (文字列)、"Messages" ("MessageHistory" エンティティのリスト)、"LastUpdatedTime" (DateTimeOffset)、"Workload" (文字列)、"WorkloadDisplayName" (文字列)、"Feature" (文字列)、"FeatureDisplayName" (文字列)、"MessageType" (列挙、既定: all) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="071b1-241">"Message" entity contains "Id" (String), "StartTime" (DateTimeOffset), "EndTime" (DateTimeOffset), "Status" (String), "Messages" (list of "MessageHistory" entity), "LastUpdatedTime" (DateTimeOffset), "Workload" (String), "WorkloadDisplayName" (String), "Feature" (String), "FeatureDisplayName" (String), "MessageType" (Enum, default: all).</span></span><br/><br/><span data-ttu-id="071b1-242">"MessageHistory" エンティティには、"PublishedTime" (DateTimeOffset)、"MessageText" (文字列) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="071b1-242">"MessageHistory" entity contains "PublishedTime" (DateTimeOffset), "MessageText" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="071b1-243">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-243">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="071b1-244">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="071b1-244">Sample response</span></span>

```json
{
 {
    "value": [
        {
            "Id": "EX20119",
            "Name": "EX20119",
            "Title": null,
            "StartTime": "2015-04-01T22:25:00Z",
            "EndTime": "2015-04-07T21:48:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-01T22:34:28.76Z",
                    "MessageText": "Current Status: Engineers are investigating an issue in which some customers may be experiencing problems accessing or using Exchange Online services or features. This event is actively being investigated. More information will be provided shortly."
                },
                {
                    "PublishedTime": "2015-04-03T18:45:32.56Z",
                    "MessageText": "Current Status: Engineers are implementing a fix within the affected infrastructure to remediate Exchange Online archive access issues. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client.\n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \n\nNext Update by: Monday, April 6, 2015, at 9:00 PM UTC\n"
                },
                {
                    "PublishedTime": "2015-04-06T21:17:34.007Z",
                    "MessageText": "Current Status: Deployment of the fix is almost complete. Engineers are monitoring service health to ensure the issue has been remediated. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client. \n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues. \n\nNext Update by: Tuesday, April 7, 2015, at 10:00 PM UTC "
                },
                {
                    "PublishedTime": "2015-04-08T21:54:49.06Z",
                    "MessageText": "Final Status: Engineers have implemented a fix which remediated end-user impact. \r\n\r\nUser Experience: Affected users were unable to access online archives when using Outlook Web App (OWA).\r\n\r\nCustomer Impact: Customer impact appears to have been limited. This issue only affected hybrid customers.\r\n\r\nIncident Start Time: Monday, March 30, 2015, at 9:28 AM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 8:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the monitoring infrastructure for improvements as this event was reported by customers before an alert prompted a high priority investigation. \r\n\r\nA post-incident report will be available on the Service Health Dashboard within five business days."
                }
            ],
            "LastUpdatedTime": "2015-04-08T21:54:49.55Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        },
        {
            "Id": "EX20789",
            "Name": "EX20789",
            "Title": null,
            "StartTime": "2015-04-06T20:00:00Z",
            "EndTime": "2015-04-07T23:00:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-07T23:26:44.643Z",
                    "MessageText": "Final Status: Engineers have validated that the deployed fix has resolved the issue and that service is restored.\r\n\r\nUser Experience: Affected users were unable to send or receive email while using Exchange Web Services (EWS) on their mobile devices.\r\n\r\nCustomer Impact: Customer impact appeared to be limited during this event. This issue was only affecting customers that use third-party Mobile Device Management software from Good Technology. As a workaround to provide immediate relief from impact, engineers implemented a configuration change for customers who reported this issue to Microsoft Support.\r\n\r\nIncident Start Time: Wednesday, April 1, 2015, at 2:00 PM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 10:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing efforts to improve service resiliency, an update was deployed to the infrastructure that facilitates connections from multiple Exchange Online protocols to mailbox databases. The update, however, contained a code issue that caused connectivity issues in some scenarios. \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the infrastructure update process to prevent reoccurrences of this scenario.\r\n\r\nPlease consider this service notification the final update on the event."
               }
            ],
            "LastUpdatedTime": "2015-04-07T23:26:45.08Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        }
    ]
}

```


## <a name="errors"></a><span data-ttu-id="071b1-245">エラー</span><span class="sxs-lookup"><span data-stu-id="071b1-245">Errors</span></span>

<span data-ttu-id="071b1-p103">サービスでエラーが検出されると、標準の HTTP エラー コードの構文を使用して、エラー応答コードが呼び出し元に報告されます。[OData V4 仕様](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html)に従って、失敗した呼び出しの本体には、追加情報が単一の JSON オブジェクトとして含められます。完全な JSON エラー本体の例を以下に示します。</span><span class="sxs-lookup"><span data-stu-id="071b1-p103">When the service encounters an error, it reports the error response code to the caller, using standard HTTP error-code syntax. As per [OData V4 specification](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), additional information is included in the body of the failed call as a single JSON object. The following is an example of a full JSON error body:</span></span>


```json

{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}

```

