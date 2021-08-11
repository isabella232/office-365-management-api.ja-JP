---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management APIs overview
title: Office 365 管理 API の概要
description: Office 365 のお客様およびパートナーの、サービス通信、セキュリティ、コンプライアンス、レポート作成、監査を含むすべての管理タスクに対応する、単一の機能拡張プラットフォームを提供します。
ms.ContentId: 4fca85f9-efa6-3b4b-b10d-a07cb31f803f
ms.topic: reference (API)
ms.date: 09/28/2016
localization_priority: Priority
ms.openlocfilehash: 21c252bcd0fe422536dd8dc5a81b7a7c79fd2d04215a8f4c125af3116947b982
ms.sourcegitcommit: 88ef5f75a9e2a25760a2caa2cef1f51f9afba90c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2021
ms.locfileid: "54274211"
---
# <a name="office-365-management-apis-overview"></a>Office 365 管理 API の概要

Office 365 管理 API は、Office 365 のお客様およびパートナーの、サービス通信、セキュリティ、コンプライアンス、レポート作成、監査を含むすべての管理タスクに対応する、単一の機能拡張プラットフォームを提供します。 すべての Office 365 管理 API は、設計および実装において Office 365 REST API の現行スイートと一貫性があり、OAuth v2、OData v4、JSON などの一般的な業界標準アプローチを使用しています。 他の Office 365 API と同様、アプリケーションは Azure Active Directory で登録され、開発者はアプリの認証と承認を一貫した方法で受けることができます。

Office 365 管理 API についての質問がある場合は、質問を [Stack Overflow](http://stackoverflow.com/tags/office365) に、[office365] タグを使用して投稿します。

## <a name="office-365-service-communications-api-preview"></a>Office 365 サービス通信 API (プレビュー)

Office 365 サービス通信 API は、プレビュー モードでリリースされています。 これは Office 365 サービス通信 API に置き換わるものであり、テナント管理者およびパートナーにサービス正常性の情報を提供します。 以前のバージョンとは異なり、新しいサービス通信 API では、URL の名前付け、データ形式、認証などが一貫した方式で構築された REST API によって、まとまりのあるプラットフォームの操作性が提供されます。

新機能は、新しいバージョンの API にのみ追加されます。旧バージョンをご使用のお客様は、早期の導入をお勧めします。 Office 365 サービス通信 API の通常の製品発表が行われると、サービス通信 API の旧バージョンの廃止に向けた期間が開始されます。 

操作のリファレンスについては、「[Office 365 サービス通信 API リファレンス (プレビュー)](office-365-service-communications-api-reference.md)」を参照してください。


## <a name="office-365-management-activity-api"></a>Office 365 管理アクティビティ API

Office 365 管理アクティビティ API は、Office 365 と Azure Active Directory のアクティビティ ログからの、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を提供します。 お客様とパートナーは、この情報を使用して、操作、セキュリティ、およびコンプライアンス監視の新しい企業向けソリューションを作成したり、既存のソリューションを拡張したりできます。 

操作のリファレンスについては、「[Office 365 管理アクティビティ API リファレンス](office-365-management-activity-api-reference.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)
- [Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)
- [Office 365 管理アクティビティ API のトラブルシューティング](troubleshooting-the-office-365-management-activity-api.md)
- [Office 365 REST API](https://docs.microsoft.com/previous-versions/office/office-365-api/how-to/platform-development-overview)

