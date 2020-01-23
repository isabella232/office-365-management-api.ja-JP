---
ms.TocTitle: Office 365 Management APIs overview
title: Office 365 管理 API の概要
description: Office 365 のお客様およびパートナーの、サービス通信、セキュリティ、コンプライアンス、レポート作成、監査を含むすべての管理タスクに対応する、単一の機能拡張プラットフォームを提供します。
ms.ContentId: 4fca85f9-efa6-3b4b-b10d-a07cb31f803f
ms.topic: reference (API)
ms.date: 09/28/2016
localization_priority: Priority
ms.openlocfilehash: 88b7e590d769699ed186d7cecaf80e162d79a095
ms.sourcegitcommit: 36d0167805d24bbb3e2cf1a02d0f011270cc31cb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2020
ms.locfileid: "41263283"
---
# <a name="office-365-management-apis-overview"></a><span data-ttu-id="52499-103">Office 365 管理 API の概要</span><span class="sxs-lookup"><span data-stu-id="52499-103">Office 365 Management APIs overview</span></span>

<span data-ttu-id="52499-104">Office 365 管理 API は、Office 365 のお客様およびパートナーの、サービス通信、セキュリティ、コンプライアンス、レポート作成、監査を含むすべての管理タスクに対応する、単一の機能拡張プラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="52499-104">The Office 365 Management APIs provide a single extensibility platform for all Office 365 customers' and partners' management tasks, including service communications, security, compliance, reporting, and auditing.</span></span> <span data-ttu-id="52499-105">すべての Office 365 管理 API は、設計および実装において Office 365 REST API の現行スイートと一貫性があり、OAuth v2、OData v4、JSON などの一般的な業界標準アプローチを使用しています。</span><span class="sxs-lookup"><span data-stu-id="52499-105">All of the Office 365 Management APIs are consistent in design and implementation with the current suite of Office 365 REST APIs, using common industry-standard approaches, including OAuth v2, OData v4, and JSON.</span></span> <span data-ttu-id="52499-106">他の Office 365 API と同様、アプリケーションは Azure Active Directory で登録され、開発者はアプリの認証と承認を一貫した方法で受けることができます。</span><span class="sxs-lookup"><span data-stu-id="52499-106">Like the other Office 365 APIs, applications are registered in Azure Active Directory, giving developers a consistent way to authenticate and authorize their apps.</span></span>

<span data-ttu-id="52499-107">Office 365 管理 API についての質問がある場合は、質問を [Stack Overflow](http://stackoverflow.com/tags/office365) に、[office365] タグを使用して投稿します。</span><span class="sxs-lookup"><span data-stu-id="52499-107">If you have questions about the Office 365 Management APIs, post your question on [Stack Overflow](http://stackoverflow.com/tags/office365), using the [office365] tag.</span></span>

## <a name="office-365-service-communications-api-preview"></a><span data-ttu-id="52499-108">Office 365 サービス通信 API (プレビュー)</span><span class="sxs-lookup"><span data-stu-id="52499-108">Office 365 Service Communications API (preview)</span></span>

<span data-ttu-id="52499-109">Office 365 サービス通信 API は、プレビュー モードでリリースされています。</span><span class="sxs-lookup"><span data-stu-id="52499-109">The Office 365 Service Communications API has been released in preview mode.</span></span> <span data-ttu-id="52499-110">これは Office 365 サービス通信 API に置き換わるものであり、テナント管理者およびパートナーにサービス正常性の情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="52499-110">It replaces the Office 365 Service Communications API to provide service health information to tenant administrators and partners.</span></span> <span data-ttu-id="52499-111">以前のバージョンとは異なり、新しいサービス通信 API では、URL の名前付け、データ形式、認証などが一貫した方式で構築された REST API によって、まとまりのあるプラットフォームの操作性が提供されます。</span><span class="sxs-lookup"><span data-stu-id="52499-111">Unlike the previous version, the new Service Communications API delivers a cohesive platform experience, with REST APIs built in a consistent fashion including URL naming, data format, and authentication.</span></span>

<span data-ttu-id="52499-112">新機能は、新しいバージョンの API にのみ追加されます。旧バージョンをご使用のお客様は、早期の導入をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="52499-112">New features are only added to the new version of the API, encouraging early adoption by legacy customers.</span></span> <span data-ttu-id="52499-113">Office 365 サービス通信 API の通常の製品発表が行われると、サービス通信 API の旧バージョンの廃止に向けた期間が開始されます。</span><span class="sxs-lookup"><span data-stu-id="52499-113">When the General Announcement of Office 365 Service Communications API was made, the older version of the Service Communications API began a period of deprecation.</span></span> 

<span data-ttu-id="52499-114">操作のリファレンスについては、「[Office 365 サービス通信 API リファレンス (プレビュー)](office-365-service-communications-api-reference.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="52499-114">For the operations reference, see [Office 365 Service Communications API reference (preview)](office-365-service-communications-api-reference.md).</span></span>


## <a name="office-365-management-activity-api"></a><span data-ttu-id="52499-115">Office 365 管理アクティビティ API</span><span class="sxs-lookup"><span data-stu-id="52499-115">Office 365 Management Activity API</span></span>

<span data-ttu-id="52499-116">Office 365 管理アクティビティ API は、Office 365 と Azure Active Directory のアクティビティ ログからの、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="52499-116">The Office 365 Management Activity API provides information about various user, admin, system, and policy actions and events from Office 365 and Azure Active Directory activity logs.</span></span> <span data-ttu-id="52499-117">お客様とパートナーは、この情報を使用して、操作、セキュリティ、およびコンプライアンス監視の新しい企業向けソリューションを作成したり、既存のソリューションを拡張したりできます。</span><span class="sxs-lookup"><span data-stu-id="52499-117">Customers and partners can use this information to create new or enhance existing operations, security, and compliance-monitoring solutions for the enterprise.</span></span> 

<span data-ttu-id="52499-118">操作のリファレンスについては、「[Office 365 管理アクティビティ API リファレンス](office-365-management-activity-api-reference.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="52499-118">For the operations reference, see [Office 365 Management Activity API reference](office-365-management-activity-api-reference.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="52499-119">関連項目</span><span class="sxs-lookup"><span data-stu-id="52499-119">See also</span></span>

- [<span data-ttu-id="52499-120">Office 365 管理 API の使用を開始する</span><span class="sxs-lookup"><span data-stu-id="52499-120">Get started with Office 365 Management APIs</span></span>](get-started-with-office-365-management-apis.md)
- [<span data-ttu-id="52499-121">Office 365 管理アクティビティ API のスキーマ</span><span class="sxs-lookup"><span data-stu-id="52499-121">Office 365 Management Activity API schema</span></span>](office-365-management-activity-api-schema.md)
- [<span data-ttu-id="52499-122">Office 365 管理アクティビティ API のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="52499-122">Troubleshooting the Office 365 Management Activity API</span></span>](troubleshooting-the-office-365-management-activity-api.md)
- [<span data-ttu-id="52499-123">Office 365 REST API</span><span class="sxs-lookup"><span data-stu-id="52499-123">Office 365 REST APIs</span></span>](https://docs.microsoft.com/previous-versions/office/office-365-api/how-to/platform-development-overview)

