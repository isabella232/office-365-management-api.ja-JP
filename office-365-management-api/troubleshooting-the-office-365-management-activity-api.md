---
ms.technology: o365-service-communications
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Office 365 マネージメント アクティビティ API のトラブルシューティング
description: この API のサポートについて Microsoft サポートに最も多く寄せられる質問のまとめです。
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 323407799cefe74b331dec01bb746971c41b5adf
ms.sourcegitcommit: ec60dbd5990cfc61b8c000b423e7ade25fa613a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397434"
---
# <a name="office-365-management-activity-api-faqs-and-troubleshooting"></a><span data-ttu-id="4bf0c-103">Office 365 マネージメント アクティビティ API の FAQ とトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="4bf0c-103">Office 365 Management Activity API FAQs and troubleshooting</span></span>

<span data-ttu-id="4bf0c-104">Office 365 マネージメント アクティビティ API （*統合監査 API* とも呼ばれます） は、Office 365 のセキュリティおよびコンプライアンス製品の一部です:</span><span class="sxs-lookup"><span data-stu-id="4bf0c-104">The Office 365 Management Activity API (also known as the *Unified Auditing API*) is a part of Office 365 security and compliance offerings, that:</span></span>

- <span data-ttu-id="4bf0c-105">複数の監査パイプライン ワークロード (SharePoint や Exchange など) にプログラムでアクセスできます</span><span class="sxs-lookup"><span data-stu-id="4bf0c-105">Allows programmatic access to multiple auditing pipeline workloads (such as SharePoint and Exchange)</span></span>

- <span data-ttu-id="4bf0c-106">監査データの集計およびインデックス作成のために、広範なサード パーティ ベンダーによって使用されるメイン インターフェイスです</span><span class="sxs-lookup"><span data-stu-id="4bf0c-106">Is the main interface used by a variety of third-party vendor products to aggregate and index auditing data</span></span>

<span data-ttu-id="4bf0c-107">マネージメント アクティビティ API を Office 365 サービス コミュニケーション API と混同しないでください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-107">The Management Activity API shouldn't be confused with the Office 365 Service Communications API.</span></span> <span data-ttu-id="4bf0c-108">マネージメント アクティビティ API は、各種のワークローでのエンド ユーザーのアクティビティを監査するためのものです。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-108">The Management Activity API is for auditing end user activities in the various workloads.</span></span> <span data-ttu-id="4bf0c-109">サービス コミュニケーション API は、Office 365 で利用可能なサービス (Dynamics CRM や ID サービスなど) によって送信される状態やメッセージを監査するためのものです。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-109">The Service Communications API is for auditing status and messages that are sent by the services that are available in Office 365 (such as Dynamics CRM or Identity Service).</span></span>

## <a name="frequently-asked-questions-about-the-office-365-management-activity-api"></a><span data-ttu-id="4bf0c-110">Office 365 マネージメント アクティビティ API についてよく寄せられる質問</span><span class="sxs-lookup"><span data-stu-id="4bf0c-110">Frequently asked questions about the Office 365 Management Activity API</span></span>

<span data-ttu-id="4bf0c-111">**特定の Office 365 イベントに関する通知が送信されるまでに必要な最長の待ち時間はどれくらいですか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-111">**What is the maximum time I will have to wait before a notification is sent about a given Office 365 event?**</span></span>

<span data-ttu-id="4bf0c-112">通知の配信について最長の待機時間に対する保証はありません (つまり、SLA はありません)。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-112">There is no guaranteed maximum latency for notification delivery (in other words, no SLA).</span></span> <span data-ttu-id="4bf0c-113">Microsoft サポートの認識では、ほとんどの通知がイベントの発生から 1 時間以内に送信されます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-113">Microsoft Support's experience has been that most notifications are sent within one hour of the event.</span></span> <span data-ttu-id="4bf0c-114">この待機時間は大幅に短くなることも、長くなることもあります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-114">Often the latency is much shorter, but often it's longer as well.</span></span> <span data-ttu-id="4bf0c-115">ワークロードごとに多少の違いはありますが、原則的に、ほとんどの通知はイベントの発生から 24 時間以内に配信されます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-115">This varies somewhat from workload to workload, but a general rule is that most notifications will be delivered within 24 hours of the originating event.</span></span>

<span data-ttu-id="4bf0c-116">**Webhook 通知はもっと即時ではありませんか? 結局のところ、イベント駆動型ではありませんか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-116">**Aren't webhook notifications more immediate? After all, aren't they are event-driven?**</span></span>

<span data-ttu-id="4bf0c-117">いいえ。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-117">No.</span></span><span data-ttu-id="4bf0c-118">Webhook 通知は、イベントによって通知がトリガーされるという意味ではイベント駆動ではありません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-118"> Webhook notifications aren't event-driven in the sense that the event triggers the notification.</span></span> <span data-ttu-id="4bf0c-119">コンテンツ BLOB の作成は依然として必要であり、コンテンツ BLOB の作成が通知の配信をトリガーします。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-119">The content blob must still be created and creating the content blob is what triggers the notification delivery.</span></span> <span data-ttu-id="4bf0c-120">最近では、Webhook の使用時の通知の待機時間は、/content 操作で API を直接クエリするよりも長くなっています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-120">Recently, there have been longer wait times for notifications when using a webhook compared to querying the API directly with the /content operation.</span></span> <span data-ttu-id="4bf0c-121">そのため、マネージメント アクティビティ API は、リアルタイムのセキュリティ警告システムとして捉えることはできません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-121">Therefore, the Management Activity API shouldn't be thought of as a real-time security alert system.</span></span> <span data-ttu-id="4bf0c-122">Microsoft は、その目的のための別の製品を用意しています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-122">Microsoft has other products for that.</span></span> <span data-ttu-id="4bf0c-123">セキュリティに関する限り、マネージメント アクティビティ API のイベント通知は、長期間にわたる使用パターンを判断するために使用するほうが適しています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-123">As far as security is concerned, Management Activity API event notifications can more appropriately be used to determine use patterns over extended periods of time.</span></span>

<span data-ttu-id="4bf0c-124">**コンテンツ BLOB 内の特定のイベント ID や RecordType などのプロパティについてマネージメント アクティビティ API を照会できますか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-124">**Can I query the Management Activity API for a particular event ID or RecordType or other properties in the content blob?**</span></span>

<span data-ttu-id="4bf0c-125">いいえ。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-125">No.</span></span><span data-ttu-id="4bf0c-126">マネージメント アクティビティ API によって利用可能になるデータは、従来の意味での「ログ」と考えないでください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-126"> Don't think of the data available through the Management Activity API as being a “log” in the traditional sense.</span></span> <span data-ttu-id="4bf0c-127">それよりも、イベントの詳細についてのダンプと考えてください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-127">Rather, think of it as a dump of event details.</span></span> <span data-ttu-id="4bf0c-128">カスタムのアプリケーションやサード パーティ製のツールを使用して、これらのイベントの詳細をすべて収集し、ローカルに保存してインデックスを作成し、独自のクエリ ロジックを実装することは、ユーザーの裁量に任されています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-128">It's up to you to gather all those event details, store and index them locally, and then implement your own query logic, by using either a custom application or a third-party tool.</span></span>

<span data-ttu-id="4bf0c-129">**マネージメント アクティビティ API からデータを収集する既存の監査アプリケーションのデータが正確で完全であることを確認する方法はありますか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-129">**How do I know the data coming from my existing auditing solution, which collects data from the Management Activity API, is accurate and complete?**</span></span>

<span data-ttu-id="4bf0c-130">簡潔に答えると、Microsoft は特定のアプリケーションやサード パーティ (ISV) のアプリケーションをクロスチェックできるようなログは提供していません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-130">The short answer is that Microsoft doesn't provide any kind of a log that will allow you to cross-check any given application or third-party (ISV) application.</span></span> <span data-ttu-id="4bf0c-131">同じパイプラインからデータを取り出す Microsoft セキュリティ製品もありますが、そうした製品についての説明は、この記事の範囲外であり、マネージメント アクティビティ API を直接クロスチェックするために使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-131">There are other Microsoft security products that draw their data from the same pipeline, but those products fall outside the scope of this discussion and can't be used to directly cross-check the Management Activity API.</span></span> <span data-ttu-id="4bf0c-132">既存のソリューションが提供する内容と予測した内容の矛盾について懸念している場合は、前述の操作を実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-132">If you're concerned about discrepancies between what your existing solution is providing and what you expect, you should implement the operations illustrated above.</span></span> <span data-ttu-id="4bf0c-133">ただし、既存のツールやソリューションがデータをリストする方法とデータにインデックスを作成する方法によっては、これは困難なことになります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-133">But this can be difficult, depending on how your existing tool or solution lists and indexes data.</span></span> <span data-ttu-id="4bf0c-134">既存のソリューションが実際のイベントの作成時刻で並べ替えたデータを表示するだけならば、結果セットを比較できるようにイベントの作成時刻で API を照会する方法は存在しません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-134">If your existing solution only presents data sorted by the creation time of the actual event, there's no way to query the API by event creation time so that you could compare result sets.</span></span> <span data-ttu-id="4bf0c-135">このシナリオでは、通知されたコンテンツ BLOB を数日間にわたって収集し、手動でインデックスを作成するか並べ替えてから、大まかな比較を実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-135">In this scenario, you'd have to collect the notified content blobs for several days, index or sort them manually, and then do a rough comparison.</span></span>

<span data-ttu-id="4bf0c-136">**コンテンツ BLOB の利用可能期間はどれくらいですか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-136">**How long will the content blobs remain available?**</span></span>

<span data-ttu-id="4bf0c-137">コンテンツ BLOB は、コンテンツ BLOB が利用可能になったことが通知されてから 7 日間利用できます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-137">Content blobs are available 7 days after the notification of the content blob's availability.</span></span> <span data-ttu-id="4bf0c-138">そのため、コンテンツ BLOB の作成に大幅な遅延があった場合は、コンテンツ BLOB が利用できなくなるまで、実際のイベント作成日の後に、それよりも長い時間 (遅延 + 7 日) 利用可能になります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-138">This means that if there is a significant delay in the creation of the content blob, you will have more time (the delay plus 7 days) after the actual event creation date before the content blob is no longer available.</span></span>

<span data-ttu-id="4bf0c-139">**通知されるまでに 24 時間の遅延があった場合、コンテンツ BLOB を取得するための期間は 6 日間しかないことになりますか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-139">**If there is a 24-hour delay in getting a notification, doesn't that mean I will have only 6 days to retrieve the content blob?**</span></span>

<span data-ttu-id="4bf0c-140">いいえ。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-140">No.</span></span><span data-ttu-id="4bf0c-141">通知が非常に長い期間遅延した場合でも (サービスの中断などの場合)、元のイベントに関連するコンテンツ BLOB をダウンロードする通知が最初に利用可能になってから 7 日間の期間があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-141"> Even if the notification is delayed for an unusually long period (for example, in the case of a service interruption), you would still have 7 days after the first availability of the notification to download the content blob related to the originating event.</span></span>

<span data-ttu-id="4bf0c-142">**特定の Office 365 サービスについて、どのイベントが監査されますか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-142">**What events are audited for a specific Office 365 service?**</span></span>

<span data-ttu-id="4bf0c-143">総合的なイベントの一覧は、Office 365 マネージメント アクティビティ API スキーマのドキュメントに記載されています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-143">Office 365 Management Activity API schema documentation has a comprehensive list of events.</span></span> <span data-ttu-id="4bf0c-144">詳細については、「Office 365 マネージメント アクティビティ API のスキーマ」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-144">For details, see Office 365 Management Activity API schema.</span></span> <span data-ttu-id="4bf0c-145">監査対象のほとんどの Office 365 サービスのイベントのリストについては、セキュリティ/コンプライアンス センターの監査ログの検索の「監査済みアクティビティ」セクションも参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-145">Also see the “Audited activities” section in Search the audit log in the Security & Compliance Center for a list of events for most of the Office 365 services that are audited.</span></span>

<span data-ttu-id="4bf0c-146">**どのようにすればマネージメント アクティビティ API の使用を開始できますか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-146">**How do I onboard to the Management Activity API?**</span></span>

<span data-ttu-id="4bf0c-147">Office 365 マネージメント アクティビティ API の使用を開始する方法については、「Office 365 管理 API の使用を開始する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-147">To get started with the Office 365 Management Activity API, see Get started with Office 365 Management APIs.</span></span>

<span data-ttu-id="4bf0c-148">**すべてのワークロードのすべてのイベントをプログラムで取得しようと考えています。これを行うための最も信頼できる方法は何ですか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-148">**We want to programmatically capture all events in all workloads. What is the most reliable way to do this?**</span></span>

<span data-ttu-id="4bf0c-149">Office 365 マネージメント アクティビティ API を使用することで実現できます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-149">You can do this by using the Office 365 Management Activity API.</span></span> <span data-ttu-id="4bf0c-150">また、webhook の使用には問題があるため、**プル モデル**を使用することもお勧めします。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-150">Also, we recommend that you use the **pull model** due to issues with using webhooks.</span></span> <span data-ttu-id="4bf0c-151">詳細については、「Office 365 マネージメント アクティビティ API のトラブルシューティング」の「Webhook の使用」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-151">For more information, see the “Using webhooks” section in Troubleshooting the Office 365 Management Activity API.</span></span>

<span data-ttu-id="4bf0c-152">**マネージメント アクティビティ API でフェッチされたレコードと、Microsoft 365 コンプライアンス センターの監査ログの検索ツールを使用して返されたレコードに違いはありますか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-152">**Are there any differences in the records that are fetched by the Management Activity API versus the records that are returned by using the audit log search tool in the Microsoft 365 compliance center?**</span></span>

<span data-ttu-id="4bf0c-153">どちらの方法でも、同じデータが返されます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-153">The data that is returned by both methods is the same.</span></span> <span data-ttu-id="4bf0c-154">フィルター処理は行われません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-154">There is no filtering that happens.</span></span> <span data-ttu-id="4bf0c-155">唯一の相違点は、API では一度に取得できるデータが過去 7 日間のものであるということです。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-155">The only difference is that with the API, you can get data for the last 7 days at a time.</span></span> <span data-ttu-id="4bf0c-156">セキュリティ/コンプライアンス センターでの監査ログの検査 (または、それに相当する Exchange Online での Search-UnifiedAuditLog コマンドレットの使用) では、過去 90 日間のデータを取得できます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-156">When searching the audit log in the Security & Compliance Center (or by using the corresponding Search-UnifiedAuditLog cmdlet in Exchange Online), you can get data for the last 90 days.</span></span>

<span data-ttu-id="4bf0c-157">**Office 365 組織の監査を無効にするとどうなりますか? マネージメント アクティビティ API を介してイベントを引き続き取得できますか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-157">**What happens if I disable auditing for my Office 365 organization? Will I still get events via the Management Activity API?**</span></span>

<span data-ttu-id="4bf0c-158">いいえ。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-158">No.</span></span><span data-ttu-id="4bf0c-159">管理アクティビティ API を介してレコードを取得するには、組織の Office 365 統合監査を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-159"> Office 365 unified auditing must be enabled for your organization to pull records via the Management Activity API.</span></span> <span data-ttu-id="4bf0c-160">手順については、「Office 365 監査ログの検索を有効または無効にする」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-160">For instructions, see Turn Office 365 audit log search on or off.</span></span>

<span data-ttu-id="4bf0c-161">**マネージメント アクティビティ API の調整制限とは何ですか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-161">**What is the throttling limit for the Management Activity API?**</span></span>

<span data-ttu-id="4bf0c-162">すべての組織には、最初に 1 分あたり 2,000 件の要求のベースラインが割り当てられます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-162">All organizations are initially allocated a baseline of 2,000 requests per minute.</span></span> <span data-ttu-id="4bf0c-163">これは静的な定義済みの制限ではありませんが、組織内のシート数や、Office 365 E5 および Microsoft 365 E5 組織が非 E5 組織の約 2 倍の帯域幅を取得するという事実などの要因の組み合わせでモデル化されています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-163">This is not a static, predefined limit but is modeled on a combination of factors including the number of seats in the organization and the fact that Office 365 E5 and Microsoft 365 E5 organizations will get approximately twice as much bandwidth as non-E5 organizations.</span></span> <span data-ttu-id="4bf0c-164">また、サービスの正常性を保護するために、最大帯域幅の上限も設定されます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-164">There will also be cap on the maximum bandwidth to protect the health of the service.</span></span>

> [!NOTE]
> <span data-ttu-id="4bf0c-165">それぞれのテナントは最初に最大 1 分あたり 2,000 の要求を送信できますが、Microsoft は応答速度を保証できません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-165">Even though each tenant can initially submit up to 2,000 requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="4bf0c-166">応答速度は、クライアント システムのパフォーマンス、ネットワーク容量、ネットワーク速度など、さまざまな要因によって決まります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-166">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span>

<span data-ttu-id="4bf0c-167">**マネージメント アクティビティ API で調整エラーが発生しました。何をすべきですか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-167">**I'm encountering a throttling error in the Management Activity API. What should I do?**</span></span>

<span data-ttu-id="4bf0c-168">Microsoft サポートでチケットを開いて、新しい調整制限を要求してください。また、制限の引き上げに対する業務上の正当な理由を含めてください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-168">Open a ticket with Microsoft Support and request a new throttling limit, and include a business justification for increasing the limit.</span></span> <span data-ttu-id="4bf0c-169">要求を審査し承諾されると、調整制限が引き上げられます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-169">We will evaluate the request, and if accepted, we will increase the throttling limit.</span></span>

<span data-ttu-id="4bf0c-170">**Azure Active Directory アクティビティの監査ログで TargetUpdatedProperties が ExtendedProperties に含まれなくなったのはなぜですか?**</span><span class="sxs-lookup"><span data-stu-id="4bf0c-170">**Why are TargetUpdatedProperties no longer in ExtendedProperties in the audit logs for Azure Active Directory activities?**</span></span>

<span data-ttu-id="4bf0c-171">TargetUpdatedProperties は ExtendedProperties に表示されていました。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-171">TargetUpdatedProperties were appearing in ExtendedProperties.</span></span> <span data-ttu-id="4bf0c-172">これが ExtendedProperties から削除され、現在では ModifiedProperties に表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-172">However, they have been removed from ExtendedProperties and now appear in ModifiedProperties.</span></span>

## <a name="troubleshooting-the-office-365-management-activity-api"></a><span data-ttu-id="4bf0c-173">Office 365 マネージメント アクティビティ API のトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="4bf0c-173">Troubleshooting the Office 365 Management Activity API</span></span>

<span data-ttu-id="4bf0c-174">Office 365 マネージメント アクティビティ API の入門者が明確にしておく必要のあることの 1 つは、イベントが発生した日付、イベントの発生元になる可能性のあるサイト コレクション、イベントの種類などのイベントの詳細によってクエリを実行するという概念がないことです。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-174">One thing that should be made clear for anyone who's getting started with the Office 365 Management Activity API is that there is no concept of querying by event specifics, such as date that the event occurred, which site collection an event might have been fired from, or the type of event.</span></span> <span data-ttu-id="4bf0c-175">その代りに、特定のワークロード (SharePoint や Azure AD など) に対するサブスクリプションを作成します。また、それぞれのサブスクリプションはテナント単位にします。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-175">Instead, you create subscriptions to specific workloads (for example, SharePoint or Azure AD) and each subscription is per tenant.</span></span>

<span data-ttu-id="4bf0c-176">以下のセクションでは、Office 365 マネージメント アクティビティ API を使用する際にお客様が抱く最も一般的な質問をまとめています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-176">The following sections summarizes the most common questions that customers have in using the Office 365 Management Activity API:</span></span>

- [<span data-ttu-id="4bf0c-177">サード パーティ製のツールとクライアントに関する質問</span><span class="sxs-lookup"><span data-stu-id="4bf0c-177">Questions about third-party tools and clients</span></span>](#questions-about-third-party-tools-and-clients)

- [<span data-ttu-id="4bf0c-178">Office 365 で統合監査ログを有効にする</span><span class="sxs-lookup"><span data-stu-id="4bf0c-178">Enabling unified audit logging in Office 365</span></span>](#enabling-unified-audit-logging-in-office-365)

- [<span data-ttu-id="4bf0c-179">API への接続</span><span class="sxs-lookup"><span data-stu-id="4bf0c-179">Connecting to the API</span></span>](#connecting-to-the-api)

- [<span data-ttu-id="4bf0c-180">サブスクリプションの確認</span><span class="sxs-lookup"><span data-stu-id="4bf0c-180">Checking your subscriptions</span></span>](#checking-your-subscriptions)

- [<span data-ttu-id="4bf0c-181">新しいサブスクリプションの作成</span><span class="sxs-lookup"><span data-stu-id="4bf0c-181">Creating a new subscription</span></span>](#creating-a-new-subscription)

- [<span data-ttu-id="4bf0c-182">Webhook の使用</span><span class="sxs-lookup"><span data-stu-id="4bf0c-182">Using webhooks</span></span>](#using-webhooks)

- [<span data-ttu-id="4bf0c-183">コンテンツ BLOB の要求と調整</span><span class="sxs-lookup"><span data-stu-id="4bf0c-183">Requesting content blobs and throttling</span></span>](#requesting-content-blobs-and-throttling)

<span data-ttu-id="4bf0c-184">ここでは、選りすぐりのシンプルな PowerShell スクリプトを示します。これらのスクリプトにより、ユーザーから最も多く寄せられる質問への回答を示すことができます。また、主な操作の用例が示されているためカスタム ソリューションの実装を開始する際に役立てることもできます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-184">We'll show a selection of simple PowerShell scripts that can help you answer the most common questions asked by customers or get you started implementing a custom solution by demonstrating the main operations.</span></span> <span data-ttu-id="4bf0c-185">これらのセクションでは説明されていない操作もありますが、「Office 365 マネージメント アクティビティ API リファレンス」には、すべての操作が示されています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-185">Not all the operations are explained in these sections, but they are all listed in Office 365 Management Activity API reference.</span></span>

### <a name="questions-about-third-party-tools-and-clients"></a><span data-ttu-id="4bf0c-186">サード パーティ製のツールとクライアントに関する質問</span><span class="sxs-lookup"><span data-stu-id="4bf0c-186">Questions about third-party tools and clients</span></span>

<span data-ttu-id="4bf0c-187">最も一般的な質問のカテゴリは、監査データのダウンロードおよび集計にサード パーティ製の製品を使用しているユーザーからのものです。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-187">The most common category of questions come from customers using third-party products to download and aggregate auditing data.</span></span> <span data-ttu-id="4bf0c-188">サード パーティ製の製品によっては、セットアップで問題が発生することや、該当する製品で公開されるデータに中断や矛盾が発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-188">Depending on the third-party product, customers may encounter difficulty with the setup or experience an interruption or an inconsistency in the data exposed in those products.</span></span> <span data-ttu-id="4bf0c-189">そのような場合は、まず、ベンダーのサポート組織に問い合せてください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-189">Here it should be stated that the first action such customers should take is to contact their vendor's support organization.</span></span> <span data-ttu-id="4bf0c-190">通常、テナント固有のベンダー構成またはサービスの問題が、お客様の不満の原因です。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-190">Typically, a tenant-specific vendor configuration or service problem is the cause of customer complaints.</span></span>

### <a name="enabling-unified-audit-logging-in-office-365"></a><span data-ttu-id="4bf0c-191">Office 365 で統合監査ログを有効にする</span><span class="sxs-lookup"><span data-stu-id="4bf0c-191">Enabling unified audit logging in Office 365</span></span>

<span data-ttu-id="4bf0c-192">管理アクティビティ API を使用するためにアプリをセットアップしたのに、それが動作しない場合は、Office 365 組織の統合監査ログが有効になっていることをご確認ください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-192">If you've just set up an app that's trying to use the Management Activity API and it's not working, be sure that you've enabled unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="4bf0c-193">これを実行するには、Office 365 監査ログをオンにします。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-193">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="4bf0c-194">手順については、「[Office 365 監査ログの検索を有効または無効にする](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-194">For instructions, see [Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span></span>

<span data-ttu-id="4bf0c-195">統合監査が有効になっていない場合は、通常、次の文字列を含むエラーが表示されます。`Microsoft.Office.Compliance.Audit``.DataServiceException: Tenant <tenantID> does not exist.`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-195">If unified auditing isn't enabled, you will typically receive an error that contains the following string: `Microsoft.Office.Compliance.Audit``.DataServiceException: Tenant <tenantID> does not exist.`</span></span>

### <a name="connecting-to-the-api"></a><span data-ttu-id="4bf0c-196">API への接続</span><span class="sxs-lookup"><span data-stu-id="4bf0c-196">Connecting to the API</span></span>

<span data-ttu-id="4bf0c-197">ほとんどのアプリケーションは、簡単なクライアント資格情報の OAuth2 フローを使用して API に接続します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-197">Most applications connect to the API using a straightforward Client Credentials OAuth2 flow.</span></span> <span data-ttu-id="4bf0c-198">そのため、最初の手順では、マネージメント アクティビティ API のデータへのアクセスに必要なアクセス許可を持つ Azure AD アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-198">Therefore, the first step is to create an Azure AD application that has the permissions needed to access the Management Activity API data.</span></span> <span data-ttu-id="4bf0c-199">Azure AD アプリの登録を作成する手順に関する説明は、この記事の範囲外になります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-199">It's outside the scope of this article to explain the steps to create an Azure AD App registration.</span></span> <span data-ttu-id="4bf0c-200">詳細については、「[クイック スタート: Azure Active Directory v1.0 エンドポイントを使用してアプリを登録する](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-200">For more information, see [Register your application with your Azure Active Directory tenant](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).</span></span>

#### <a name="azure-application-permissions"></a><span data-ttu-id="4bf0c-201">Azure アプリケーションのアクセス許可</span><span class="sxs-lookup"><span data-stu-id="4bf0c-201">Azure application permissions</span></span>

<span data-ttu-id="4bf0c-202">現在、Office 365 マネージメント アクティビティ API に使用されている 3 つのアクセス許可は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-202">The three permissions currently used for the Office 365 Management Activity API are:</span></span>

1. <span data-ttu-id="4bf0c-203">組織のアクティビティ データの読み取り</span><span class="sxs-lookup"><span data-stu-id="4bf0c-203">Read activity data for your organization</span></span>

2. <span data-ttu-id="4bf0c-204">組織のサービス正常性情報の読み取り</span><span class="sxs-lookup"><span data-stu-id="4bf0c-204">Read service health information for your organization</span></span>

3. <span data-ttu-id="4bf0c-205">データ損失防止 (DLP) ポリシー イベントの読み取り (機密情報の検出を含む)</span><span class="sxs-lookup"><span data-stu-id="4bf0c-205">Read Data Loss Prevention (DLP) policy events, including detected sensitive information</span></span>

> [!NOTE]
> <span data-ttu-id="4bf0c-206">上記のアクセス許可セットの少なくとも最初の 2 つには、「アプリケーションのアクセス許可」と「デリゲートされたアクセス許可」の両方を有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-206">You should enable both the Application Permissions and the Delegated Permissions for at least the first two of the above permission sets.</span></span> <span data-ttu-id="4bf0c-207">DLP ポリシー イベントの読み取りは、DLP ワークロードに注目する場合にのみ必要になります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-207">Read DLP policy events will only be necessary if you are interested in the DLP workloads.</span></span>

#### <a name="getting-an-access-token"></a><span data-ttu-id="4bf0c-208">アクセス トークンの取得</span><span class="sxs-lookup"><span data-stu-id="4bf0c-208">Getting an access token</span></span>

<span data-ttu-id="4bf0c-209">次に示す PowerShell スクリプトでは、アプリ ID とクライアント シークレットを使用して、マネージメント アクティビティ API 認証エンドポイントから OAuth2 トークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-209">The following PowerShell script uses the App ID and a Client Secret to obtain the OAuth2 token from the Management Activity API authentication endpoint.</span></span> <span data-ttu-id="4bf0c-210">その後で、HTTP 要求に添付する `$headerParams` 配列変数にアクセス トークンを格納します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-210">It then places the access token into the `$headerParams` array variable, which you'll attach to your HTTP request.</span></span> <span data-ttu-id="4bf0c-211">API エンドポイントの値 ($resource 変数内) には、組織の Microsoft 365 または Office 365 サブスクリプション プランに基づいて、次の値のいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-211">For the value for the API endpoint (in the $resource variable) use one of the following values based on your organization's Microsoft 365 or Office 365 subscription plan:</span></span>

- <span data-ttu-id="4bf0c-212">Enterprise プラン: `manage.office.com`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-212">Enterprise plan: `manage.office.com`</span></span>

- <span data-ttu-id="4bf0c-213">GCC 政府機関向けプラン: `manage-gcc.office.com`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-213">GCC government plan: `manage-gcc.office.com`</span></span>

- <span data-ttu-id="4bf0c-214">GCC High 政府機関向けプラン: `manage.office365.us`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-214">GCC High government plan: `manage.office365.us`</span></span>

- <span data-ttu-id="4bf0c-215">DoD 政府機関向けプラン: `manage.protection.apps.mil`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-215">DoD government plan: `manage.protection.apps.mil`</span></span>

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

<span data-ttu-id="4bf0c-216">`$oauth` 変数には、応答オブジェクトを格納します。このオブジェクトには、アクセス トークンなど複数のプロパティが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-216">The `$oauth` variable will contain the response object, which has several properties including the access token.</span></span> <span data-ttu-id="4bf0c-217">次に、応答例を示します:</span><span class="sxs-lookup"><span data-stu-id="4bf0c-217">Here's an example of a response:</span></span>

```json
token_type     : Bearer
expires_in     : 3599
ext_expires_in : 0
expires_on     : 1508285860
not_before     : 1508281960
resource       : https://manage.office.com
access_token   : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyIsImtpZCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyJ9.eyJhdWQiOiJodHRwczov…
```

### <a name="checking-your-subscriptions"></a><span data-ttu-id="4bf0c-218">サブスクリプションの確認</span><span class="sxs-lookup"><span data-stu-id="4bf0c-218">Checking your subscriptions</span></span>

<span data-ttu-id="4bf0c-219">既存のマネージメント アクティビティ API クライアントまたはソリューションへのデータ フローに中断が発生したときには、サブスクリプションに何らかの問題が発生しているのではないかと疑われることがあります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-219">If you've experienced an interruption in data flowing to an existing Management Activity API client or solution, you might wonder if something happened to your subscription.</span></span> <span data-ttu-id="4bf0c-220">アクティブなサブスクリプションを確認するために、前述のスクリプトに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-220">To check your active subscriptions, add the following to the previous script:</span></span>

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
```

#### <a name="sample-response"></a><span data-ttu-id="4bf0c-221">応答例</span><span class="sxs-lookup"><span data-stu-id="4bf0c-221">Sample response</span></span>

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

<span data-ttu-id="4bf0c-222">これは、Audit.Exchange と Audit.SharePoint のサブスクリプションがテナントで有効になっていることを示しています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-222">This says that the tenant has both Audit.Exchange and Audit.SharePoint subscriptions enabled.</span></span> <span data-ttu-id="4bf0c-223">Exchange サブスクリプションには使用可能な Webhook がありません (null)。SharePoint サブスクリプションには使用可能な Webhook があります (登録されたエンドポイントのアドレスが示されています)。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-223">The Exchange subscription has no webhook enabled (null) and the SharePoint subscription has a webhook enabled with the address of the registered endpoint shown.</span></span>

### <a name="creating-a-new-subscription"></a><span data-ttu-id="4bf0c-224">新しいサブスクリプションの作成</span><span class="sxs-lookup"><span data-stu-id="4bf0c-224">Creating a new subscription</span></span>

<span data-ttu-id="4bf0c-225">新規サブスクリプションを作成するには、/start 操作を使用します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-225">To create a new subscription, you use the /start operation.</span></span> <span data-ttu-id="4bf0c-226">API エンドポイントには、サブスクリプション プランに基づいて、次の値のいずれかを使用します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-226">For the API endpoint, use one of these values base on your subscription plan:</span></span>

- <span data-ttu-id="4bf0c-227">Enterprise プラン: `manage.office.com`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-227">Enterprise plan: `manage.office.com`</span></span>

- <span data-ttu-id="4bf0c-228">GCC 政府機関向けプラン: `manage-gcc.office.com`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-228">GCC government plan: `manage-gcc.office.com`</span></span>

- <span data-ttu-id="4bf0c-229">GCC High 政府機関向けプラン: `manage.office365.us`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-229">GCC High government plan: `manage.office365.us`</span></span>

- <span data-ttu-id="4bf0c-230">DoD 政府機関向けプラン: `manage.protection.apps.mil`</span><span class="sxs-lookup"><span data-stu-id="4bf0c-230">DoD government plan: `manage.protection.apps.mil`</span></span>

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://<YOUR_API_ENDPOINT>/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"

> [!NOTE]
> Remember that `$headerParams` was populated in the first part of the script listed in the [Connecting to the API](#connecting-to-the-api) section in this article.

The previous code will create a new subscription to the Audit.AzureActiveDirectory content type, with a webhook that is null. You can then check your subscriptions using the code in the [Checking your subscriptions](#checking-your-subscriptions) section in this article.

## Checking content availability

To check what content blobs were created during a certain period, you can add the following line to the script in the “Connecting to the API” section.

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

<span data-ttu-id="4bf0c-231">上記の例では、本日 (午前 12 時 00 分 UTC から現在の時刻までに) 利用可能になったすべてのコンテンツの通知を取得しています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-231">The previous example will get all the content notifications that became available today, which means from 12:00 AM UTC to the current time.</span></span> <span data-ttu-id="4bf0c-232">別の期間を指定する場合は、URI に *starttime* パラメーターと *endtime* パラメーターを追加します (照会可能な最長の期間は 24 時間である点に注意してください)。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-232">If you want to specify a different time period (keeping in mind that the maximum period for which you can query is 24 hours), add the *starttime* and *endtime* parameters to the URI; for example:</span></span>

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE]
> <span data-ttu-id="4bf0c-233">*starttime* パラメーターと *endtime* パラメーターは、「両方とも使用する」または「両方とも使用しない」のどちらかにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-233">You must use either both *starttime* and *endtime* parameters or neither.</span></span>

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
> - <span data-ttu-id="4bf0c-234">*contentUri* プロパティは、コンテンツ BLOB を取得できる URI です。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-234">The *contentUri* property is the URI from which you can retrieve the content blob.</span></span> <span data-ttu-id="4bf0c-235">イベントの詳細は BLOB 自体に格納されていて、1 ～ N 件のイベントに関する詳細が格納されています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-235">The blob itself is what contains the event details; it will contain details about 1 – N events.</span></span> <span data-ttu-id="4bf0c-236">コレクションには 30 件の JSON オブジェクトが存在している可能性があり、それらの 30 件のコンテンツ URI には、さらに多くのイベントの詳細が存在している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-236">While there may be 30 JSON objects in the collection, there may be many more events detailed in those 30 content URIs.</span></span>
>
> - <span data-ttu-id="4bf0c-237">*contentCreated* プロパティは、通知されるイベントが作成された日付ではありません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-237">The *contentCreated* property is not the date that the event being notified was created.</span></span> <span data-ttu-id="4bf0c-238">通知が作成された日付です。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-238">This is the date the notification was created.</span></span> <span data-ttu-id="4bf0c-239">その BLOB で詳細が示されるイベントは、コンテンツ BLOB が作成されたときよりも相当前に作成されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-239">The events detailed in that blob may have been created well before the content blob was created.</span></span> <span data-ttu-id="4bf0c-240">そのため、特定の期間内に発生したイベントについて API を直接照会することはできません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-240">Therefore, you can never query the API directly for events that occurred within any given period.</span></span>

#### <a name="paging-contents-for-busy-tenants"></a><span data-ttu-id="4bf0c-241">ビジー状態のテナントに対するコンテンツのページング</span><span class="sxs-lookup"><span data-stu-id="4bf0c-241">Paging contents for busy tenants</span></span>

<span data-ttu-id="4bf0c-242">多くの大規模な Office 365 テナントでは、1 時間に数千ものイベントが生成されています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-242">Many larger Office 365 tenants have thousands of events being generated every hour.</span></span> <span data-ttu-id="4bf0c-243">これに該当する組織で、前述の例のように期間が 24 時間のクエリを実行すると、1 つの応答では返しきれないほどの通知の取得が必要になることがあります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-243">If this is the case with your organization, and you try to execute a query for a 24-hour period like in the example above, you may need to retrieve more notifications than can be returned in one response.</span></span> <span data-ttu-id="4bf0c-244">この場合、ある種の論理的なループの実装が必要になります。そのループでは、毎回、**NextPageUrl:** ヘッダー値について応答ヘッダーを調べます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-244">In this case, you'll need to implement a logical loop of some kind, each time checking the response headers for the **NextPageUrl:** header value.</span></span> <span data-ttu-id="4bf0c-245">詳細については、Office 365 マネージメント アクティビティ API リファレンスの「改ページ」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-245">See the Pagination section in the Office 365 Management Activity API reference for more details.</span></span>

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

<span data-ttu-id="4bf0c-246">このループ コードのテストは、極度に活発なテナントが存在していないと難しくなります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-246">It will be difficult to test this looping code unless you have a very active tenant.</span></span> <span data-ttu-id="4bf0c-247">スクリプトで数千回の更新操作を実行してテストしてみましたが、**NextPageUrl** ヘッダーの送信が必要になるほどの数の通知を生成することができませんでした。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-247">In our testing, we tried to execute several thousand update operations in a script and was unable to generate a large enough number of notifications to require the **NextPageUrl** header to be sent.</span></span>

### <a name="using-webhooks"></a><span data-ttu-id="4bf0c-248">Webhook の使用</span><span class="sxs-lookup"><span data-stu-id="4bf0c-248">Using webhooks</span></span>

<span data-ttu-id="4bf0c-249">コンテンツ BLOB が作成されたことを通知する方法は 2 つあります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-249">There two ways to get a notification that content blobs have been created.</span></span> <span data-ttu-id="4bf0c-250">*プッシュ* アプローチは、Webhook エンドポイントによって実装されます。このエンドポイントは、ユーザーが作成する Web アプリケーションで、ユーザー自身またはクラウド プラットフォームでホストします。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-250">The *push* approach is implemented with a webhook endpoint, which is a web application that you create and host yourself or on a cloud platform.</span></span> <span data-ttu-id="4bf0c-251">Webhook は、監査対象のコンテンツ タイプに対するサブスクリプションを作成するときに登録します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-251">You register the webhook at the time you create a subscription to an audited content type.</span></span> <span data-ttu-id="4bf0c-252">また、後述するアプローチを使用して、既存のサブスクリプションに Webhook の登録を追加することもできます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-252">You may also add a webhook registration to an existing subscription using the approach shown below.</span></span> <span data-ttu-id="4bf0c-253">*プル* アプローチでは、/content 操作を使用して、特定の期間 (24 時間以内) についてのクエリを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-253">The *pull* approach requires you to query for a particular timespan (no more than 24 hours) using the /content operation.</span></span> <span data-ttu-id="4bf0c-254">その応答によって、指定した期間中に作成されたコンテンツ BLOB が知らされます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-254">The response will tell you which content blobs were created during the period specified.</span></span>

<span data-ttu-id="4bf0c-255">Webhook を追加する前に、次の 2 つの問題について注意してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-255">Before you add a webhook, be aware of the following two issues:</span></span>

1. <span data-ttu-id="4bf0c-256">Webhook は、デバッグやトラブルシューティングに難点があるため Microsoft では重要視されなくなっています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-256">Webhooks are being de-emphasized by Microsoft because of the difficulty in debugging and troubleshooting.</span></span> <span data-ttu-id="4bf0c-257">通常、着信要求に応答する WebAPI エンドポイントはユーザーがホストすることになります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-257">Typically, you would host a WebApi endpoint that responds to incoming requests.</span></span> <span data-ttu-id="4bf0c-258">多くのユーザーは、ホスティング環境 (ユーザーが完全には制御できない環境) またはオンプレミス環境 (着信 HTTP 要求の許可が困難な環境) のどちらかを使用します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-258">Many customers either use hosting environments (which they don't have full control over) or on-premises environments (that have difficulty allowing incoming HTTP requests).</span></span> <span data-ttu-id="4bf0c-259">サポートでは、Office 365 監査パイプラインからの着信要求がファイアウォールやルーターによってブロックされるという多くの問題を確認しています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-259">Support has seen many problems where the incoming requests from the Office 365 auditing pipeline have been blocked by a firewall or router.</span></span> <span data-ttu-id="4bf0c-260">この場合、API ではバックオフ アルゴリズムを実装することになりますが、このアルゴリズムは複雑になることがあり、サブスクリプションで Webhook が無効になる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-260">In this case, the API will implement a back-off algorithm, which can be confusing and may result in disabling the webhook in the subscription.</span></span>

2. <span data-ttu-id="4bf0c-261">Webhook は、開始操作の実行後に、検証要求に即座に応答できるように準備が整っている必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-261">The webhook must be ready to immediately respond to a validation request after the start operation is executed.</span></span> <span data-ttu-id="4bf0c-262">Webhook アプリケーションにバグがあると、検証に失敗して Webhook は無効になります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-262">If there is a bug in the webhook application, the validation will fail, and the webhook will not be enabled.</span></span> <span data-ttu-id="4bf0c-263">検証要求スキーマの詳細については、Office 365 マネージメント アクティビティ API リファレンスの「Webhook 検証」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-263">For information about the validation request schema, see the Webhook validation section in the Office 365 Management Activity API reference.</span></span> <span data-ttu-id="4bf0c-264">マネージメント アクティビティ API の通知に応答する実稼働可能な Webhook を作成する際の問題点について慎重に検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-264">You should seriously consider the challenges in producing a production-ready webhook to respond to Management Activity API notifications.</span></span>

<span data-ttu-id="4bf0c-265">Webhook を実装する場合は、最初に呼び出される Webhook エンドポイントを指定する /start 操作の前に、そのエンドポイントが検証要求と通常の通知要求の両方に HTTP 200 応答で応答する準備ができていることを検証するためのテストが必要です。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-265">If you decide to implement a webhook, it should be tested to verify that the endpoint is prepared to respond with an HTTP 200 response to both the validation request and the normal notification requests before any /start operation that specifies a webhook endpoint is called for the first time.</span></span> <span data-ttu-id="4bf0c-266">通常、この準備状況をテストするには、API からの疑似要求を使用します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-266">Typically, you would use a mocked request from the API to test this readiness.</span></span> <span data-ttu-id="4bf0c-267">Office 365 マネージメント アクティビティ API リファレンスの「Webhook 検証」セクションと「コンテンツの取得」セクションの両方を慎重に読んで確認して、この 2 種類の要求のスキーマについて理解してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-267">Carefully read and observe both the Webhook validation and Retrieving content sections in the Office 365 Management Activity API reference to understand the schema of these two types of requests.</span></span>

<span data-ttu-id="4bf0c-268">Webhook エンドポイントでサブスクリプションを追加する場合は、body パラメーターを /start エンドポイントへの POST に追加します。次に例を示します:</span><span class="sxs-lookup"><span data-stu-id="4bf0c-268">To add a subscription with a webhook endpoint, add a body parameter to the POST to the /start endpoint; for example:</span></span>

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

<span data-ttu-id="4bf0c-269">この呼出しの直後に、検証要求が `https://webhook.myapp.com/o365/ …` に送信されます。Office 365 マネージメント アクティビティ API リファレンスの「Webhook 検証」セクションで説明されているように、この要求に応答できる状態のリスナーが存在している必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-269">Immediately following this call, a validation request will be sent out to `https://webhook.myapp.com/o365/ …` and there should be a listener ready to respond, as per the description in the Webhook validation section in the Office 365 Management Activity API reference.</span></span> <span data-ttu-id="4bf0c-270">リスナーは、HTTP 200 で応答する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-270">Your listener must respond with HTTP 200.</span></span> <span data-ttu-id="4bf0c-271">この時点で即座に /list 操作を実行すると、検証が正常に返されるまで null として示される以外の Webhook は表示されません。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-271">If you immediately run the /list operation at this point, you will not see the webhook shown as other than null until the validation has returned successfully.</span></span>

#### <a name="checking-notifications-to-webhooks"></a><span data-ttu-id="4bf0c-272">webhook への通知の確認</span><span class="sxs-lookup"><span data-stu-id="4bf0c-272">Checking notifications to webhooks</span></span>

<span data-ttu-id="4bf0c-273">/notifications 操作と /content 操作は区別することが重要です。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-273">It's important to distinguish between the /notifications operation and the /content operation.</span></span> <span data-ttu-id="4bf0c-274">通知の確認は、Webhook エンドポイントでサブスクライブした場合にのみ重要になります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-274">Checking notifications is only relevant if you have subscribed with a webhook endpoint.</span></span> <span data-ttu-id="4bf0c-275">この操作により、Webhook への通知が成功したかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-275">This operation will let you know if attempts to send notifications to your webhook have been successful or not.</span></span> <span data-ttu-id="4bf0c-276">この操作は、利用可能なコンテンツをリストするために使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-276">This operation should not be used to list available content.</span></span> <span data-ttu-id="4bf0c-277">すでに Webhook で受信している可能性のあるコンテンツが利用できるかどうかをクロスチェックする場合は、/content 操作を使用します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-277">To cross-check the availability of content against what you may have already received in your webhook, you would use the /content operation.</span></span> <span data-ttu-id="4bf0c-278">ただし、/notifications 操作を使用して、失敗した通知について最初に確認しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-278">But be sure to first check for failed notifications using the /notifications operation.</span></span>

### <a name="requesting-content-blobs-and-throttling"></a><span data-ttu-id="4bf0c-279">コンテンツ BLOB の要求と調整</span><span class="sxs-lookup"><span data-stu-id="4bf0c-279">Requesting content blobs and throttling</span></span>

<span data-ttu-id="4bf0c-280">コンテンツ URI のリストを取得したら、その URI で指定される BLOB を要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-280">After you've obtained a list of content URIs, you must request the blobs specified by the URIs.</span></span> <span data-ttu-id="4bf0c-281">PowerShell を使用して (Enterprise 組織の場合には manage.office.com API エンドポイントを使用して) コンテンツ BLOB を要求する例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-281">The following is an example of requesting a content blob (using the manage.office.com API endpoint for Enterprise organizations) using PowerShell.</span></span> <span data-ttu-id="4bf0c-282">この例は、この記事の「[アクセス トークンの取得](#getting-an-access-token)」セクションに示した例を使用してアクセス トークンを取得していることと、`$headerParams` 変数に適切な値が設定されていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-282">This example assumes you have already used the previous example in the [Getting an access token](#getting-an-access-token) section in this article to get an access token and have populated the `$headerParams` variable appropriately.</span></span>

```powershell
# Get a content blob
$uri = 'https://manage.office.com/api/v1.0/<<your-tenant-guid>>/activity/feed/audit/<<ContentID>$audit_sharepoint$Audit_SharePoint'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

<span data-ttu-id="4bf0c-283">前述の例の *$uri* 変数に関して、次の事項に注目してください。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-283">Note the following things about the *$uri* variable in the previous example:</span></span>

- <span data-ttu-id="4bf0c-284">PowerShell で *$* 記号が変数として解釈されないように、単一引用符を使用しています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-284">We used single quotes so that the *$* symbols aren't interpreted as variables in PowerShell</span></span>

- <span data-ttu-id="4bf0c-285">URI 全体は、前の /content エンドポイントへの呼出しに対する応答の *contentUri* プロパティで返されます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-285">The entire URI will be returned in the *contentUri* property of the response to your previous call to the /content endpoint.</span></span> <span data-ttu-id="4bf0c-286">プレースホルダーのトークンは、単に説明のために示したものです。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-286">The placeholder tokens shown are just for illustration.</span></span>

<span data-ttu-id="4bf0c-287">利用可能なコンテンツ BLOB を取得しようとすると、多くのユーザー (ほとんどの場合は、ビジー状態のテナントを使用しているユーザー) に次のようなエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-287">When attempting to retrieve the available content blobs, many customers (mostly working with busy tenants) have experienced errors that look like this:</span></span>

```json
Response Code 403: {'error':{'code':'AF429','message':'Too many requests. Method=GetBlob, PublisherId=00000000-0000-0000-0000-000000000000'}}
```

<span data-ttu-id="4bf0c-288">これは、調整が原因になっていると考えられます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-288">This is likely due to throttling.</span></span> <span data-ttu-id="4bf0c-289">PublisherId パラメーターの値に注目してください。この値は、クライアントが要求で *PublisherIdentifier* を指定していない可能性があることを示しています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-289">Note that the value of the PublisherId parameter likely indicates that the client didn't specify the *PublisherIdentifier* in the request.</span></span> <span data-ttu-id="4bf0c-290">また、403 エラー応答に *PublisherId* と表示されていても、正しいパラメーター名は *PublisherIdentifier* である点にも注意が必要です。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-290">Also, keep in mind that the correct parameter name is *PublisherIdentifier* even though you see *PublisherId* listed in the 403 error responses.</span></span>

> [!NOTE]
> <span data-ttu-id="4bf0c-291">API リファレンスでは、どの API 操作にも *PublisherIdentifier* パラメーターが示されていますが、このパラメーターはコンテンツ BLOB の取得時の contentUri URL に対する GET 要求にも含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-291">In the API reference, the *PublisherIdentifier* parameter is listed in every operation of the API, but it should also be included in the GET request to the contentUri URL when retrieving the content blob.</span></span>

<span data-ttu-id="4bf0c-292">問題のトラブルシューティングのために単純な API 呼び出しを実行する場合は (たとえば、サブスクリプションがアクティブかどうかを確認する場合)、*PublisherIdentifier* パラメーターを省略してもかまいませんが、最終的に実稼働用に使用するコードでは、すべての呼び出しに必ず *PublisherIdentifier* パラメーターを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-292">If you're doing simple API calls to troubleshoot problems (for example, checking if a given subscription is active) you can safely omit the *PublisherIdentifier* parameter, but absolutely any code that is eventually meant for production use should include the *PublisherIdentifier* parameter on every call.</span></span>

<span data-ttu-id="4bf0c-293">会社のテナントに対応するクライアントを実装する場合、*PublisherIdentifier* はテナント GUID になります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-293">If you're implementing a client for your company's tenant, the *PublisherIdentifier* is the Tenant GUID.</span></span> <span data-ttu-id="4bf0c-294">複数の顧客に対応する ISV アプリケーションまたはアドインを作成する場合、*PublisherIdentifier* は ISV のテナント GUID にする必要があります (エンド ユーザーの会社のテナント GUID ではありません)。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-294">If you are creating an ISV application or add-in for multiple customers, the *PublisherIdentifier* should be the ISV's Tenant GUID, and not the tenant GUID of end user's company.</span></span>

<span data-ttu-id="4bf0c-295">有効な *PublisherIdentifier* を含めると、テナントごとに 1 分あたり 60K の要求が割り当てられるプールに入れられます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-295">If you include the valid *PublisherIdentifier*, then you will be in a pool that is allotted 60K requests per minute per tenant.</span></span> <span data-ttu-id="4bf0c-296">これは、莫大な数の要求です。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-296">This is an exceptionally large number of requests.</span></span> <span data-ttu-id="4bf0c-297">ただし、*PublisherIdentifier* パラメーターを含めていないと、すべてのテナントに対して 1 分あたり 60K の要求が割り当てられる汎用プールに入れられます。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-297">However, if you don't include the *PublisherIdentifier* parameter, you will be in the general pool allotted 60K requests per minute for all tenants.</span></span> <span data-ttu-id="4bf0c-298">この場合、呼び出しが調整される可能性が高くなります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-298">In this case, you will more than likely find that your calls are getting throttled.</span></span> <span data-ttu-id="4bf0c-299">これを防止するために、*PublisherIdentifier* を使用してコンテンツ BLOB を要求する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-299">To prevent this, here's how you would request a content blob using the *PublisherIdentifier*:</span></span>

```json
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

<span data-ttu-id="4bf0c-300">前述の例は、*$response* 変数が /content エンドポイントに対する要求の応答で設定されていることと、*$headerParams* 変数に有効なアクセス トークンが含まれていることを前提としています。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-300">The previous example assumes that the *$response* variable was populated with the response to a request to the /content endpoint and that the *$headerParams* variable includes a valid access token.</span></span> <span data-ttu-id="4bf0c-301">このスクリプトでは、応答からのコンテンツ URI の配列内で最初の項目を取得し、その BLOB をダウンロードするために GET を呼び出して、*$contents* 変数に格納します。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-301">The script grabs the first item in the array of content URIs from the response and then invokes the GET to download that blob and put it in the *$contents* variable.</span></span> <span data-ttu-id="4bf0c-302">ユーザーのコードでは、*contentUri* ごとに GET を発行して、contentUri コレクション全体をループ処理することになります。</span><span class="sxs-lookup"><span data-stu-id="4bf0c-302">Your code will likely loop through the contentUri collection, issuing the GET for each *contentUri*.</span></span>
