---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management APIs overview
title: Office 365 管理 API の概要
description: Office 365 のお客様およびパートナーの、サービス通信、セキュリティ、コンプライアンス、レポート作成、監査を含むすべての管理タスクに対応する、単一の機能拡張プラットフォームを提供します。
ms.ContentId: 4fca85f9-efa6-3b4b-b10d-a07cb31f803f
ms.topic: reference (API)
ms.date: 09/28/2016
ms.localizationpriority: high
ms.openlocfilehash: 52924d518dd74f822a61977d96c5edbb7fc1e888
ms.sourcegitcommit: 13b50617b1a73f5890414087d8eabe6b2240cfb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2021
ms.locfileid: "58510112"
---
# <a name="office-365-management-apis-overview"></a>Office 365 管理 API の概要

Office 365 管理 API は、Office 365 のお客様およびパートナーの、サービス通信、セキュリティ、コンプライアンス、レポート作成、および監査を含むすべての管理タスクに対応する、単一の機能拡張プラットフォームを提供します。すべての Office 365 管理 API は、設計および実装において Office 365 REST API の現行スイートと一貫性があり、OAuth v2、OData v4、および JSON などの一般的な業界標準アプローチを使用しています。他の Office 365 API と同様、アプリケーションは Azure Active Directory で登録され、開発者はアプリの認証と承認を一貫した方法で受けることができます。

Office 365 管理 API についての質問がある場合は、質問を [Stack Overflow](http://stackoverflow.com/tags/office365) に、[office365] タグを使用して投稿します。

## <a name="office-365-service-communications-api-preview"></a>Office 365 サービス通信 API (プレビュー)

Office 365 サービス通信 API は、プレビュー モードでリリースされています。これは Office 365 サービス通信 API に置き換わるものであり、テナント管理者およびパートナーにサービス正常性の情報を提供します。以前のバージョンとは異なり、新しいサービス通信 API は、URL の名前付け、データ形式、および認証を含め、一貫した方式で構築された REST API により、まとまりのよいプラットフォーム操作性を提供します。

新機能は、新しいバージョンの API にのみ追加されます。旧バージョンをご使用のお客様は、早期の導入をお勧めします。Office 365 サービスの通信 API の通常のお知らせが行われた際に、サービス通信 API の旧バージョンの廃止に向けた期間が開始しました。 

操作のリファレンスについては、「[Office 365 サービス通信 API リファレンス (プレビュー)](office-365-service-communications-api-reference.md)」を参照してください。


## <a name="office-365-management-activity-api"></a>Office 365 管理アクティビティ API

Office 365 マネージメント アクティビティ API は、Office 365 と Azure Active Directory のアクティビティ ログからの、ユーザー、管理者、システム、およびポリシー アクションとポリシー イベントについての情報を提供します。お客様とパートナーは、この情報を使用して、操作、セキュリティ、およびコンプライアンス監視の新しい企業向けソリューションを作成したり、既存のソリューションを拡張したりできます。 

操作のリファレンスについては、「[Office 365 管理アクティビティ API リファレンス](office-365-management-activity-api-reference.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Office 365 管理 API の使用を開始する](get-started-with-office-365-management-apis.md)
- [Office 365 管理アクティビティ API のスキーマ](office-365-management-activity-api-schema.md)
- [Office 365 管理アクティビティ API のトラブルシューティング](troubleshooting-the-office-365-management-activity-api.md)
- [Office 365 REST API](/previous-versions/office/office-365-api/how-to/platform-development-overview)
