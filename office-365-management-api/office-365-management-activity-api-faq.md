---
ms.TocTitle: Office 365 Management Activity API frequently asked questions
title: Office 365 マネージメント アクティビティ API についてよく寄せられる質問
description: Office 365 マネージメント アクティビティ API の使用についてよく寄せられる質問
ms.ContentId: ''
ms.topic: reference (API)
ms.date: 09/21/2018
ms.openlocfilehash: 612aac60ab421d79a1c866a4a79157ee255d167d
ms.sourcegitcommit: 525c0d0e78cc44ea8cb6a4bdce1858cb4ef91d57
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2018
ms.locfileid: "25834888"
---
# <a name="office-365-management-activity-api-frequently-asked-questions"></a>Office 365 マネージメント アクティビティ API についてよく寄せられる質問

#### <a name="what-events-are-audited-for-a-specific-office-365-service"></a>特定の Office 365 サービスについて、どのイベントが監査されますか?

総合的なイベントの一覧は、Office 365 マネージメント アクティビティ API スキーマのドキュメントに記載されています。 詳細については、「[Office 365 マネージメント アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)」を参照してください。

#### <a name="how-do-i-onboard-to-the-management-activity-api"></a>どのようにすればマネージメント アクティビティ API の使用を開始できますか?

Office 365 マネージメント アクティビティ API の使用を開始する方法については、「[Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)」を参照してください。
 
#### <a name="what-is-the-throttling-limit-for-the--management-activity-api"></a>マネージメント アクティビティ API の調整制限とは何ですか?

現在の調整制限は、パブリッシャー ID ごとに 60K 要求/分です。 

#### <a name="we-want-to-programmatically-capture-all-events-in-all-workloads-what-is-the-most-reliable-way-to-do-this"></a>すべてのワークロードのすべてのイベントをプログラムで取得しようと考えています。 この場合に最も確実な方法はありますか?

Office 365 マネージメント アクティビティ API を使用することで実現できます。 また、webhook の使用には問題があるため、**プル モデル**を使用することもお勧めします。 詳細については、「[Office 365 マネージメント アクティビティ API のトラブルシューティング](troubleshooting-the-office-365-management-activity-api.md#using-webhooks)」の「Webhook の使用」セクションを参照してください。

#### <a name="is-it-true-that-mailbox-auditing-in-exchange-online-can-only-be-enabled-by-using-powershell"></a>Exchange Online ではメールボックスの監査が PowerShell を使用してのみ有効化できるというのは本当ですか?

はい。 ただし、Office 365 組織のすべてのメールボックスに対して、既定でメールボックスの監査を有効化するための作業が進行中です。 詳細については、「[Microsoft セキュリティ、プライバシー、およびコンプライアンス ブログ](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Exchange-Mailbox-Auditing-will-be-enabled-by-default/ba-p/215171)」の「既定で有効化される Exchange メールボックスの監査」を参照してください。

#### <a name="are-there-any-differences-in-the-records-that-are-fetched-by-the-management-activity-api-versus-the-records-that-are-returned-by-using-the-audit-log-search-tool-in-the-office-365-security--compliance-center"></a>マネージメント アクティビティ API でフェッチされたレコードと、Office 365 セキュリティ/コンプライアンス センターの監査ログの検索ツールで返されたレコードに違いはありますか?

どちらの方法でも、同じデータが返されます。 フィルター処理は行われません。 唯一の相違点は、API では一度に取得できるデータが過去 7 日間のものであるということです。 セキュリティ/コンプライアンス センターでの監査ログの検査 (または、それに相当する Exchange Online での [Search-UnifiedAuditLog](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance-audit/search-unifiedauditlog) コマンドレットの使用) では、過去 90 日間のデータを取得できます。 
 
#### <a name="arent-webhook-notifications-more-immediate-after-all-arent-they-event-driven"></a>webhook 通知のほうが早くなりませんか? 結局のところ、イベント駆動型ではないですか?

いいえ。 Webhook 通知は、イベントによって通知がトリガーされるという意味ではイベント駆動ではありません。 コンテンツ BLOB の作成は依然として必要であり、コンテンツ BLOB の作成が通知の配信をトリガーします。 最近では、webhook の使用時の通知の待機時間は、*/content* 操作で API を直接クエリするよりも長くなっています。 そのため、マネージメント アクティビティ API は、リアルタイムのセキュリティ警告システムとして捉えることはできません。 Microsoft は、その目的のための別の製品を用意しています。 セキュリティに関する限り、マネージメント アクティビティ API のイベント通知は、長期間にわたる使用パターンを判断するために使用するほうが適しています。

#### <a name="when-pulling-the-data-from-the-management-activity-api-there-is-sometimes-a-delay-of-more-than-3-to-5-days-why-is-this"></a>マネージメント アクティビティ API からデータを収集するときに、3 日から 5 日以上の遅延が発生することがあります。 これはなぜですか?

一時的な停止などの問題が Office 365 サービスに発生するときがあります。 そうした場合、一部の監査レコードに取りこぼしが発生し、サービスは取りこぼしのバックフィルを試行します。 これは、レコードの約 5% から 10 % でのみ発生しますが、そのようなレコードに特定の状況で遅延が発生することがあります。 遅延期間が 5 日を過ぎた場合は、Office 365 管理センターのサービス正常性ダッシュボードを調べてください。 必要な場合は、[Microsoft サポート](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online)でチケットを開くこともできます。

#### <a name="i-am-encountering-a-throttling-error-in-the-management-activity-api-what-should-i-do"></a>マネージメント アクティビティ API で調整エラーが発生しました。 どうすればよいですか?

[Microsoft サポート](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online)でチケットを開いて、新しい調整制限を要求してください。また、制限の引き上げに対する業務上の正当な理由を含めてください。 要求が審査されて承諾されると、調整制限が引き上げられます。