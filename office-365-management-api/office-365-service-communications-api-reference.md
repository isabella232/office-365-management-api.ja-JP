---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Service Communications API reference
title: Office 365 サービス通信 API リファレンス
description: この API を使用して、Get Services、Get Current Status、Get Historical Status、Get Messages のデータにアクセスします。
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
ms.localizationpriority: high
ms.openlocfilehash: 32a1304006d81f5d37deedb369dd63ae41da24a9
ms.sourcegitcommit: 6becab1db19ca810b10a3563a5e4c9dd097aa6ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2021
ms.locfileid: "58506196"
---
# <a name="office-365-service-communications-api-reference"></a>Office 365 サービス通信 API リファレンス

> [!IMPORTANT]
> Microsoft Graph てサービスの正常性とAPI 通信が現在利用可能です。 Microsoft Graph API は、この記事に記載されているサービス通信 API に取って代わるものです。 2021 年 12 月 17 日以降、サービス通信 API の従来バージョンは廃止されます。 新しい Microsoft Graph API の詳細については、「[Microsoft Graph を使用してサービスの正常性と通信にアクセスするための概要](/graph/service-communications-concept-overview)」を参照してください。

Office 365 サービス通信 API V2 を使用して、次のデータにアクセスできます。

- **Get Services**:サブスクライブしているサービスのリストを取得します。

- **Get Current Status**: 現在進行中のサービス インシデントのリアルタイム ビューを取得します。

- **Get Historical Status**: サービス インシデントの過去のビューを取得します。

- **Get Messages**: インシデントとメッセージ センター通信を検索します。

現在、Office 365 サービス通信 API には、Office 365、Yammer、Dynamics CRM および Microsoft Intune のクラウド サービスのデータが含まれます。

## <a name="the-fundamentals"></a>基本事項

API のルート URL には、操作の範囲を単一のテナントに限定するテナント ID が含まれています。

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

**Office 365 Service Communications API** は、 REST サービスであり、Web 言語を使用してソリューションの開発を可能し、HTTPS および X.509 認証をサポートする環境をホストします。API は、認証と承認のために、**Microsoft Azure Active Directory** と **OAuth2** プロトコルに依存します。ご使用のアプリから API にアクセスするには、まずそれを Azure AD で登録して、適切なスコープのアクセス許可を持たせて構成します。これにより、ご使用のアプリは API の呼び出しに必要な OAuth2 アクセス トークンを要求できるようになります。Azure AD でのアプリの登録と構成の詳細については、「[Office 365 管理 API の概要](get-started-with-office-365-management-apis.md)」.を参照してください。

すべての API 要求は、**ServiceHealth.Read** 要求が含まれている Azure AD から取得した有効な OAuth2 JWT のアクセス トークンがある、承認 HTTP ヘッダーを必要とします。テナント ID は、ルート URL のテナント ID と一致していなければなりません。

```json
Authorization: Bearer {OAuth2 token}
```

### <a name="request-headers"></a>要求ヘッダー

以下に示すのは、Office 365 サービス通信 API のすべての操作に対してサポートされている要求ヘッダーです。

|ヘッダー|説明|
|:-----|:-----|
|**Accept (省略可能)**|以下が、受け入れられる応答の表記です。<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>[ヘッダーが指定されていない場合の既定値] **application/json;odata.metadata=none**|
|**Authorization (必須)**|要求の認証トークン (Bearer JWT Azure トークン)。|

<br/>

### <a name="response-headers"></a>応答ヘッダー

以下に示すのは、Office 365 サービス通信 API のすべての操作に対して返される応答ヘッダーです。

|ヘッダー|説明|
|:-----|:-----|
|**コンテンツ長**|応答本体の長さです。|
|**コンテンツ タイプ**|以下が応答の表記です。<br/>**application/json**<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>**application/json;odata.metadata=none**<br/>**odata.streaming=true**|
|**Cache-Control**|要求/応答チェーンに沿うすべてのキャッシュ機構が従う必要があるディレクティブを指定するために使用されます。|
|**Pragma**|実装固有の動作。|
|**Expires**|クライアントがリソースを有効期限切れにする必要があるタイミング。|
|**X-Activity-Id**|サーバー生成のアクティビティ ID。|
|**OData-Version**|サポートされている OData のバージョン (4.0)。|
|**Date**|サーバーから応答が送信されたときの、UTC 形式の日付。|
|**X-Time-Taken**|応答の生成にかかった時間 (ミリ秒)。|
|**X-Instance-Name**|(デバッグ目的で) 応答の生成に使用される Azure インスタンスの ID。|
|**Server**|(デバッグ目的で) 応答を生成するために使用されるサーバー。|
|**X-ASPNET-Version**|(デバッグ目的で) 応答を生成したサーバーにより使用される ASP.Net のバージョン。|
|**X-Powered-By**|(デバッグ目的で) 応答を生成したサーバーで使用されるテクノロジ。|
|||

<br/>

以下に示すのは、Office 365 サービス通信 API の操作です。

## <a name="get-services"></a>Get Services

サブスクライブしているサービスのリストを返します。

|情報|サービス|説明|
|:-----|:-----|:-----|
|**パス**| `/Services`||
|**クエリ オプション**|$select|プロパティのサブセットを選択します。|
|**応答**|"Service" エンティティのリスト|"Service" エンティティには、"Id" (文字列)、"DisplayName" (文字列)、および "FeatureNames" (文字列のリスト) が含まれています。|
||||

### <a name="sample-request"></a>要求のサンプル

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

### <a name="sample-response"></a>応答のサンプル

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

## <a name="get-current-status"></a>現在の状態の取得

過去 24 時間からのサービスの状態を返します。

> [!NOTE] 
> サービスの応答には、過去 24 時間以内の状態とインシデントが含まれます。 StatusDate または StatusTime の値は、過去 24 時間の値が返されます。 特定のインシデントの最後の更新を取得するには、メッセージの取得機能を使用して、インシデント ID と一致する応答レコードから LastUpdatedTime 値を読み取ります。 <br/>

<br/>

|情報|サービス|説明|
|:-----|:-----|:-----|
|**パス**| `/CurrentStatus`||
|**フィルター**|ワークロード|ワークロードでフィルター (文字列、既定値: all)。|
|**クエリ オプション**|$select|プロパティのサブセットを選択します。|
|**応答**|"WorkloadStatus" エンティティのリスト。|"WorkloadStatus" エンティティには、"Id" (文字列)、"Workload" (文字列)、"StatusTime"(DateTimeOffset)、"WorkloadDisplayName" (文字列)、"Status" (文字列)、"IncidentIds" (文字列のリスト)、FeatureGroupStatusCollection ("FeatureStatus" のリスト) が含まれます。<br/><br/>"FeatureStatus" エンティティには、"Feature" (文字列)、"FeatureGroupDisplayName" (文字列)、"FeatureStatus" (文字列) が含まれます。|
||||

### <a name="sample-request"></a>要求のサンプル

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>応答のサンプル

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

### <a name="status-definitions"></a>状態の定義

状態の定義には次の値が含まれます。

- Investigating
- ServiceDegradation
- ServiceInterruption
- RestoringService
- ExtendedRecovery
- InvestigationSuspended
- ServiceRestored
- FalsePositive
- PostIncidentReportPublished
- ServiceOperational

これらの状態の定義の説明については、「[Microsoft 365 サービスの正常性をチェックする方法](/enterprise/view-service-health#status-definitions)」を参照してください。

## <a name="get-historical-status"></a>Get Historical Status

特定の時間範囲内のサービスの履歴状態を、日単位で返します。

|情報|サービス|説明|
|:-----|:-----|:-----|
|**パス**| `/HistoricalStatus`||
|**Filters**|ワークロード|ワークロードでフィルター (文字列、既定値: all)。|
||StatusTime|StatusTime より後の日付でフィルター処理します (DateTimeOffset、既定値: ge CurrentTime - 7 日)。|
|**クエリ オプション**|$select|プロパティのサブセットを選択します。|
|**応答**|"WorkloadStatus" エンティティのリスト。|"WorkloadStatus" エンティティには、"Id" (文字列)、"Workload" (文字列)、"StatusTime"(DateTimeOffset)、"WorkloadDisplayName" (文字列)、"Status" (文字列)、"IncidentIds" (文字列のリスト)、FeatureGroupStatusCollection ("FeatureStatus" のリスト) が含まれます。<br/><br/>"FeatureStatus" エンティティには、"Feature" (文字列)、"FeatureGroupDisplayName" (文字列)、"FeatureStatus" (文字列) が含まれます。|
||||

### <a name="sample-request"></a>要求のサンプル

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>応答のサンプル

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

## <a name="get-messages"></a>Get Messages

特定の時間範囲内のサービスに関するメッセージを返します。"サービス インシデント"、"計画済みメンテナンス"、または "メッセージ センター" メッセージをフィルター処理するためのタイプ フィルターを使用します。

|情報|サービス|説明|
|:-----|:-----|:-----|
|**パス**| `/Messages`||
|**Filters**|ワークロード|ワークロードでフィルター (文字列、既定値: all)。|
||StartTime|開始時刻でフィルター処理します (DateTimeOffset、既定値: ge CurrentTime - 7 日)。|
||EndTime|終了時刻でフィルター処理します (DateTimeOffset、既定値: le CurrentTime)。|
||MessageType|メッセージの種類でフィルター処理します (文字列、既定値: all)。|
||ID|ID でフィルター処理します (文字列、既定値: all)。|
|**クエリ オプション**|$select|プロパティのサブセットを選択します。|
||$top|結果の最上位数を選択します (既定値および最大値 $top = 100)。|
||$skip|結果の数をスキップします (既定値: $skip = 0)。|
|**応答**|"Message" エンティティのリスト。|"Message" エンティティには、"Id" (文字列)、"StartTime" (DateTimeOffset)、"EndTime" (DateTimeOffset)、"Status" (文字列)、"Messages" ("MessageHistory" エンティティのリスト)、"LastUpdatedTime" (DateTimeOffset)、"Workload" (文字列)、"WorkloadDisplayName" (文字列)、"Feature" (文字列)、"FeatureDisplayName" (文字列)、"MessageType" (列挙、既定: all) が含まれます。<br/><br/>"MessageHistory" エンティティには、"PublishedTime" (DateTimeOffset)、"MessageText" (文字列) が含まれます。|
||||

### <a name="sample-request"></a>要求のサンプル

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>応答のサンプル

```json
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

## <a name="errors"></a>エラー

サービスでエラーが検出されると、標準の HTTP エラー コードの構文を使用して、エラー応答コードが呼び出し元に報告されます。[OData V4 仕様](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html)に従って、失敗した呼び出しの本体には、追加情報が単一の JSON オブジェクトとして含められます。完全な JSON エラー本体の例を以下に示します。


```json
{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}
```
