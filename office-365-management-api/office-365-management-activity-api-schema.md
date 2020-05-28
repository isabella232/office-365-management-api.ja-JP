---
ms.TocTitle: Office 365 Management Activity API schema
title: Office 365 管理アクティビティ API のスキーマ
description: Office 365 管理アクティビティ API のスキーマは、共通スキーマと製品固有スキーマの 2 つのレイヤーでデータ サービスとして提供されます。
ms.ContentId: 1c2bf08c-4f3b-26c0-e1b2-90b190f641f5
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 882967c45d8cee813ec1abb6064258e49a98a1e0
ms.sourcegitcommit: 91db29fbd6695c92ca5e5647b336d8f10ca267bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "44407442"
---
# <a name="office-365-management-activity-api-schema"></a>Office 365 管理アクティビティ API のスキーマ

Office 365 管理アクティビティ API のスキーマは、次の 2 つのレイヤーでデータ サービスとして提供されます。

- **共通スキーマ**。 レコードの種類、作成時刻、ユーザーの種類、およびアクションなどの中心的な Office 365 監査概念にアクセスし、コア ディメンション (ユーザー ID など)、場所の詳細情報 (クライアント IP アドレスなど)、および製品固有のプロパティ (オブジェクト ID など) を提供するインターフェイスです。 これにより一貫性がある統一ビューが確立され、いくつかの最上位ビューで適切なパラメーターを指定して、すべての Office 365 監査データを抽出できます。さらに、学習のコストを大幅に削減する、すべてのデータ ソース向けの固定スキーマも提供されます。 共通スキーマのデータは、Exchange、SharePoint、Azure Active Directory、Yammer、および OneDrive for Business などの各製品チームが所有する製品データから調達されます。 製品チームは [オブジェクト ID] フィールドを、製品固有のプロパティを追加するために拡張できます。

- **製品固有スキーマ**。 共通スキーマ上に構築され、製品固有の属性セット (Sway スキーマ、SharePoint スキーマ、OneDrive for Business スキーマ、および Exchange 管理者スキーマなど) を提供します。

**各自のシナリオでどのレイヤーを使用するべきですか?**
一般に、データが上位レイヤーで使用可能であれば、下位レイヤーには戻らないでください。 つまり、データ要件が製品固有のスキーマに適合できるのであれば、共通スキーマに戻る必要はありません。 

## <a name="office-365-management-api-schemas"></a>Office 365 管理 API のスキーマ

この記事では、共通スキーマと、製品固有の各スキーマについて詳細に説明します。 次の表では、使用可能なスキーマについて説明しています。 

|スキーマ名|説明|
|:-----|:-----|
|[共通スキーマ](#common-schema)|レコードの種類、ユーザー ID、クライアント IP、ユーザーの種類、およびアクションと、ユーザーのプロパティ (ユーザー ID など)、場所のプロパティ (クライアント IP など)、および製品固有のプロパティ (オブジェクト ID など) といったコア ディメンションを抽出するためのビューです。|
|[SharePoint 基本スキーマ](#sharepoint-base-schema)|共通スキーマを、すべての SharePoint 監査データに固有のプロパティで拡張します。|
|[SharePoint ファイルの操作](#sharepoint-file-operations)|SharePoint 基本スキーマを、ファイル アクセスと SharePoint での操作に固有のプロパティで拡張します。|
|[SharePoint 共有スキーマ](#sharepoint-sharing-schema)|SharePoint 基本スキーマを、ファイル共有に固有のプロパティで拡張します。|
|[SharePoint スキーマ](#sharepoint-schema)|SharePoint 基本スキーマを、SharePoint に固有であるものの、ファイル アクセスと操作には関連がないプロパティで拡張します。|
|[Project スキーマ](#project-schema)|SharePoint 基本スキーマを、プロジェクトに固有のプロパティで拡張します。|
|[Exchange 管理者スキーマ](#exchange-admin-schema)|共通スキーマを、すべての Exchange 管理者監査データに固有のプロパティで拡張します。|
|[Exchange メールボックス スキーマ](#exchange-mailbox-schema)|共通スキーマを、すべての Exchange メールボックス監査データに固有のプロパティで拡張します。|
|[Azure Active Directory 基本スキーマ](#azure-active-directory-base-schema)|共通スキーマを、すべての Azure Active Directory 監査データに固有のプロパティで拡張します。|
|[Azure Active Directory アカウント ログオン スキーマ](#azure-active-directory-account-logon-schema)|Azure Active Directory 基本スキーマを、すべての Azure Active Directory ログオン イベントに固有のプロパティで拡張します。|
|[Azure Active Directory の Secure STS ログオン スキーマ](#azure-active-directory-secure-token-service-sts-logon-schema)|Azure Active Directory 基本スキーマを、すべての Azure Active Directory の Secure Token Service (STS) ログオン イベントに固有のプロパティで拡張します。|
|[Azure Active Directory スキーマ](#azure-active-directory-schema)|共通スキーマを、すべての Azure Active Directory 監査データに固有のプロパティで拡張します。|
|[DLP スキーマ](#dlp-schema)|共通スキーマを、データ損失防止イベントに固有のプロパティで拡張します。|
|[セキュリティ/コンプライアンス センター スキーマ](#security-and-compliance-center-schema)|共通スキーマを、すべてのセキュリティ/コンプライアンス センターのイベントに固有のプロパティで拡張します。|
|[セキュリティ/コンプライアンス アラート スキーマ](#security-and-compliance-alerts-schema)|共通スキーマを、すべてのOffice 365 セキュリティ/コンプライアンス アラートに固有のプロパティで拡張します。|
|[Yammer スキーマ](#yammer-schema)|共通スキーマを、すべての Yammer イベントに固有のプロパティで拡張します。|
|[Sway スキーマ](#sway-schema)|共通スキーマを、すべての Sway イベントに固有のプロパティで拡張します。|
|[データ センター セキュリティ基本スキーマ](#data-center-security-base-schema)|共通スキーマを、すべてのデータ センター セキュリティ監査データに固有のプロパティで拡張します。|
|[データ センター セキュリティ コマンドレット スキーマ](#data-center-security-cmdlet-schema)|データ センター セキュリティ基本スキーマを、すべてのデータ センター セキュリティ コマンドレット監査データに固有のプロパティで拡張します。|
|[Microsoft Teams スキーマ](#microsoft-teams-schema)|共通スキーマを、すべての Microsoft Teams イベントに固有のプロパティで拡張します。|
|[Office 365 Advanced Threat Protection および脅威の調査と対応スキーマ](#office-365-advanced-threat-protection-and-threat-investigation-and-response-schema)|Office 365 Advanced Threat Protection および脅威の調査と対応のデータに固有のプロパティを使用して、共通スキーマを拡張します。|
|[自動調査および対応イベント スキーマ](#automated-investigation-and-response-events-in-office-365)|Office 365 自動調査および応答 (AIR) イベントに固有のプロパティを使用して、共通スキーマを拡張します。|
|[検疫イベントスキーマ](#hygiene-events-schema)|共通スキーマを、Exchange Online Protection と Advanced Threat Protection のイベントに固有のプロパティで拡張します。|
|[Power BI スキーマ](#power-bi-schema)|共通スキーマを、すべての Power BI イベントに固有のプロパティで拡張します。|
|[Dynamics 365 スキーマ](#dynamics-365-schema)|共通スキーマを、Dynamics 365 イベントに固有のプロパティで拡張します。|
|[Workplace Analytics スキーマ](#workplace-analytics-schema)|共通スキーマを、すべての Microsoft Workplace Analytics イベントに固有のプロパティで拡張します。|
|[検疫スキーマ](#quarantine-schema)|共通スキーマを、すべての検疫イベントに固有のプロパティで拡張します。|
|[Microsoft Forms スキーマ](#microsoft-forms-schema)|共通スキーマを、すべての Microsoft Forms イベントに固有のプロパティで拡張します。|
|[MIP ラベルのスキーマ](#mip-label-schema)|メール メッセージに手動または自動で適用される秘密度ラベルの固有のプロパティを使用して、共通のスキーマを拡張します。|
|[通信コンプライアンス Exchange スキーマ](#communication-compliance-exchange-schema)|共通スキーマを、コミュニケーションコンプライアンス不快の言葉モデルに固有のプロパティで拡張します。|
|||

## <a name="common-schema"></a>共通スキーマ

**EntityType の名前**: AuditRecord

|パラメーター|型|必須かどうか?|説明|
|:-----|:-----|:-----|:-----|
|Id|Combination GUIDEdm.Guid|はい|監査レコードの一意識別子。|
|RecordType|Self.[AuditLogRecordType](#auditlogrecordtype)|はい|レコードによって示される操作の種類。監査ログ レコードの種類の詳細については、[AuditLogRecordType](#auditlogrecordtype) の表を参照してください。|
|CreationTime|Edm.Date|はい|ユーザーがアクティビティを実行した、世界協定時刻 (UTC) での日時。|
|Operation|Edm.String|はい|ユーザーまたは管理者アクティビティの名前。 一般的な操作/アクティビティの説明については、「[Office 365 プロテクション センターでの監査ログの検索](https://go.microsoft.com/fwlink/p/?LinkId=708432)」を参照してください。 Exchange 管理者アクティビティでは、このプロパティは、実行されたコマンドレットの名前を識別します。 DLP イベントでは、これは "DlpRuleMatch"、"DlpRuleUndo" または "DlpInfo" (後続の「DLP スキーマ」で説明) になる可能性があります。|
|OrganizationId|Edm.Guid|はい|組織の Office 365 テナントの GUID。 この値は Office 365 サービスに関係なく、組織では常に同じ値になります。|
|UserType|Self.[UserType](#user-type)|はい|操作を実行したユーザーの種類。 ユーザーの種類の詳細については、「[ユーザーの種類](#user-type)」の表を参照してください。|
|UserKey|Edm.String|はい|UserId プロパティで識別されるユーザーの別の ID。たとえば、このプロパティには、SharePoint、OneDrive for Business、および Exchange のユーザーにより実行されたイベントの Passport 固有 ID (PUID) が格納されます。このプロパティは、他のサービスで発生するイベントや、システム アカウントで実行されるイベントの UseID プロパティと同じ値を指定することもできます。|
|Workload|Edm.String|いいえ|アクティビティが発生した Office 365 サービス。 
|ResultStatus|Edm.String|不要|(Operation プロパティで指定された) アクションが正常に終了したかどうかどうかを示します。 指定可能な値は **Succeeded**、**PartiallySucceeded**、または **Failed** です。 Exchange 管理者アクティビティでは、値は **True** または **False** のいずれかになります。<br/><br/>**重要**: さまざまなワークロードにより ResultStatus プロパティの値が上書きされる可能性があります。 たとえば、Azure Active Directory の STS ログオン イベントの場合、ResultStatus の**Succeeded**値によって示されるものは、HTTP 操作が正常に完了したことだけであり、ログオンが正常に完了したことを意味しません。 実際のログオンが成功しているかどうかを確認するには、「[Azure Active Directory の STS ログオン スキーマ](#azure-active-directory-secure-token-service-sts-logon-schema)」の LogonError プロパティを参照してください。 ログオンに失敗していた場合、このプロパティにはログオン試行に失敗した理由が含まれます。 |
|ObjectId|Edm.string|いいえ|SharePoint および OneDrive for Business のアクティビティの場合、ユーザーによりアクセスされるファイルまたはフォルダーの完全パス名。 Exchange 管理者の監査ログの場合は、コマンドレットによって変更されたオブジェクトの名前。|
|UserId|Edm.string|はい|レコードがログに記録されることになった、(Operation プロパティで指定された) アクションを実行したユーザーの UPN (ユーザー プリンシパル名)。たとえば、`my_name@my_domain_name` などです。 システム アカウント (SHAREPOINT\system または NT AUTHORITY\SYSTEM など) で実行されるアクティビティのレコードも含まれることに注意してください。 SharePoint では、UserId プロパティの別の値が app@sharepoint に表示されます。 これは、アクティビティを実行した "ユーザー" が、ユーザー、管理者、またはサービスの代理として、組織全体のアクション (SharePoint サイトまたは OneDrive アカウント検索など) を実行するために必要な アクセス許可が SharePoint に与えられているアプリケーションであることを示しています。 詳細については、「[監査レコード内の app@sharepoint ユーザー](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#the-appsharepoint-user-in-audit-records)」を参照してください。 |
|ClientIP|Edm.String|はい|アクティビティがログに記録されたときに使用されたデバイスの IP アドレス。IP アドレスは、IPv4 または IPv6 アドレスの形式で表示されます。<br/><br/>一部のサービスでは、このプロパティに表示される値は、ユーザーに代わってサービスを呼び出す信頼できるアプリケーション (Office on the web アプリなど) の IP アドレスであり、アクティビティを実行したユーザーが使用するデバイスの IP アドレスではない場合があります。 <br/><br/>また、Azure Active Directory 関連のイベントの場合、 IP アドレスはログに記録されず、ClientIP プロパティの値は `null` になります。|
|範囲|Self.[AuditLogScope](#auditlogscope)|いいえ|このイベントは、ホストされた O365 サービスまたはオンプレミスのサーバーによって作成されたものですか。 設定できる値は **online** および **onprem** です。 SharePoint は現在、オンプレミスから O365 にイベントを送信する唯一のワークロードです。|
|||||

### <a name="enum-auditlogrecordtype---type-edmint32"></a>列挙値: AuditLogRecordType - 型: Edm.Int32

#### <a name="auditlogrecordtype"></a>AuditLogRecordType

|値|メンバ名|説明|
|:-----|:-----|:-----|
|1 |ExchangeAdmin|Exchange 管理者監査ログからのイベント。|
|pbm-2|ExchangeItem|単一のアイテムに対して実行されるアクション (単一の電子メール メッセージの作成や受信など) の、Exchange メールボックス監査ログからのイベント。|
|1/3|ExchangeItemGroup|複数のアイテムに対して実行できるアクション (1 つ以上の電子メール メッセージの移動や削除など) の、Exchange メールボックス監査ログからのイベント。|
|4 |SharePoint|SharePoint イベント。|
|6 |SharePointFileOperation|SharePoint ファイル操作イベント。|
|8 |AzureActiveDirectory|Azure Active Directory イベント。|
|9 |AzureActiveDirectoryAccountLogon|Azure Active Directory OrgId ログオン イベント (非推奨)。|
|10  |DataCenterSecurityCmdlet|データ センター セキュリティ コマンドレット イベント。|
|#|ComplianceDLPSharePoint|SharePoint のデータ損失防止 (DLP) イベントと OneDrive for Business。|
|12 |Sway|Sway サービスおよびクライアントからのイベント。|
|スリー|ComplianceDLPExchange|統合 DLP ポリシーを使用して構成された場合の Exchange のデータ損失防止 (DLP) イベント。 Exchange トランスポート ルールに基づく DLP イベントはサポートされていません。|
|14 |SharePointSharingOperation|SharePoint 共有イベント。|
|約|AzureActiveDirectoryStsLogon|Azure Active Directory の Secure Token Service (STS) ログオン イベント。|
|18 |SecurityComplianceCenterEOPCmdlet|セキュリティ センターとコンプライアンス センターの管理者アクション|
|1280|PowerBIAudit|Power BI イベント。|
| 21|CRM|Dynamics 365 イベント。|
|×|Yammer|Yammer イベント。|
|最高|SkypeForBusinessCmdlets|Skype for Business イベント。|
|ソケット|Discovery|セキュリティ/コンプライアンス センターでコンテンツ検索を実行し、eDiscovery のケースを管理することによって実行される、電子情報開示アクティビティのイベント。|
|まで|MicrosoftTeams|Microsoft Teams のイベント。|
|個|ThreatIntelligence|Exchange Online Protection と Office 365 Advanced Threat Protection からのフィッシングとマルウェアのイベント。|
|29|MailSubmission|Exchange Online Protection と Office 365 Advanced Threat Protection からの送信イベント。|
|31|MicrosoftFlow|Microsoft Power Automate (旧称 Microsoft Flow) イベント。|
|31|AeD|Advanced eDiscovery イベント。|
|32|MicrosoftStream|Microsoft Stream のイベント。|
|33|ComplianceDLPSharePointClassification|SharePoint の DLP 分類に関連するイベント。|
|35|Project|Microsoft Project のイベント。|
|36|SharePointListOperation|SharePoint リスト イベント。|
|38|DataGovernance|セキュリティ/コンプライアンス センターにおけるアイテム保持ポリシーと保持ラベルに関連するイベント|
|40|SecurityComplianceAlerts|セキュリティ/コンプライアンス アラートのシグナル。|
|41|ThreatIntelligenceUrl|ブロック時の安全なリンクと Office 365 Advanced Threat Protection からのイベントの上書きブロック。|
|42|SecurityComplianceInsights|Office 365 セキュリティおよびコンプライアンス センターの分析情報とレポートに関連するイベント。|
|43|MIPLabel|秘密度ラベルで (手動または自動で) タグ付けされたメール メッセージのトランスポート パイプラインでの検出に関連するイベント。 |
|44|WorkplaceAnalytics|Workplace Analytics イベント。|
|45|PowerAppsApp|Power Apps イベント。|
|47|ThreatIntelligenceAtpContent|SharePoint、OneDrive for Business、Microsoft Teams のファイルについての Office 365 Advanced Threat Protection からのフィッシングとマルウェアのイベント。|
|48|LabelContentExplorer|[データ分類コンテンツ エクスプローラー](https://docs.microsoft.com/microsoft-365/compliance/data-classification-content-explorer)に関係するイベント。|
|49|TeamsHealthcare|Microsoft 医療関係向けのTeams の[患者アプリケーション](https://docs.microsoft.com/MicrosoftTeams/expand-teams-across-your-org/healthcare/patients-audit)に関連するベント。|
|51|HygieneEvent|送信スパム保護に関連するイベント。 |
|52|DataInsightsRestApiAudit|データ インサイト REST API イベント。|
|54|SharePointListItemOperation|SharePoint リスト アイテム イベント。|
|55|SharePointContentTypeOperation|SharePoint リスト コンテンツ タイプ イベント。|
|56|SharePointFieldOperation|SharePoint リスト フィールド イベント。|
|64|AIR 調査|自動インシデント応答 (AIR) イベント|
|65|Quarantine|検疫イベント。|
|66|MicrosoftForms|Microsoft Forms イベント。|
|68|ComplianceSupervisionExchange|通信コンプライアンス不快な言語モデルによって追跡されたイベント。|
||||

### <a name="enum-user-type---type-edmint32"></a>列挙値: User Type - 型: Edm.Int32

#### <a name="user-type"></a>ユーザーの種類

|値|メンバ名|説明|
|:-----|:-----|:-----|
|.0|Regular|正規ユーザー。|
|1 |Reserved|予約済みユーザー。|
|pbm-2|Admin|管理者。|
|1/3|DcAdmin|Microsoft データセンターのオペレーター。|
|4 |System|システム アカウント。|
|5 |Application|アプリケーション。|
|6 |ServicePrincipal|サービス プリンシパル。|
|7 |CustomPolicy|カスタム ポリシー。|
|8 |SystemPolicy|システム ポリシー。|
||||

### <a name="enum-auditlogscope---type-edmint32"></a>列挙値: AuditLogScope - 型: Edm.Int32

#### <a name="auditlogscope"></a>AuditLogScope

|値|メンバ名|説明|
|:-----|:-----|:-----|
|.0|Online|このイベントは、ホストされた O365 サービスによって作成されました。|
|1 |Onprem|このイベントは、オンプレミスのサーバーによって作成されました。|
||||

## <a name="sharepoint-base-schema"></a>SharePoint Base schema

|**パラメーター**|**型**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|サイト|Edm.Guid|いいえ|ユーザーによりアクセスされるファイルまたはフォルダーが置かれているサイトの GUID。|
|ItemType|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[ItemType](#itemtype)"|いいえ|アクセスまたは変更されたオブジェクトの種類。オブジェクトの種類の詳細については、「[ItemType](#itemtype)」の表を参照してください。|
|EventSource|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[EventSource](#eventsource)"|いいえ|SharePoint でイベントが発生したことを示します。 指定可能な値は **SharePoint** または **ObjectModel**。|
|SourceName|Edm.String|いいえ|監査対象の操作をトリガーしたエンティティ。 指定可能な値は、SharePoint または **ObjectModel**。|
|UserAgent|Edm.String|不要|ユーザーのクライアントまたはブラウザーに関する情報。この情報は、クライアントまたはブラウザーによって提供されます。|
|MachineDomainInfo|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|いいえ|デバイスの同期操作に関する情報。この情報は、要求で指定されている場合にのみ報告されます。|
|MachineId|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|いいえ|デバイスの同期操作に関する情報。この情報は、要求で指定されている場合にのみ報告されます。|
|||||

### <a name="enum-itemtype---type-edmint32"></a>列挙:ItemType - タイプ:Edm.Int32

#### <a name="itemtype"></a>ItemType

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Invalid|アイテムは、その他の種類のアイテム (この表にリストされている) のいずれでもありません。|
|1 |File|アイテムはファイルです。|
|5 |Folder|アイテムはフォルダーです。|
|6 |Web|アイテムは Web です。|
|7 |Site|アイテムはサイトです。|
|8 |Tenant|アイテムはテナントです。|
|9 |DocumentLibrary|アイテムはドキュメント ライブラリです。|
|#|Page|アイテムはページです。|
||||

### <a name="enum-eventsource---type-edmint32"></a>列挙値: EventSource - 型: Edm.Int32

#### <a name="eventsource"></a>EventSource

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|SharePoint|イベント ソースは SharePoint です。|
|1 |ObjectModel|イベント ソースは ObjectModel です。|
||||

### <a name="enum-sharepointauditoperation---type-edmint32"></a>列挙:SharePointAuditOperation - タイプ:Edm.Int32

|**メンバー名**|**説明**|
|:-----|:-----|
|AccessInvitationAccepted*|共有ファイル (またはフォルダー) の表示または編集への招待の受信者が、招待のリンクをクリックして共有ファイルにアクセスしました。|
|AccessInvitationCreated*|ユーザーは、SharePoint または OneDrive for Business サイトにある共有ファイルまたはフォルダーの表示または編集への招待を、(組織の内外の) 他のユーザーに送信します。イベント エントリの詳細は、共有されたファイルの名前、招待状の送付先ユーザー、および招待を送信したユーザーが選択した共有アクセス許可の種類を示します。|
|AccessInvitationExpired*|外部ユーザーに送信する招待に有効期限を設定します。既定では、組織外のユーザーに送信する招待は、招待が承諾されない場合には 7 日後に有効期限が切れます。|
|AccessInvitationRevoked*|SharePoint または OneDrive for Business のサイト管理者、サイト所有者、またはドキュメント所有者は、組織外のユーザーに送信された招待を取り下げます。招待は、承諾前にのみ取り下げることができます。|
|AccessInvitationUpdated*|SharePoint または OneDrive for Business サイトにある共有ファイルまたはフォルダーの表示または編集への招待を作成して送信したユーザーが、招待を再送します。|
|AccessRequestApproved|SharePoint または OneDrive for Business のサイト管理者、サイト所有者、またはドキュメント所有者は、サイトまたはドキュメントにアクセスするユーザー要求を承認します。|
|AccessRequestCreated|ユーザーは、アクセス許可がない SharePoint または OneDrive for Business のサイトまたはドキュメントへのアクセス権限を要求します。 |
|AccessRequestRejected*|SharePoint のサイト管理者、サイト所有者、またはドキュメント所有者は、サイトまたはドキュメントへのアクセスを求めるユーザー要求を拒否します。|
|ActivationEnabled*|ユーザーは、フォーム コードが含まれていないフォーム テンプレートをブラウザー対応にする、完全な信頼を要求する、モバイル デバイスでのレンダリングを有効にする、サーバー管理者が管理するデータ接続を使用する、などができます。|
|AdministratorAddedToTermStore*|用語ストア管理者が追加されました。|
|AdministratorDeletedFromTermStore*|用語ストア管理者が削除されました。|
|AllowGroupCreationSet*|サイト管理者またはサイト所有者は、許可が割り当てられたユーザーが SharePoint または OneDrive for Business サイトのグループを作成できる許可レベルを、それらのサイトに追加します。|
|AppCatalogCreated*|SharePoint 環境でカスタム ビジネス アプリを利用できるように、アプリ カタログが作成されました。|
|AuditPolicyRemoved*|サイト コレクションのドキュメント ライフサイクル ポリシーが削除されました。|
|AuditPolicyUpdate*|サイト コレクションのドキュメント ライフサイクル ポリシーが更新されました。|
|AzureStreamingEnabledSet*|ビデオ ポータルの所有者が、Azure からのビデオ ストリーミングを許可されました。|
|CollaborationTypeModified*|サイト (イントラネット、エクストラネット、またはパブリックなど) で許可されているコラボレーションの種類が変更されました。|
|ConnectedSiteSettingModified|ユーザーが Project Web App でプロジェクトとプロジェクト サイト間のリンクを作成、変更、または削除したか、ユーザーがリンク上の同期設定を変更します。|
|CreateSSOApplication*|ターゲット アプリケーションが Secure Store Service で作成されました。|
|CustomFieldOrLookupTableCreated|ユーザーが Project Web App でユーザー設定フィールドまたはルックアップ テーブル/アイテムを作成しました。|
|CustomFieldOrLookupTableDeleted|ユーザーが Project Web App でユーザー設定フィールドまたはルックアップ テーブル/アイテムを削除しました。|
|CustomFieldOrLookupTableModified|ユーザーが Project Web App でユーザー設定フィールドまたはルックアップ テーブル/アイテムを変更しました。|
|CustomizeExemptUsers*|グローバル管理者が、SharePoint 管理センターで適用除外ユーザー エージェントのリストをカスタマイズしました。インデックスを作成する Web ページ全体を受け取らせないように除外するユーザー エージェントを指定できます。つまり、除外対象として指定したユーザー エージェントが InfoPath フォームを検出すると、フォームは、Web ページ全体ではなく XML ファイルとして返されます。これにより InfoPath フォームのインデックス作成の速度が上がります。|
|DefaultLanguageChangedInTermStore*|用語ストアで変更された言語設定。|
|DelegateModified|ユーザーが Project Web App でセキュリティの代理人を作成または変更しました。|
|DelegateRemoved|ユーザーが Project Web App でセキュリティの代理人を削除しました。|
|DeleteSSOApplication*|SSO アプリケーションが削除されました。|
|eDiscoveryHoldApplied*|インプレース ホールドが、コンテンツ ソースに置かれました。インプレース ホールドは、SharePoint で (電子情報開示センターなどの) 電子情報開示サイト コレクションを使用して管理されます。|
|eDiscoveryHoldRemoved*|インプレース ホールドが、コンテンツ ソースから削除されました。インプレース ホールドは、SharePoint で (電子情報開示センターなどの) 電子情報開示サイト コレクションを使用して管理されます。|
|eDiscoverySearchPerformed*|電子情報開示検索は、SharePoint の電子情報開示サイト コレクションを使用して実行されました。|
|EngagementAccepted|ユーザーが Project Web App でリソースのエンゲージメントを承諾します。|
|EngagementModified|ユーザーが Project Web App でリソースのエンゲージメントを変更します。|
|EngagementRejected|ユーザーが Project Web App でリソースのエンゲージメントを拒否します。|
|EnterpriseCalendarModified|ユーザーが Project Web App でエンタープライズ カレンダーをコピー、変更、または削除します。|
|EntityDeleted|ユーザーが Project Web App でタイムシートを削除します。|
|EntityForceCheckedIn|ユーザーが Project Web App で、予定表、ユーザー設定フィールド、またはルックアップ テーブルに対してチェックインを強制します。|
|ExemptUserAgentSet*|グローバル管理者が、SharePoint 管理センターで適用除外ユーザー エージェントのリストにユーザー エージェントを追加しました。|
|FileAccessed|ユーザーまたはシステム アカウントは、SharePoint または OneDrive for Business サイトにあるファイルにアクセスします。システム アカウントが FileAccessed イベントを生成する場合もあります。|
|FileCheckOutDiscarded*|ユーザーは、チェックアウトしたファイルを破棄します (または元に戻します)。つまり、チェックアウト時にファイルに加えた変更はすべて破棄され、ドキュメント ライブラリ内のドキュメントのバージョンには保存されないということです。|
|FileCheckedIn*|ユーザーは、SharePoint または OneDrive for Business ドキュメント ライブラリからチェックアウトしたドキュメントをチェックインします。|
|FileCheckedOut*|ユーザーは、SharePoint または OneDrive for Business ドキュメント ライブラリにあるドキュメントをチェックアウトします。共有しているドキュメントは、複数のユーザーがチェックアウトし、変更を加えることができます。|
|FileCopied|ユーザーは、SharePoint または OneDrive for Business サイトからドキュメントをコピーします。コピーしたファイルは、サイト上の別のフォルダーに保存できます。|
|FileDeleted|ユーザーは、SharePoint または OneDrive for Business サイトからドキュメントを削除します。|
|FileDeletedFirstStageRecycleBin|ユーザーが SharePoint または OneDrive for Business サイトのごみ箱からファイルを削除します。|
|FileDeletedSecondStageRecycleBin|ユーザーが SharePoint または OneDrive for Business サイトの第 2 段階のごみ箱からファイルを削除します。|
|FileDownloaded|ユーザーは、SharePoint または OneDrive for Business サイトからドキュメントをダウンロードします。|
|FileFetched|このイベントは、FileAccessed イベントに置き換えられており、推奨されていません。|
|FileModified|ユーザーまたはシステム アカウントは、SharePoint あるいは OneDrive for Business サイトにあるドキュメントの内容またはプロパティを変更します。|
|FileMoved|ユーザーが SharePoint または OneDrive for Business サイトの現在の場所から新しい場所にドキュメントを移動します。|
|FilePreviewed|ユーザーが SharePoint または OneDrive for Business サイトにあるドキュメントをプレビューします。|
|FileRenamed|ユーザーは、SharePoint または OneDrive for Business サイトにあるドキュメントの名前を変更します。|
|FileRestored|ユーザーは、SharePoint または OneDrive for Business サイトのごみ箱からドキュメントを復元します。 |
|FileSyncDownloadedFull|ユーザーは、同期関係を確立し、SharePoint または OneDrive for Business ドキュメント ライブラリから自分のコンピューターに初めてファイルを正常にダウンロードします。|
|FileSyncDownloadedPartial|ユーザーは、SharePoint または OneDrive for Business ドキュメント ライブラリから、ファイルに加えたすべての変更内容を正常にダウンロードします。このイベントは、ドキュメント ライブラリ内のファイルに加えたすべての変更内容がユーザーのコンピューターにダウンロードされたことを示します。ドキュメント ライブラリは (FileSyncDownloadedFull イベントが示すとおり) ユーザーによって以前ダウンロードされているため、変更内容のみがダウンロードされました。|
|FileSyncUploadedFull*|ユーザーは、同期関係を確立し、自分のコンピューターから SharePoint または OneDrive for Business ドキュメント ライブラリに初めてファイルを正常にアップロードします。|
|FileSyncUploadedPartial*|ユーザーは、SharePoint または OneDrive for Business ドキュメント ライブラリにあるファイルに、変更内容を正常にアップロードします。このイベントは、ドキュメント ライブラリからダウンロードしたローカル バージョンのファイルに加えた変更内容が、ドキュメント ライブラリに正常にアップロードされたことを示します。ファイルは (FileSyncUploadedFull イベントが示すとおり) ユーザーによって以前にアップロードされているため、変更内容のみがアップロードされます。|
|FileUploaded|ユーザーは、SharePoint または OneDrive for Business サイトにあるフォルダーにドキュメントをアップロードします。 |
|FileViewed|このイベントは、FileAccessed イベントに置き換えられており、推奨されていません。|
|FolderCopied|ユーザーがフォルダーを SharePoint または OneDrive for Business サイトから SharePoint または OneDrive for Business の別の場所にコピーします。|
|FolderCreated|ユーザーが SharePoint または OneDrive for Business サイトでフォルダーを作成します。|
|FolderDeleted|ユーザーが SharePoint または OneDrive for Business サイトからフォルダーを削除します。|
|FolderDeletedFirstStageRecycleBin|ユーザーが SharePoint または OneDrive for Business サイトのごみ箱からフォルダーを削除します。|
|FolderDeletedSecondStageRecycleBin|ユーザーが SharePoint または OneDrive for Business サイトの第 2 段階のごみ箱からフォルダーを削除します。|
|FolderModified|ユーザーが SharePoint または OneDrive for Business サイトでフォルダーを変更します。 このイベントには、フィルダーのメタデータ (タグやプロパティなど) の変更が含まれます。|
|FolderMoved|ユーザーが SharePoint または OneDrive for Business サイトからフォルダーを移動します。|
|FolderRenamed|ユーザーが SharePoint または OneDrive for Business サイトのフォルダーの名前を変更します。|
|FolderRestored|ユーザーが SharePoint または OneDrive for Business サイトのごみ箱からフォルダーを復元します。|
|GroupAdded*|サイト管理者または所有者は、SharePoint または OneDrive for Business のグループを作成するか、グループが作成されることになるタスクを実行します。たとえば、ユーザーがファイルを共有するためのリンクを初めて作成すると、システム グループがユーザーの OneDrive for Business に追加されます。ユーザーが共有ファイルの編集許可があるリンクを作成したときにも、このイベントになる場合があります。|
|GroupRemoved*|ユーザーは、SharePoint または OneDrive for Business サイトからグループを削除します。 |
|GroupUpdated*|サイト管理者または所有者は、SharePoint または OneDrive for Business サイトのグループの設定を変更します。これには、グループの名前、グループ メンバーシップを表示または編集できるユーザー、およびメンバーシップ要求を処理する方法の変更を含めることができます。|
|LanguageAddedToTermStore*|用語ストアに言語が追加されました。|
|LanguageRemovedFromTermStore*|用語ストアから言語が削除されました。|
|LegacyWorkflowEnabledSet*|サイト管理者または所有者は、SharePoint ワークフロー タスク コンテンツ タイプをサイトに追加します。グローバル管理者は、SharePoint 管理センターで組織全体のワークフローを有効にすることもできます。|
|LookAndFeelModified|ユーザーがサイド リンク バー、ガント チャートの書式、またはグループの形式を変更します。 または、ユーザーが Project Web App でビューを作成、変更、または削除します。|
|ManagedSyncClientAllowed|ユーザーが SharePoint または OneDrive for Business サイトとの同期関係を正常に確立します。 ユーザーのコンピューターが、組織内のドキュメント ライブラリにアクセスできるドメインのリスト (宛先セーフ リストと呼ばれる) に追加されているドメインのメンバーであるため、同期関係は成功しました。 詳細については、「[SharePoint Online PowerShell を使用する](https://go.microsoft.com/fwlink/p/?LinkID=534609)」を参照し、宛先セーフ リスト上のドメインに対して OneDrive 同期を有効にしてください。|
|MaxQuotaModified*|サイトの最大クォータは変更されています。|
|MaxResourceUsageModified*|サイトの最大許容リソース配分状況は変更されています。|
|MySitePublicEnabledSet*|SharePoint 管理者によって、ユーザーが公開 MySite を持てるようにするフラグが設定されています。|
|NewsFeedEnabledSet*|サイト管理者または所有者は、SharePoint または OneDrive for Business サイトの RSS フィードを有効にします。グローバル管理者は、SharePoint 管理センターで組織全体の RSS フィードを有効にできます。|
|ODBNextUXSettings*|OneDrive for Business 用の新しい UI が使用可能になっています。|
|OfficeOnDemandSet*|サイト管理者は、Office オンデマンドを有効にします。これによりユーザーは、Office デスクトップ アプリケーションの最新バージョンにアクセスできます。Office オンデマンドは Office SharePoint 管理センターで有効にされ、インストール済みのすべての Office アプリケーションを含む Office 365 サブスクリプションを必要とします。|
|PageViewed|ユーザーが SharePoint または OneDrive for Business サイトにあるページを表示します。 これには、SharePoint サイトまたは One Drive for Business サイトのドキュメント ライブラリのファイルをブラウザーで表示することは含まれません。|
|PeopleResultsScopeSet*|サイト管理者は、SharePoint サイトの人の検索の結果ソースを作成または変更します。|
|PermissionSyncSettingModified|ユーザーが Project Web App でプロジェクトのアクセス許可の同期設定を変更します。|
|PermissionTemplateModified|ユーザーが Project Web App で、アクセス許可テンプレートを作成、変更、または削除します。|
|PortfolioDataAccessed|ユーザーが Project Web App で、ポートフォリオのコンテンツ (ドライバー ライブラリ、ドライバーの優先順位付け、ポートフォリオ分析) にアクセスします。|
|PortfolioDataModified|ユーザーが Project Web App で、ポートフォリオのデータ (ドライバー ライブラリ、ドライバーの優先順位付け、ポートフォリオ分析) を作成、変更、または削除します。|
|PreviewModeEnabledSet*|サイト管理者は、SharePoint サイトのドキュメント プレビューを有効にします。|
|ProjectAccessed|ユーザーが Project Web App でプロジェクトのコンテンツにアクセスします。|
|ProjectCheckedIn|ユーザーが Project Web App からチェックアウトしたプロジェクトをチェックインします。|
|ProjectCheckedOut|ユーザーが Project Web App にあるプロジェクトをチェックアウトします。 ユーザーが開く権限を持つプロジェクトをチェックアウトして、変更することができます。|
|ProjectCreated|ユーザーが Project Web App でプロジェクトを作成します。|
|ProjectDeleted|ユーザーが Project Web App でプロジェクトを削除します。|
|ProjectForceCheckedIn|ユーザーが Project Web App でプロジェクトに対してチェックインを強制します。|
|ProjectModified|ユーザーが Project Web App でプロジェクトを変更します。|
|ProjectPublished|ユーザーが Project Web App でプロジェクトを公開します。|
|ProjectWorkflowRestarted|ユーザーが Project Web App でワークフローを再起動します。|
|PWASettingsAccessed|ユーザーが CSOM を使用して、Project Web App の設定にアクセスします。|
|PWASettingsModified|ユーザーが Project Web App の構成を変更します。|
|QueueJobStateModified|ユーザーが Project Web App でキュー ジョブをキャンセルまたは再開します。|
|QuotaWarningEnabledModified*|ストレージ クォータ警告が変更されました。|
|RenderingEnabled*|ブラウザー対応フォーム テンプレートが、InfoPath フォーム サービスでレンダリングされます。|
|ReportingAccessed|ユーザーが Project Web App でレポートのエンドポイントにアクセスしました。|
|ReportingSettingModified|ユーザーが Project Web App でレポートの構成を変更します。|
|ResourceAccessed|ユーザーが Project Web App でエンタープライズ リソースのコンテンツにアクセスします。|
|ResourceCheckedIn|ユーザーが Project Web App からチェックアウトしたエンタープライズ リソースをチェックインします。|
|ResourceCheckedOut|ユーザーが Project Web App にあるエンタープライズ リソースをチェックアウトします。|
|ResourceCreated|ユーザーが Project Web App でエンタープライズ リソースを作成します。|
|ResourceDeleted|ユーザーが Project Web App でエンタープライズ リソースを削除します。|
|ResourceForceCheckedIn|ユーザーが Project Web App でエンタープライズ リソースのチェックインを強制します。|
|ResourceModified|ユーザーが Project Web App でエンタープライズ リソースを変更します。|
|ResourcePlanCheckedInOrOut|ユーザーが Project Web App でリソース計画をチェックインまたはチェックアウトします。|
|ResourcePlanModified|ユーザーが Project Web App でリソース計画を変更します。|
|ResourcePlanPublished|ユーザーが Project Web App でリソース計画を公開します。|
|ResourceRedacted|ユーザーが Project Web App でエンタープライズ リソースを編集し、すべての個人情報を削除します。|
|ResourceWarningEnabledModified*|リソース クォータ警告が変更されました。|
|SSOGroupCredentialsSet*|Secure Store Service でグループ資格情報が設定されました。|
|SSOUserCredentialsSet*|Secure Store Service でユーザー資格情報が設定されました。|
|SearchCenterUrlSet*|検索センターの URL が設定されました。|
|SecondaryMySiteOwnerSet*|ユーザーがその MySite に代理所有者を追加しました。|
|SecurityCategoryModified|ユーザーが Project Web App で、セキュリティのカテゴリを作成、変更、または削除します。|
|SecurityGroupModified|ユーザーが Project Web App で、セキュリティ グループを作成、変更、または削除します。|
|SendToConnectionAdded*|グローバル管理者は、SharePoint 管理センターの [レコード管理] ページで、新しい [送信先] 接続を作成します。[送信先] 接続は、ドキュメント リポジトリまたはレコード センターの設定を指定します。[送信先] 接続を作成すると、コンテンツ オーガナイザーにより、指定された場所にドキュメントを送信できます。|
|SendToConnectionRemoved*|グローバル管理者は、SharePoint 管理センターの [レコード管理] ページで、[送信先] 接続を削除します。|
|SharedLinkCreated|ユーザーは、SharePoint または OneDrive for Business で共有ファイルへのリンクを作成します。このリンクは、共有ファイルにアクセスできるように他のユーザーに送信できます。ユーザーは、共有ファイルの表示と編集を許可するリンク、またはファイルの表示だけを許可するリンクの、2 種類のリンクを作成できます。|
|SharedLinkDisabled*|ユーザーは、ファイルを共有するために作成されたリンクを (完全に) 無効にします。|
|SharingInvitationAccepted*|User accepts an invitation to share a file or folder. This event is logged when a user shares a file with other users.|
|SharingRevoked*|ユーザーは、他のユーザーと以前に共有していたファイルまたはフォルダーを共有解除します。このイベントは、ユーザーが他のユーザーとのファイルの共有を停止すると記録されます。|
|SharingSet|ユーザーは、SharePoint または OneDrive for Business にあるファイルまたはフォルダーを、組織内の他のユーザーと共有します。|
|SiteAdminChangeRequest*|ユーザーが、SharePoint サイト コレクションのサイト コレクション管理者として追加されるように要求します。サイト コレクション管理者は、サイト コレクションとすべてのサブサイトのフル コントロール権限を持ちます。|
|SiteCollectionAdminAdded*|サイト コレクション管理者または所有者は、ユーザーを SharePoint または OneDrive for Business サイトのサイト コレクション管理者として追加します。サイト コレクション管理者は、サイト コレクションとすべてのサブサイトのフル コントロール権限を持ちます。|
|SiteCollectionCreated*| グローバル管理者は、SharePoint 組織に新しいサイト コレクションを作成します。|
|SiteRenamed*|サイト管理者または所有者は、SharePoint または OneDrive for Business サイトの名前を変更します。|
|StatusReportModified|ユーザーが Project Web App で、進捗レポートを作成、変更、または削除します。|
|SyncGetChanges*|ユーザーがドキュメント ライブラリ内のファイルに加えたすべての変更内容を自分のコンピューターに同期するために、SharePoint または OneDrive for Business のアクション トレイにある **[同期]** をクリックします。|
|TaskStatusAccessed|ユーザーが Project Web App で、1 つまたは複数のタスクの状態にアクセスします。|
|TaskStatusApproved|ユーザーが Project Web App で、1 つまたは複数のタスクの状態の更新を承認します。|
|TaskStatusRejected|ユーザーが Project Web App で、1 つまたは複数のタスクの状態の更新を拒否します。|
|TaskStatusSaved|ユーザーが Project Web App で、1 つまたは複数のタスクの状態の更新を保存します。|
|TaskStatusSubmitted|ユーザーが Project Web App で、1 つまたは複数のタスクの状態の更新を送信します。|
|TimesheetAccessed|ユーザーが Project Web App でタイムシートにアクセスします。|
|TimesheetApproved|ユーザーが Project Web App でタイムシートを承認します。|
|TimesheetRejected|ユーザーが Project Web App でタイムシートを拒否します。|
|TimesheetSaved|ユーザーが Project Web App でタイムシートを保存します。|
|TimesheetSubmitted|ユーザーが Project Web App で状態のタイムシートを送信します。|
|UnmanagedSyncClientBlocked|ユーザーは、組織のドメインのメンバーではないコンピューター、または組織のドキュメント ライブラリにアクセスできるものの、ドメインのリスト (宛先セーフ リスト) に追加されていないドメインのメンバーであるコンピューターから、SharePoint または OneDrive for Business サイトとの同期関係を確立しようとします。 同期関係は許可されていません。ユーザーのコンピューターは、ドキュメント ライブラリ上のファイルの同期、ダウンロード、アップロードがブロックされています。 この機能については、「[Windows PowerShell コマンドレットを使用して宛先セーフ リスト上のドメインに対して OneDrive 同期を有効にする](https://docs.microsoft.com/powershell/module/sharepoint-online/index?view=sharepoint-ps)」を参照してください。|
|UpdateSSOApplication*|ターゲット アプリケーションが Secure Store Service で更新されました。|
|UserAddedToGroup*|サイト管理者または所有者は、SharePoint または OneDrive for Business サイトにあるグループにユーザーを追加します。ユーザーをグループに追加すると、そのユーザーにはグループに割り当てられたアクセス許可が付与されます。 |
|UserRemovedFromGroup*|サイト管理者または所有者は、SharePoint または OneDrive for Business サイトにあるグループからユーザーを削除します。削除されると、そのユーザーにはグループに割り当てられたアクセス許可は付与されなくなります。 |
|WorkflowModified|ユーザーが Project Web App で、エンタープライズ プロジェクトの種類、ワークフローのフェーズ、またはステージを作成、変更、または削除します。|
|||||


> [!NOTE] 
> *この操作はプレビュー段階です。

## <a name="sharepoint-file-operations"></a>SharePoint ファイルの操作

「[セキュリティ/コンプライアンス センターでの監査ログの検索](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance)」の「ファイルとフォルダーのアクティビティ」セクションにリストされているファイル関連 SharePoint イベントは、このスキーマを使用します。



|**パラメーター**|**型**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|SiteUrl|Edm.String|はい|ユーザーによりアクセスされるファイルまたはフォルダーが置かれているサイトの URL。|
|SourceRelativeUrl|Edm.String|不要|ユーザーがアクセスするファイルが含まれているフォルダーの URL。_SiteURL_、_SourceRelativeURL_、および _SourceFileName_ パラメーターの値の組み合わせは、**ObjectID** プロパティの値と同じであり、ユーザーがアクセスするファイルの完全パス名です。|
|SourceFileName|Edm.String|はい|ユーザーによりアクセスされるファイルまたはフォルダーの名前。|
|SourceFileExtension|Edm.String|不要|ユーザーがアクセスしたファイルのファイル拡張子。このプロパティは、アクセスされたオブジェクトがフォルダーの場合には、空白になります。|
|DestinationRelativeUrl|Edm.String|不要|ファイルのコピー先または移動先フォルダーの URL。_SiteURL_、_SourceRelativeURL_、および _SourceFileName_ パラメーターの値の組み合わせは、**ObjectID** プロパティの値と同じであり、コピーされたファイルの完全パス名です。このプロパティは、FileCopied および FileMoved イベントに対してのみ表示されます。|
|DestinationFileName|Edm.String|不要|コピーまたは移動したファイルの名前。このプロパティは、FileCopied および FileMoved イベントに対してのみ表示されます。|
|DestinationFileExtension|Edm.String|不要|コピーまたは移動したファイルのファイル拡張子。このプロパティは、FileCopied および FileMoved イベントに対してのみ表示されます。|
|UserSharedWith|Edm.String|不要|リソースを共有したユーザー。|
|SharingType|Edm.String|不要|リソースを共有したユーザーに割り当てられているアクセス許可の種類。このユーザーは、_UserSharedWith_ パラメーターにより識別されます。|
|||||


## <a name="sharepoint-sharing-schema"></a>SharePoint 共有スキーマ

 ファイル共有関連の SharePoint イベント。 これは、ユーザーが別のユーザーに何らかの影響があるアクションを取るという点で、ファイル関連イベントやフォルダー関連イベントとは異なります。 SharePoint 共有スキーマについては、「[Office 365 監査ログで共有監査を使う](https://docs.microsoft.com/microsoft-365/compliance/use-sharing-auditing
)」を参照してください。



|**パラメーター**|**型**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|TargetUserOrGroupName |Edm.String|不要|リソースを共有していたターゲット ユーザーまたはグループの UPN または名前を格納します。|
|TargetUserOrGroupType|Edm.String|不要|ターゲット ユーザーまたはグループが、メンバー、ゲスト、グループ、またはパートナーであるかどうかを示します。 |
|EventData|XML コード|いいえ|グループへのユーザーの追加や編集アクセス許可の付与などの、発生した共有アクションに関する追加情報を伝達します。|
|||||


## <a name="sharepoint-schema"></a>SharePoint スキーマ

「[セキュリティ/コンプライアンス センターでの監査ログの検索](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance)」にリストされている SharePoint イベント (ファイルおよびフォルダー イベントを除く) は、このスキーマを使用します。


|**パラメーター**|**型**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|CustomEvent|Edm.String|不要|カスタム イベントのオプション文字列。|
|EventData|Edm.String|不要|カスタム イベントのオプション ペイロード。|
|ModifiedProperties|Collection(ModifiedProperty)|いいえ|このプロパティは、サイトまたはサイト コレクション管理者グループのメンバーとしてユーザーを追加するなどの、管理イベントの場合に含まれます。プロパティには、変更されたプロパティの名前 (サイト管理者グループなど)、変更されたプロパティの新しい値 (サイト管理者として追加されたユーザーなど)、および変更されたオブジェクトの以前の値が含まれます。|
|||||

## <a name="project-schema"></a>Project スキーマ

|**パラメーター**|**型**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|Entity|Edm.String|はい| 監査の対象になった [ProjectEntity](#project-entity)。|
|Action|Edm.String|はい|取得された [ProjectAction](#project-action)。|
|OnBehalfOfResId|Edm.Guid|いいえ|アクションが実行されたリソース ID。|
|||||

### <a name="enum-project-action---type-edmint32"></a>列挙値: Project Action - 型: Edm.Int32

#### <a name="project-action"></a>Project 操作　

|**メンバー名**|**説明**|
|:-----|:-----|
|Accepted|ユーザーがイベントまたはワークフローを承諾しました。|
|Accessed|ユーザーがエンティティにアクセスしました。|
|Activated|ユーザーがエンティティ、イベント、またはワークフローをアクティブ化しました。|
|Cancelled|ユーザーがイベントまたはワークフローをキャンセルしました。|
|CheckedIn|ユーザーがエンティティをチェックインします。|
|CheckedOut|ユーザーがエンティティをチェックアウトします。|
|Copied|ユーザーがエンティティをコピーしました。|
|Created|ユーザーがエンティティを作成しました。|
|Deactivated|ユーザーがエンティティを非アクティブ化しました。|
|Deleted|ユーザーがエンティティを削除しました。|
|Exported|ユーザーがエンティティをエクスポートしました。|
|ForceCheckedIn|ユーザーがエンティティを強制的にチェックインさせました。|
|Modified|ユーザーがエンティティを変更しました。|
|Published|ユーザーがエンティティを公開しました。|
|Redacted|ユーザーがエンティティを編集しました。|
|Rejected|ユーザーがエンティティを拒否しました。|
|Restarted|ユーザーがイベントまたはワークフローを再起動しました。|
|Saved|ユーザーがエンティティを保存しました。|
|Sent|ユーザーがエンティティを送信しました。|
|Submitted|ユーザーがレビューまたはワークフローのエンティティを送信します。|
|||||

### <a name="enum-project-entity---type-edmint32"></a>列挙値: Project Entity - 型: Edm.Int32

#### <a name="project-entity"></a>Project エンティティ

|**メンバー名**|**説明**|
|:-----|:-----|
|CustomField|エンタープライズ ユーザー設定フィールドを表します。|
|Driver|ポートフォリオのドライバーを表します。|
|DriverPrioritization|ポートフォリオの優先順位付けを表します。|
|Engagement|リソースのエンゲージメントを表します。|
|EnterpriseCalendar|エンタープライズ リソース カレンダーを表します。|
|EnterpriseProjectType|エンタープライズ プロジェクトの種類を表します。|
|FiscalPeriod|会計期間を表します。|
|GanttChartFormat|ガント チャートの書式を表します。|
|GroupingFormat|ビューのグループ化の書式を表します。|
|LineClassification|タイムシート行の分類を表します。|
|LookupTable|エンタープライズ ルックアップ テーブルを表します。|
|PermissionTemplate|セキュリティ アクセス許可のテンプレートを表します。|
|PortfolioAnalysis|ポートフォリオ分析を表します。|
|Project|プロジェクトを表します。|
|QueueJob|キュー ジョブを表します。|
|QuickLaunch|サイド リンク バーの項目を表します。|
|Reporting|レポートのエンドポイントを表します。|
|Resource|エンタープライズ リソースを表します。|
|ResourcePlan|プロジェクトに関連付けられたリソース計画を表します。|
|SecurityCategory|セキュリティのカテゴリを表します。|
|SecurityGroup|セキュリティ グループを表します。|
|Setting|Project Web App の設定を表します|
|Statusing|タスクの状態の更新を表します。|
|StatusReport|進捗レポートを表します。|
|TimeReportingPeriod|タイムシートの期間を表します|
|Timesheet|タイムシートのエンティティを表します。|
|TimesheetAuditLog|タイムシートの監査ログを表します。|
|TimesheetManager|タイムシートの管理者を表します。|
|UserDelegate|別のユーザーへのユーザー委任を表します。|
|View|ビューの定義を表します。|
|WorkflowPhase|ワークフローのフェーズを表します。|
|WorkflowStage|ワークフローのステージを表します。|
|||||

## <a name="exchange-admin-schema"></a>Exchange Admin schema


|**パラメーター**|**型**|**必須**|**説明**|
|:-----|:-----|:-----|:-----|
|ModifiedObjectResolvedName|Edm.String|不要|これはコマンドレットによって変更されたオブジェクトのユーザー フレンドリ名です。これはコマンドレットによるオブジェクトの変更の場合にのみ記録されます。|
|パラメーター|Collection(Common.NameValuePair)|いいえ|Operations プロパティで示されているコマンドレットで使用された、すべてのパラメーターの名前と値。|
|ModifiedProperties|Collection(Common.ModifiedProperty)|いいえ|このプロパティは、管理イベント用に組み込まれています。プロパティには、変更されたプロパティの名前、変更されたプロパティの新しい値、および変更されたオブジェクトの以前の値が含まれます。|
|ExternalAccess|Edm.Boolean|はい|組織内のユーザー、Microsoft データセンター担当者またはデータセンター サービス アカウント、あるいは代理管理者により、コマンドレットが実行されたかどうかを示します。 値 **False** は、コマンドレットが組織内のユーザーによって実行されたことを示します。 値 **True** は、コマンドレットがデータセンターの担当者、データセンターのサービス アカウント、または代理管理者によって実行されたことを示します。|
|OriginatingServer|Edm.String|不要|コマンドレット実行元のサーバーの名前。|
|OrganizationName|Edm.String|いいえ|テナントの名前。|
|||||

## <a name="exchange-mailbox-schema"></a>Exchange メールボックス スキーマ


|**パラメーター**|**型**|**必須**|**説明**|
|:-----|:-----|:-----|:-----|
|LogonType|Self.[LogonType](#logontype)|いいえ| メールボックスにアクセスして、ログに記録された操作を実行したユーザーの種類を示します。|
|InternalLogonType|Self.[LogonType](#logontype)|いいえ|内部使用のため予約済みです。|
|MailboxGuid|Edm.String|不要|アクセスされたメールボックスの Exchange GUID。|
|MailboxOwnerUPN|Edm.String|不要|アクセスされたメールボックスの所有者の電子メール アドレス。|
|MailboxOwnerSid|Edm.String|不要|メールボックス所有者の SID。|
|MailboxOwnerMasterAccountSid|Edm.String|不要|メールボックス所有者のアカウントのマスター アカウント SID。|
|LogonUserSid|Edm.String|いいえ|操作を実行したユーザーの SID。|
|LogonUserDisplayName|Edm.String|不要|操作を実行したユーザーのユーザー フレンドリ名。|
|ExternalAccess|Edm.Boolean|はい|これは、ログオン ユーザーのドメインがメールボックス所有者のドメインと異なる場合は、true です。|
|OriginatingServer |Edm.String|不要|これは、操作の発生場所です。|
|OrganizationName|Edm.String|不要|テナントの名前。|
|ClientInfoString|Edm.String|不要|操作を実行するために使用された電子メール クライアントについての情報 (ブラウザーのバージョン、Outlook のバージョン、およびモバイル デバイスの情報など)。|
|ClientIPAddress|Edm.String|不要|操作がログに記録されたときに使用されたデバイスの IP アドレス。IP アドレスは、IPv4 または IPv6 アドレスの形式で表示されます。|
|ClientMachineName|Edm.String|不要|Outlook クライアントをホストしているマシン名。|
|ClientProcessName|Edm.String|不要|メールボックスへのアクセスに使用された電子メール クライアント。 |
|ClientVersion|Edm.String|不要|電子メール クライアントのバージョン。|
|||||

### <a name="enum-logontype---type-edmint32"></a>列挙:LogonType - タイプ:Edm.Int32

#### <a name="logontype"></a>LogonType


|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Owner|メールボックス所有者。|
|1 |Admin|他のユーザーのメールボックスに対する管理者特権を持つユーザー。|
|pbm-2|委任|他のユーザーのメールボックスに対する代理人特権を持つユーザー。|
|1/3|Transport|Microsoft データセンターのトランスポート サービス。|
|4 |SystemService|Microsoft データセンターのサービス アカウント。|
|5 |BestAccess|内部使用のため予約済みです。|
|6 |DelegatedAdmin|代理管理者。|
|||||

### <a name="exchangemailboxauditgrouprecord-schema"></a>ExchangeMailboxAuditGroupRecord スキーマ


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|フォルダー|Self.[ExchangeFolder](#exchangefolder-complex-type)|いいえ|アイテムのグループが存在するフォルダー。|
|CrossMailboxOperations|Edm.Boolean|いいえ|操作に複数のメールボックスが関係したかどうかを示します。|
|DestMailboxId|Edm.Guid|いいえ|CrossMailboxOperations パラメーターが **True** の場合にのみ設定します。 ターゲット メールボックスの GUID を指定します。|
|DestMailboxOwnerUPN|Edm.String|いいえ|CrossMailboxOperations パラメーターが **True** の場合にのみ設定します。 ターゲット メールボックス所有者の UPN を指定します。|
|DestMailboxOwnerSid|Edm.String|いいえ|CrossMailboxOperations パラメーターが **True** の場合にのみ設定します。 ターゲット メールボックスの SID を指定します。|
|DestMailboxOwnerMasterAccountSid|Edm.String|いいえ|CrossMailboxOperations パラメーターが **True** の場合にのみ設定します。 ターゲット メールボックス所有者のマスター アカウント SID の SID を指定します。|
|DestFolder|Self.[ExchangeFolder](#exchangefolder-complex-type)|いいえ|移動などの操作の場合の、移動先フォルダー。|
|Folders|Collection(Self.[ExchangeFolder](#exchangefolder-complex-type))|いいえ|操作に関連したソース フォルダーに関する情報 (フォルダーが選択されて削除された場合など)。|
|AffectedItems|Collection(Self.[ExchangeItem](#exchangeitem-complex-type))|いいえ|グループ内の各項目についての情報。|
|||||


### <a name="exchangemailboxauditrecord-schema"></a>ExchangeMailboxAuditRecord スキーマ


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|アイテム|Self.[ExchangeItem](#exchangeitem-complex-type)|いいえ|操作の実行対象のアイテムを表します。|
|ModifiedProperties|Collection(Edm.String)|不要|TBD|
|SendAsUserSmtp|Edm.String|不要|偽装しているユーザーの SMTP アドレス。|
|SendAsUserMailboxGuid|Edm.Guid|いいえ|電子メールを偽装ユーザーとして送信するためにアクセスされたメールボックスの Exchange GUID。|
|SendOnBehalfOfUserSmtp|Edm.String|不要|電子メールが代理で送信されたユーザーの SMTP アドレス。|
|SendOnBehalfOfUserMailboxGuid|Edm.Guid|いいえ|電子メールを代理で送信するためにアクセスされたメールボックスの Exchange GUID。|
|||||

### <a name="exchangeitem-complex-type"></a>ExchangeItem 複合型


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|はい|ストア ID。|
|Subject|Edm.String|不要|アクセスされたメッセージの件名。|
|ParentFolder|Edm.ExchangeFolder|いいえ|アイテムが置かれているフォルダーの名前。|
|Attachments|Edm.String|不要|メッセージに添付されているすべてのアイテムの名前とファイル サイズのリスト。|
|||||

### <a name="exchangefolder-complex-type"></a>ExchangeFolder 複合型


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|はい|フォルダー オブジェクトのストアの ID。|
|Path|Edm.String|不要|アクセスされたメッセージが置かれているメールボックス フォルダーの名前。|
|||||


## <a name="azure-active-directory-base-schema"></a>Azure Active Directory 基本スキーマ


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|AzureActiveDirectoryEventType|Self.[AzureActiveDirectoryEventType](#azureactivedirectoryeventtype)|はい|Azure AD イベントの種類。 |
|ExtendedProperties|Collection(Common.NameValuePair)|いいえ|Azure AD イベントの拡張プロパティ。|
|ModifiedProperties|Collection(Common.ModifiedProperty)|いいえ|このプロパティは、管理イベント用に組み込まれています。プロパティには、変更されたプロパティの名前、変更されたプロパティの新しい値、および変更されたプロパティの以前の値が含まれています。|
|||||

### <a name="enum-azureactivedirectoryeventtype---type--edmint32"></a>列挙:AzureActiveDirectoryEventType - タイプ: -Edm.Int32

#### <a name="azureactivedirectoryeventtype"></a>AzureActiveDirectoryEventType

|**メンバー名**|**説明**|
|:-----|:-----|
|AccountLogon|アカウント ログイン イベント。|
|AzureApplicationAuditEvent|Azure アプリケーション セキュリティ イベント。|
|||||

## <a name="azure-active-directory-account-logon-schema"></a>Azure Active Directory アカウント ログオン スキーマ


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|アプリケーション|Edm.String|いいえ|Office 15 などの、アカウント ログイン イベントをトリガーするアプリケーション。|
|Client|Edm.String|いいえ|クライアント デバイス、デバイスの OS、およびアカウント ログイン イベントに使用したデバイスのブラウザーに関する詳細。|
|LoginStatus|Edm.Int32|はい|このプロパティは、OrgIdLogon.LoginStatus に直接由来しています。関心の対象となるさまざまなログオン失敗のマッピングは、警告アルゴリズムによって行うことができます。|
|UserDomain|Edm.String|はい|テナント ID 情報 (TII)。|
|||||


### <a name="enum-credentialtype---type-edmint32"></a>列挙:CredentialType - タイプ:Edm.Int32


|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|-1|Other|その他の認証。|
|.0|Password|ユーザー資格情報は、ユーザー名とパスワードです。|
|1 |MobilePhone|ユーザー資格情報は、携帯電話です。|
|pbm-2|SecretQuestion|ユーザー資格情報は、秘密の質問です。|
|1/3|SecurePin|ユーザー資格情報は、セキュア PIN です。|
|4 |SecurePinReset|ユーザー資格情報は、セキュア PIN リセットです。|
|#|EasyID|ユーザー資格情報は、EasyID です。|
|14 |PasswordIndexCredentialType|ユーザー資格情報は、PasswordIndexCredentialType です。|
|16 |Device|ユーザー資格情報は、デバイスです。|
|17 |ForeignRealmIndex|ユーザーの資格情報は、ForeignRealmIndex です。|
|||||

### <a name="enum-logintype---type-edmint32"></a>列挙:LoginType - タイプ:Edm.Int32


|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|-1|Other|その他の i タイプ。|
|1 |InitialAuth|最初の認証でログイン。|
|pbm-2|CookieCopy|Cookie を使用してログイン。|
|1/3|SilentReAuth|自動再認証でログイン。|
|||||

### <a name="enum-authenticationmethod---type-edmint32"></a>列挙:AuthenticationMethod - タイプ:Edm.Int32


|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Min|認証方法は、Min です。|
|1 |Password|認証方法は、パスワードです。|
|pbm-2|Digest|認証方法は、ダイジェストです。|
|1/3|ProxyAuth|認証方法は、ProxyAuth です。|
|4 |InfoCard|認証方法は、InfoCard です。|
|5 |DAToken|認証方法は、DAToken です。|
|6 |Sha1RememberMyPassword|認証方法は、Sha1RememberMyPassword です。|
|7 |LMPasswordHash|認証方法は、LMPasswordHash です。|
|8 |ADFSFederatedToken|認証方法は、ADFSFederatedToken です。|
|9 |EID|認証方法は、EID です。|
|10  |DeviceID|認証方法は、DeviceID です。 |
|#|MD5|認証方法は、MD5 です。|
|12 |EncProxyPasswordHash|認証方法は、EncProxyPasswordHash です。|
|スリー|LWAFederation|認証方法は、LWAFederation です。|
|14 |Sha1HashedPassword|認証方法は、Sha1HashedPassword です。|
|約|SecurePin|認証方法は、セキュア PIN です。|
|16 |SecurePinReset|認証方法は、セキュア PIN リセットです。|
|17 |SAML20PostSimpleSign|認証方法は、SAML20PostSimpleSign です。|
|18 |SAML20Post|認証方法は、SAML20Post です。|
|年|OneTimeCode|認証方法は、ワンタイム・コードです。|
|||||


## <a name="azure-active-directory-schema"></a>Azure Active Directory スキーマ


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|Actor|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|いいえ|アクションを実行したユーザーまたはサービス プリンシパル。|
|ActorContextId|Edm.String|不要|アクターが属する組織の GUID。|
|ActorIpAddress|Edm.String|不要|IPV4 または IPV6 アドレス形式の、アクターの IP アドレス。|
|InterSystemsId|Edm.String|不要|Office 365 サービス内の複数のコンポーネント間でアクションを追跡する GUID。|
|IntraSystemsId|Edm.String|不要|アクションを追跡するために Azure Active Directory で生成された GUID。|
|SupportTicketId|Edm.String|不要|「代理人」状態でのアクションのカスタマー サポート チケット ID。|
|Target|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|いいえ|アクション (Operation プロパティで示される) の実行対象であったユーザー。|
|TargetContextId|Edm.String|不要|対象ユーザーが属する組織の GUID。|
|||||

### <a name="complex-type-identitytypevaluepair"></a>複合型 IdentityTypeValuePair


|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|はい|種類を指定した ID の値。|
|種類|Self.IdentityType|はい|ID の種類。|
|||||

### <a name="enum-identitytype---type-edmint32"></a>列挙:IdentityType - タイプ:Edm.Int32

#### <a name="identitytype"></a>IdentityType

|**メンバー名**|**説明**|
|:-----|:-----|
|クレーム|ID は、認証目的の要求です。|
|Name|監査アクション アクターまたはターゲット ID の表示名。|
|Other|アクターの ID は、Office 365 サービスによって生成された GUID の ObjectId などの、他の種類です。|
|PUID|監査アクション アクターまたはターゲット パスポートの固有 ID (PUID)。|
|SPN|Office 365 サービスでアクションが実行される場合、サービス プリンシパルの ID。|
|UPN|ユーザー プリンシパル名。|
|||||


## <a name="azure-active-directory-secure-token-service-sts-logon-schema"></a>Azure Active Directory の Secure Token Service (STS) ログオン スキーマ

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|ApplicationId|Edm.String|不要|ログインを要求しているアプリケーションを表す GUID。表示名は、Azure Active Directory グラフ API を使用して検索できます。|
|クライアント|Edm.String|いいえ|ログインを実行するブラウザーが提供する、クライアント デバイス情報。|
|LogonError|Edm.String|不要|失敗したログインの場合、ログインが失敗した理由が含まれます。 LogonErrors の詳細な説明については「[認証と承認エラー コード](https://docs.microsoft.com/azure/active-directory/develop/reference-aadsts-error-codes#aadsts-error-codes)」の一覧を参照してください。
|||||

## <a name="dlp-schema"></a>DLP スキーマ

DLP イベントは、Exchange Online、SharePoint Online、および OneDrive For Business で使用できます。 Exchange の DLP イベントは、統合された DLP ポリシーに基づいたイベント (セキュリティ/コンプライアンス センターで構成されたものなど) でのみ使用できます。 Exchange トランスポート ルールに基づく DLP イベントはサポートされていません。

共通スキーマでは、DLP (データ損失防止) イベントに必ず UserKey="DlpAgent" があります。 共通スキーマの Operation プロパティの値として格納される 3 種類の DLP イベントがあります。

- DlpRuleMatch: ルールが一致したことを示します。 これらのイベントは、Exchange、SharePoint Online、OneDrive for Business のいずれにも存在します。 Exchange では、誤検知と上書きの情報が含まれます。 SharePoint Online と OneDrive for Business では、誤検知と上書きは異なるイベントを生成します。

- DlpRuleUndo: SharePoint Online と OneDrive for Business にのみ存在し、ユーザーによる対象の誤検知/上書きにより、またはドキュメントがポリシーの適用対象ではなくなった (ポリシーを変更したか、ドキュメントのコンテンツを変更したため) ことにより、以前に適用されたポリシー アクションが取り消された ("undone") ことを示します。

- DlpInfo: SharePoint Online と OneDrive for Business にのみ存在し、対象を誤検知したものの、取り消された ("undone") アクションはないことを示します。

|**パラメーター**|**型**|**必須**|**説明**|
|:-----|:-----|:-----|:-----|
|SharePointMetaData|Self.[SharePointMetadata](#sharepointmetadata-complex-type)|いいえ|機密情報を含む SharePoint または OneDrive for Business 内のドキュメントに関するメタデータを記述します。|
|ExchangeMetaData|Self.[ExchangeMetadata](#exchangemetadata-complex-type)|いいえ|機密情報を含んだ電子メール メッセージに関するメタデータを記述します。|
|ExceptionInfo|Edm.String|いいえ|ポリシーが適用されなくなった理由や、エンド ユーザーが記した誤検知や上書きに関する情報を識別します。|
|PolicyDetails|Collection(Self.[PolicyDetails](#policydetails-complex-type))|はい|DLP イベントをトリガーした 1 つ以上のポリシーに関する情報。|
|SensitiveInfoDetectionIsIncluded|ブール型|はい|ソース コンテンツからの機密性の高いデータ型の値や周囲のコンテキストがイベントに含まれているかどうかを示します。 Azure Active Directory では、機密性の高いデータへのアクセスは「機密情報を含む DLP ポリシー イベントの読み取り」アクセス許可が必要です。|
|||||

### <a name="sharepointmetadata-complex-type"></a>SharePointMetadata 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|接続元|Edm.String|はい|イベントを実行したユーザーの ID。 This will be either the FileOwner, LastModifier, or LastSharer.|
|itemCreationTime|Edm.Date|はい|イベントのログの記録日時に関する UTC の Datetimestamp。|
|SiteCollectionGuid|Edm.Guid|はい|サイト コレクションの GUID。|
|SiteCollectionUrl|Edm.String|はい|SharePoint サイトの名前。|
|FileName|Edm.String|はい|パスの名前。|
|FileOwner|Edm.String|はい|ドキュメントの所有者。|
|FilePathUrl|Edm.String|はい|文書の URL。|
|DocumentLastModifier|Edm.String|はい|最後にドキュメントを変更したユーザー。|
|DocumentSharer|Edm.String|はい|最後にドキュメントの共有を変更したユーザー。|
|UniqueId|Edm.String|はい|ファイルを識別する GUID。|
|LastModifiedTime|Edm.DateTime|はい|ドキュメントの最終更新日時に関する UTC の Timestamp。|
|||||


### <a name="exchangemetadata-complex-type"></a>ExchangeMetadata 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|MessageID|Edm.String|はい|イベントをトリガーした電子メールのメッセージ ID。|
|送信元|Edm.String|はい|電子メールを送信したユーザー。|
|宛先|Collection(Edm.String)|いいえ|メッセージの宛先行にあった電子メール アドレスのコレクション。|
|CC|Collection(Edm.String)|いいえ|メッセージの CC 行にあった電子メール アドレスのコレクション。|
|BCC|Collection(Edm.String)|いいえ|メッセージの BCC 行にあった電子メール アドレスのコレクション。|
|件名|Edm.String|はい|電子メール メッセージの件名。|
|送信日時|Edm.DateTime|はい|電子メールが送信された時の UTC の時間。|
|RecipientCount|Edm.Int32|はい|メッセージの宛先、CC、および BCC の各行に含まれるすべての受信者の合計数。|
|||||

### <a name="policydetails-complex-type"></a>PolicyDetails 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|PolicyId|Edm.Guid|はい|このイベントにおける DLP ポリシーの GUID。|
|PolicyName|Edm.String|はい|このイベントにおける DLP ポリシーのフレンドリ名。|
|ルール|Collection(Self.[Rules](#rules-complex-type))|はい|このイベントと一致したポリシー内のルールに関する情報。|
|||||

### <a name="rules-complex-type"></a>ルール複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|RuleId|Edm.Guid|はい|このイベントにおける DLP ルールの GUID。|
|RuleName|Edm.String|はい|このイベントにおける DLP ルールの フレンドリ名。|
|アクション|Collection(Edm.String)|いいえ|DLP RuleMatch イベントの結果として実行されたアクションのリスト。|
|OverriddenActions|Collection(Edm.String)|いいえ|以前に実行されたものの、DLPRuleUndo イベントによって取り消されたアクションのリスト。 |
|重要度|Edm.String|不要|ルールの重要度 (低、中、高) が一致します。|
|RuleMode|Edm.String|はい|DLP ルールが強制、通知を伴う監査、または監査のみのいずれに設定されているかを示します。|
|ConditionsMatched|Self.[ConditionsMatched](#conditionsmatched-complex-type)|いいえ|このイベントと一致したルールの条件に関する詳細。|
|||||

### <a name="conditionsmatched-complex-type"></a>ConditionsMatched 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|SensitiveInformation|Collection(Self.[SensitiveInformation](#sensitiveinformation-complex-type))|いいえ|検出された機密情報の種類に関する情報。|
|DocumentProperties|Collection(NameValuePair)|いいえ|ルールの一致をトリガーしたドキュメント プロパティに関する情報。|
|OtherConditions|Collection(NameValuePair)|いいえ|一致した他のすべての条件を説明するキーと値の組み合わせリスト。|
|||||

### <a name="sensitiveinformation-complex-type"></a>SensitiveInformation 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|Confidence|Edm.Int|はい|検出と一致したパターンの信頼度。|
|カウント|Edm.Int|はい|検出された機密性の高いインスタンスの数。|
|SensitiveType|Edm.Guid|はい|検出された機密性の高いデータの種類を識別する GUID。|
|SensitiveInformationDetections|Self.SensitiveInformationDetections|いいえ|詳細 (一致した値と一致した値のコンテキスト) のある機密情報データを含むオブジェクトの配列。|
|||||

### <a name="sensitiveinformationdetections-complex-type"></a>SensitiveInformationDetections complex type 
DLP 機密データは、「DLP 機密データの読み取り」アクセス許可が付与されたユーザーが、アクティビティ フィード API でのみ利用できます。 

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|Detections|Collection(Self.Detections)|はい|検出された機密情報の配列。 情報には、値 = 一致した値 ( SSN のクレジットカードの値など) と、コンテキスト = 一致した値を含むソース コンテンツからの抜粋のあるキー値のペアが含まれます。 |
|ResultsTruncated|Edm.Boolean|はい|結果が多いためにログが切り捨てられたかどうかを示します。 |
|||||

### <a name="exceptioninfo-complex-type"></a>ExceptionInfo 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|理由|Edm.String|不要|For a DLPRuleUndo event, this indicates why the rule no longer applies, which can be one of 3 reasons: Override, Document Change, or Policy Change|
|FalsePositive|Edm.Boolean|いいえ|ユーザーが誤検知としてこのイベントを指定したかどうかを示します。|
|妥当性|Edm.String|不要|ユーザーがポリシーを上書きすることにした場合、ユーザーによる指定の妥当性をここで確認できます。|
|ルール|Collection(Edm.Guid)|いいえ|誤検知または上書き、もしくはアクションが取り消されるものとして指定された各ルールの GUID のコレクション。|
|||||

## <a name="security-and-compliance-center-schema"></a>セキュリティ/コンプライアンス センター スキーマ

|**パラメーター**|**型**|**必須**|**説明**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|いいえ|コマンドレットが実行された日付と時刻。|
|ClientRequestId|Edm.String|不要|A GUID that can be used to correlate this cmdlet with the Security & Compliance Center UX operations. This information is only used by Microsoft support.|
|CmdletVersion|Edm.String|不要|実行された時のコマンドレットのビルド バージョン。|
|EffectiveOrganization|Edm.String|不要|The GUID for the organization impacted by the cmdlet. (Deprecated: This parameter will stop appearing in the future.)|
|UserServicePlan|Edm.String|不要|コマンドレットを実行したユーザーに割り当てられる Exchange Online Protection サービス プラン。|
|ClientApplication|Edm.String|いいえ|コマンドレットが (リモート PowerShell とは対照的に) アプリケーションによって実行された場合、このフィールドにはそのアプリケーションの名前が含まれます。|
|パラメーター|Edm.String|不要|個人を特定できる情報を含まないコマンドレットで使用されたパラメーターの名前と値。|
|NonPiiParameters|Edm.String|いいえ|The name and value for parameters that were used with the cmdlet that include Personally Identifiable Information. (Deprecated: This field will stop appearing in the future and its content merged with the Parameters field.)|
|||||

## <a name="security-and-compliance-alerts-schema"></a>セキュリティとコンプライアンスのアラート スキーマ

アラートの通知には、次のものが含まれます。

- [セキュリティ/コンプライアンス センターのアラート ポリシー](https://docs.microsoft.com/office365/securitycompliance/alert-policies#default-alert-policies)に基づいて生成されたすべてのアラート。
- [Office 365 Cloud App Security](https://docs.microsoft.com/office365/securitycompliance/office-365-cas-overview) および [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) で生成された Office 365 関連のアラート。

これらのイベントの UserId と UserKey は、常に SecurityComplianceAlerts になります。 共通スキーマの Operation プロパティの値として格納される 2 種類のアラート通知があります。

- AlertTriggered: 新しいアラートがポリシーとの一致によって生成されている。

- AlertEntityGenerated: 新しいエンティティがアラートに追加されている。 このイベントは、Office 365 セキュリティ/コンプライアンス センターのアラート ポリシーに基づいて生成されたアラートにのみ適用されます。 生成されたアラートごとに、これらのイベントが 1 つまたは複数関連付けられます。 たとえば、いずれかのユーザーが 5 分以内に 100 ファイル以上削除したときに、アラートをトリガーするポリシーが定義されているとします。 2 人のユーザーがほとんど同時にしきい値を超えた場合、AlertEntityGenerated イベントは 2 つになりますが、AlertTriggered イベントは 1 つのみになります。

|**パラメーター**|**型**|**必須**|**Description**|
|:-----|:-----|:-----|:-----|
|AlertId|Edm.Guid|はい|アラートの GUID。|
|AlertType|Self.String|はい|アラートの種類。 アラートの種類には、次のものが含まれます。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>System</p></li><li><p>Custom</p></li>|
|Name|Edm.String|はい|アラートの名前。|
|PolicyId|Edm.Guid|いいえ|アラートをトリガーしたポリシーの GUID。|
|Status|Edm.String|不要|アラートの状態。 状態には、次のものが含まれます。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Active</p></li><li><p>Investigating</p></li><li><p>Resolved</p></li><li><p>Dismissed</p></li></ul>|
|重要度|Edm.String|不要|アラートの重大度。 重大度レベルには、次のものが含まれます。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>低</p></li><li><p>中</p></li><li><p>高</p></li></ul>|
|カテゴリ|Edm.String|不要|アラートのカテゴリ。 カテゴリには、次のものが含まれます。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>DataLossPrevention</p></li><li><p>ThreatManagement</p></li><li><p>DataGovernance</p></li><li><p>AccessGovernance</p></li><li><p>MailFlow</p></li><li><p>Other</p></li></ul>|
|Source|Edm.String|不要|アラートのソース。 ソースには、次のものが含まれます。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Office 365 セキュリティ/コンプライアンス</p></li><li><p>Cloud App Security</p></li></ul>|
|Comments|Edm.String|不要|アラートが表示されたユーザーが残したコメント。 既定は、"New alert" です。|
|Data|Edm.String|不要|アラートまたはアラート エンティティの詳細データ BLOB。|
|AlertEntityId|Edm.String|不要|アラート エンティティの識別子。 このパラメーターは、AlertEntityGenerated イベントにのみ適用されます。|
|EntityType|Edm.String|いいえ|アラートまたはアラート エンティティの種類。 エンティティの種類には、次のものが含まれます。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>User</p></li><li><p>Recipients</p></li><li><p>Sender</p></li><li><p>MalwareFamily</p></li></ul>このパラメーターは、AlertEntityGenerated イベントにのみ適用されます。|
|||||

## <a name="yammer-schema"></a>Yammer スキーマ

「[セキュリティ/コンプライアンス センターで監査ログを検索する](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#yammer-activities)」にリストされている Yammer イベントは、このスキーマを使用します。

|**パラメーター**|**型**|**必須**|**説明**|
|:-----|:-----|:-----|:-----|
|ActorUserId|Edm.String|不要|操作を実行したユーザーの電子メール。|
|ActorYammerUserId|Edm.Int64|いいえ|操作を実行したユーザーの ID。|
|DataExportType|Edm.String|不要|データのエクスポートにメッセージ、メモ、ファイル、トピック、ユーザー、およびグループが含まれている場合は "data" を返します。データのエクスポートにユーザーのみが含まれている場合は "user" を返します。|
|FileId|Edm.Int64|いいえ|操作中のファイルの ID。 |
|FileName|Edm.String|不要|操作中のファイルの名前。 操作に関係のない場合は空白が表示されます。|
|GroupName|Edm.String|不要|操作中のグループの名前。 操作に関係のない場合は空白が表示されます。|
|IsSoftDelete|Edm.Boolean|いいえ|ネットワークのデータ保持ポリシーが論理的な削除に設定されている場合は "true" を返します。ネットワークのデータ保持ポリシーが物理的な削除に設定されている場合は "false" を返します。|
|MessageId|Edm.Int64|いいえ|操作中のメッセージの ID。|
|YammerNetworkId|Edm.Int64|いいえ|操作を実行したユーザーのネットワーク ID。|
|TargetUserId|Edm.String|いいえ|操作中のターゲット ユーザーのメール アドレス。 操作に関係のない場合は空白が表示されます。|
|TargetYammerUserId|Edm.Int64|いいえ|操作中のターゲット ユーザーの ID。|
|VersionId|Edm.Int64|いいえ|操作中のファイルのバージョン ID。|
|||||

## <a name="sway-schema"></a>Sway スキーマ

「[Office 365 プロテクション センターでの監査ログの検索](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&amp;rs=en-US&amp;ad=US)」にリストされている Sway イベント (ファイルおよびフォルダー イベントを除く) は、このスキーマを使用します。

|**パラメーター**|**型**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|ObjectType|Self.[ObjectType](#objecttype)|いいえ|トリガーされたイベントのアクセス ポイント。アクセス ポイントには以下が含まれます。 <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Sway</p></li><li><p>ホスト内に埋め込まれた Sway。</p></li><li><p>Office 365 管理ポータル内の Sway 設定。</p></li></ul>|
|エンドポイント|Self.[Endpoint](#endpoint)|いいえ|トリガーされたイベントの Sway クライアント エンドポイント。Sway クライアント エンドポイントには、Web、iOS、Windows、または Android を使用できます。 |
|BrowserName|Edm.String|不要|トリガーされたイベントの Sway にアクセスするために使用するブラウザー。 |
|DeviceType|Self.[DeviceType](#devicetype)|いいえ|トリガーされたイベントの Sway にアクセスするために使用するデバイスの種類。デバイスの種類は、デスクトップ、モバイル、またはタブレットのいずれかにできます。|
|SwayLookupId|Edm.String|不要|Sway ID。 |
|SiteUrl|Edm.String|不要|Sway の URL。|
|OperationResult|Self.[OperationResult](#operationresult)|いいえ|成功または失敗のいずれか。|
|||||


### <a name="enum-objecttype---type-edmint32"></a>列挙:ObjectType - タイプ: Edm.Int32

#### <a name="objecttype"></a>ObjectType

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Sway|Sway からトリガーされたイベント。|
|1 |SwayEmbedded|ホストに埋め込まれている、Sway からトリガーされたイベント。|
|pbm-2|SwayAdminPortal|イベントは、Office 365 管理ポータルの Sway サービス設定からトリガーされました。|
|||||


### <a name="enum-operationresult---type-edmint32"></a>列挙:OperationResult - タイプ: Edm.Int32

#### <a name="operationresult"></a>OperationResult

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Succeeded|イベントは成功しました。|
|1 |Failed|イベントは失敗しました。|
|||||


### <a name="enum-endpoint---type-edmint32"></a>列挙:Endpoint - タイプ: Edm.Int32

#### <a name="endpoint"></a>Endpoint

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|SwayWeb|Sway の Web クライアントを使用してイベントがトリガーされました。|
|1 |SwayIOS|Sway の iOS クライアントを使用してイベントがトリガーされました。|
|pbm-2|SwayWindows|Sway の Windows クライアントを使用してイベントがトリガーされました。|
|1/3|SwayAndroid|Sway の Android クライアントを使用してイベントがトリガーされました。|
|||||


### <a name="enum-devicetype---type-edmint32"></a>列挙:DeviceType - タイプ: Edm.Int32

#### <a name="devicetype"></a>DeviceType

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Desktop|イベントはデスクトップを使用してトリガーされました。|
|1 |Mobile|イベントはモバイル デバイスを使用してトリガーされました。|
|pbm-2|Tablet|イベントはタブレット デバイスを使用してトリガーされました。|
|||||

### <a name="enum-swayauditoperation---type-edmint32"></a>列挙:SwayAuditOperation - タイプ: Edm.Int32

#### <a name="swayauditoperation"></a>SwayAuditOperation

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|1-d|Create|ユーザーは Sway を作成します。|
|pbm-2|Delete|ユーザーは Sway を削除します。|
|1/3|View|ユーザーは Sway を表示します。|
|4 |Edit|ユーザーは Sway を編集します。|
|5 |Duplicate|ユーザーは Sway を複製します。|
|7 |共有|ユーザーは Sway の共有を開始します。このイベントは、Sway 共有メニュー内で特定の共有先をクリックするユーザー アクションをキャプチャします。イベントでは、ユーザーが実際に共有アクションを最後まで実行して完了させるかどうかは示されません。|
|8 |ChangeShareLevel|ユーザーは Sway の共有のレベルを変更します。このイベントは、ユーザーによる、Sway に関連付けられている共有のスコープの変更をキャプチャします。たとえば、「組織内から」と比較して「パブリック」などへの変更です。|
|9 |RevokeShare|ユーザーは、アクセス権限の取り消しによって、Sway の共有を停止します。アクセス権限を取り消すと、Sway に関連付けられているリンクは変更されます。|
|10  |EnableDuplication|ユーザーは Sway を複製できます (既定ではオン)。|
|#|DisableDuplication|ユーザーは Sway を複製できません (既定ではオフ)。|
|12 |ServiceOn|ユーザーは、Office 365 管理センターを使用して、組織全体で Sway を有効にします (既定ではオン)。|
|スリー|ServiceOff|ユーザーは、Office 365 管理センターを使用して、組織全体で Sway を無効にします (既定ではオフ)。|
|14 |ExternalSharingOn|ユーザーは、Office 365 管理センターを使用して、組織全体で外部共有を有効にします。|
|約|ExternalSharingOff|ユーザーは、Office 365 管理センターを使用して、組織全体で外部共有を無効にします。|
|||||

## <a name="data-center-security-base-schema"></a>データ センター セキュリティ基本スキーマ

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|DataCenterSecurityEventType|Self.[DataCenterSecurityEventType](#datacentersecurityeventtype)|はい|ロック ボックス内のコマンドレット イベントのタイプ。|
|||||

### <a name="enum-datacentersecurityeventtype---type-edmint32"></a>列挙:DataCenterSecurityEventType - タイプ:Edm.Int32

#### <a name="datacentersecurityeventtype"></a>DataCenterSecurityEventType


|**メンバー名**|**説明**|
|:-----|:-----|
|DataCenterSecurityCmdletAuditEvent|これは、コマンドレット監査タイプ イベントの列挙型の値です。|
|||


## <a name="data-center-security-cmdlet-schema"></a>データ センター セキュリティ コマンドレット スキーマ

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|はい|コマンドレット実行の開始時刻。|
|EffectiveOrganization|Edm.String|はい|昇格/コマンドレットの対象とされたテナントの名前。|
|ElevationTime|Edm.Date|はい|イベントの開始時刻。|
|ElevationApprover|Edm.String|はい|Microsoft 管理者の名前。|
|ElevationApprovedTime|Edm.Date|いいえ|昇格が承認されたときのタイムスタンプ。|
|ElevationRequestId|Edm.Guid|はい|昇格要求の一意識別子。|
|ElevationRole|Edm.String|不要|昇格が要求されたロール。|
|ElevationDuration|Edm.Int32|はい|昇格がアクティブであった期間。|
|GenericInfo|Edm.String|いいえ|コメントやその他の一般的な情報に使用されます。|
|||||


## <a name="microsoft-teams-schema"></a>Microsoft Teams スキーマ

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|MessageId|Edm.String|不要|チャットまたはチャネル メッセージの識別子。|
|Members|Collection(Self.[MicrosoftTeamsMember](#microsoftteamsmember-complex-type))|いいえ|チーム内のユーザーの一覧。|
|TeamName|Edm.String|不要|監査対象のチームの名前。|
|TeamGuid|Edm.Guid|いいえ|監査対象のチームの一意識別子。|
|ChannelType|Edm.String|不要|監査対象のチャネルの種類 (標準/プライベート)。　 |
|ChannelName|Edm.String|不要|監査対象のチャネルの名前。|
|ChannelGuid|Edm.Guid|いいえ|監査対象のチャネルの一意識別子。|
|ExtraProperties|Collection(Self.[KeyValuePair](#keyvaluepair-complex-type))|いいえ|追加のプロパティのリスト。|
|AddOnType|Self.[AddOnType](#addontype)|いいえ|このイベントを生成したアドオンの種類。|
|AddonName|Edm.String|不要|イベントを生成したアドオンの名前。|
|AddOnGuid|Edm.Guid|いいえ|イベントを生成したアドオンの一意識別子。|
|TabType|Edm.String|不要|タブ イベントにのみ存在します。 イベントを生成したタブの種類。|
|Name|Edm.String|いいえ|設定のイベントにのみ存在します。 変更された設定の名前。|
|OldValue|Edm.String|いいえ|設定のイベントにのみ存在します。 設定の以前の値。|
|NewValue|Edm.String|いいえ|設定のイベントにのみ存在します。 設定の新しい値。|
||||


### <a name="microsoftteamsmember-complex-type"></a>MicrosoftTeamsMember complex type

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|UPN|Edm.String|不要|ユーザーのユーザー プリンシパル名。|
|Role|Self.[MemberRoleType](#memberroletype)|いいえ|チーム内のユーザーの役割。|
|DisplayName|Edm.String|不要|ユーザーの表示名。|
|||||

### <a name="enum-memberroletype---type-edmint32"></a>列挙値: MemberRoleType - 型: Edm.Int32

#### <a name="memberroletype"></a>MemberRoleType

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Member|チームのメンバーであるユーザー。|
|1 |Owner|チームの所有者であるユーザー。|
|pbm-2|Guest|チームのメンバーでないユーザー。|
||||

### <a name="keyvaluepair-complex-type"></a>KeyValuePair 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|キー|Edm.String|不要|キーと値のペアのキー。|
|値|Edm.String|いいえ|キーと値のペアの値。|
|||||


### <a name="enum-addontype---type-edmint32"></a>列挙型: AddOnType - 型: Edm.Int32

#### <a name="addontype"></a>AddOnType

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|1-d|Bot|Microsoft Teams ボット。|
|pbm-2|Connector|Microsoft Teams コネクタ。|
|1/3|Tab|Microsoft Teams タブ。|
||||

## <a name="office-365-advanced-threat-protection-and-threat-investigation-and-response-schema"></a>Office 365 Advanced Threat Protection および脅威の調査と対応スキーマ

[Office 365 Advanced Threat Protection](https://docs.microsoft.com/office365/securitycompliance/office-365-atp) (ATP) および脅威の調査と対応のイベントは、Office 365 Advanced Threat Protection Plan 1、Office 365 Advanced Threat Protection Plan 2、または E5 サブスクリプションをお持ちの Office 365 のお客様が利用できます。 Office 365 ATP フィードの各イベントは、脅威が含まれていると判断された次のように対応します。

- 配信時および [Zero-hour Auto Purge](https://support.office.com/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15) によってメッセージに対する検出が行われた、組織内のユーザーが送信または受信する電子メール メッセージ。 

- [Office 365 の ATP の安全なリンク](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links)の保護に基づいてクリック時に悪意があるとして検出された組織内のユーザーがクリックした URL。  

- [Office 365 の ATP](https://docs.microsoft.com/office365/securitycompliance/atp-for-spo-odb-and-teams) により悪意があるとして検出された SharePoint Online、OneDrive for Business、または Microsoft Teams 内のファイル。

- トリガーされ、[自動調査](https://docs.microsoft.com/office365/securitycompliance/automated-investigation-response-office)を開始したアラート。

> [!NOTE]
> Office 365 Advanced Threat Protection および Office 365 脅威の調査と対応 (旧称: Office 365 脅威インテリジェンス) の機能は、Office 365 Advanced Threat Protection Plan 2 および追加の脅威保護機能の一部になっています。 詳細については、「[Office 365 ATP のプランと価格](https://products.office.com/exchange/advance-threat-protection)」および「[Office 365 ATP サービスの説明](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description)」を参照してください。

### <a name="email-message-events"></a>電子メール メッセージ イベント

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|AttachmentData|Collection(Self.[AttachmentData](#attachmentdata))|いいえ|イベントをトリガーした電子メール メッセージの添付ファイルに関するデータ。|
|DetectionType|Edm.String|はい|検出タイプ (例: **Inline** - 配信時に検出、**Delayed** - 配布後に検出、**ZAP** - [Zero hour auto purge](https://support.office.com/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15) によって削除されたメッセージ)。 ZAP の検出タイプのイベントの前には、通常、**Delayed** 検出タイプのメッセージが表示されます。|
|DetectionMethod|Edm.String|はい|Office 365 の ATP で検出に使用されるメソッドまたはテクノロジ。|
|InternetMessageId|Edm.String|はい|インターネット メッセージ ID。|
|NetworkMessageId|Edm.String|はい|Exchange Online のネットワーク メッセージ ID。|
|P1Sender|Edm.String|はい|電子メール メッセージの送信者の返信先。|
|P2Sender|Edm.String|はい|電子メール メッセージの送信者。|
|ポリシー|Self.[Policy](#policy-type-and-action-type)|はい|メール メッセージに関連するフィルタリング ポリシーのタイプ (**スパム対策**や**フィッシング対策**など) および関連するアクションタイプ (**高確度スパム**、**スパム**、**フィッシング**など)。|
|ポリシー|Self.[PolicyAction](#policy-action)|はい|メール メッセージに関連するフィルタリング ポリシーで構成されたアクション (たとえば、**迷惑メールフォルダーに移動**または**検疫**)。|
|P2Sender|Edm.String|はい|電子メール メッセージの**送信者**。|
|受信者|Collection(Edm.String)|はい|電子メール メッセージの受信者の配列。|
|SenderIp|Edm.String|はい|Office 365 の電子メールを送信した IP アドレス。 IP アドレスは、IPv4 または IPv6 アドレスの形式で表示されます。|
|件名|Edm.String|はい|メッセージの件名。|
|Verdict|Edm.String|はい|メッセージの判定。|
|MessageTime|Edm.Date|はい|メール メッセージが受信または送信された、協定世界時 (UTC) での日時。|
|EventDeepLink|Edm.String|はい|エクスプローラーのメール イベントまたは Office 365 セキュリティ/コンプライアンス センターのリアルタイム レポートへのディープリンク。|
|||||

### <a name="attachmentdata-complex-type"></a>AttachmentData complex type

#### <a name="attachmentdata"></a>AttachmentData

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|FileName|Edm.String|はい|添付ファイルのファイル名。|
|FileType|Edm.String|はい|添付ファイルのファイルの種類。|
|FileVerdict|Self.[FileVerdict](#fileverdict)|はい|ファイルのマルウェア判定。|
|MalwareFamily|Edm.String|いいえ|ファイルのマルウェア ファミリ。|
|SHA256|Edm.String|はい|ファイルの SHA256 ハッシュ。|
|||||

### <a name="enum-fileverdict---type-edmint32"></a>列挙値: FileVerdict - 型: Edm.Int32

#### <a name="fileverdict"></a>FileVerdict

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Good|脅威は検出されませんでした。|
|1 |Bad|添付ファイルにマルウェアが見つかりました。|
|-1|Error|スキャン/分析のエラー。|
|-2|Timeout|スキャン/分析のタイムアウト。|
|-3|Pending|スキャン/分析が完了していません。|
|||||

### <a name="enum-policy---type-edmint32"></a>列挙値: Policy - 型: Edm.Int32

#### <a name="policy-type-and-action-type"></a>ポリシー タイプおよびアクション タイプ

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|1|スパム対策、HSPM|スパム対策ポリシーの高確度スパム (HSPM) アクション。|
|pbm-2|スパム対策、SPM|スパム対策ポリシーのスパム (SPM) アクション。|
|1/3|スパム対策、バルク|スパム対策ポリシーのバルク アクション。|
|4 |スパム対策、PHSH|スパム対策ポリシーのフィッシング (PHSH) アクション。|
|5 |フィッシング対策、DIMP|フィッシング対策ポリシーのドメイン偽装 (DIMP) アクション。|
|6 |フィッシング対策、UIMP|フィッシング対策ポリシーのユーザー偽装 (UIMP) アクション。|
|7 |フィッシング対策、SPOOF|フィッシング対策ポリシーのスプーフィング アクション。|
|8 |フィッシング対策、GIMP|フィッシング対策ポリシーのメールボックス インテリジェンス アクション。|
|9 |マルウェア対策、AMP| マルウェア対策ポリシーのマルウェア ポリシー アクション。|
|10  |安全な添付ファイル、SAP| Office 365 ATP の安全な添付ファイル ポリシーのポリシー アクション。|
|#|Exchange トランスポート ルール、ETR| Exchange トランスポート ルールのポリシー アクション。|
|12 |マルウェア対策、ZAPM| ゼロアワー自動消去 (ZAP) に適用されるマルウェア対策ポリシーのマルウェア対策ポリシー アクション。|
|スリー|フィッシング対策、ZAPP| ZAP に適用されるフィッシング対策のフィッシング詐欺ポリシー アクション。|
|14 |フィッシング対策、ZAPS| ZAP に適用されるスパム対策 ポリシーの迷惑メール ポリシー アクション。|
|約|スパム対策、高確度フィッシング メール (HPHISH)|スパム対策ポリシーの高確度フィッシング ポリシー アクション。|
|17 |スパム対策、送信スパム ポリシー (OSPM)|スパム対策の送信スパム フィルター ポリシーのポリシー アクション。|
||||

### <a name="enum-policyaction---type-edmint32"></a>列挙値: PolicyAction - 型: Edm.Int32

#### <a name="policy-action"></a>ポリシー アクション

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|MoveToJMF|迷惑メールフォルダーに移動するポリシー アクション。|
|1 |AddXHeader|メール メッセージに X-header を追加するポリシー アクション。|
|pbm-2|ModifySubject|フィルタリング ポリシーで指定された情報でメール メッセージの件名を変更するポリシー アクション。|
|1/3|Redirect|フィルタリング ポリシーで指定されたメール アドレスにメール メッセージをリダイレクトするポリシー アクション。|
|4 |Delete|メール メッセージを削除 (ドロップ) するポリシー アクション。|
|5 |Quarantine|メール メッセージを隔離するポリシー アクション。|
|6 |NoAction| メール メッセージに対してアクションを実行しないように構成されたポリシー。|
|7 |BccMessage|フィルタリング ポリシーで指定されたメール アドレスにメール メッセージを Bcc するポリシー アクション。|
|8 |ReplaceAttachment|ポリシーアクションとは、フィルタリング ポリシーで指定されたメールメッセージの添付ファイルを置き換えることです。|
||||

### <a name="url-time-of-click-events"></a>URL time-of-click イベント

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|UserId|Edm.String|はい|URL をクリックしたユーザーの識別子 (例: 電子メール アドレス)。|
|AppName|Edm.String|はい|URL がクリックされた Office 365 サービス (例: Outlook メール)。|
|URLClickAction|Self.[URLClickAction](#urlclickaction)|はい|[Office 365 ATP の安全なリンク](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links)に関する組織のポリシーに基づいた、URL のクリック アクション。|
|SourceId|Edm.String|はい|URL がクリックされた Office 365 サービスの識別子 (例: メールの場合、これは Exchange Online のネットワーク メッセージ ID)。|
|TimeOfClick|Edm.Date|はい|ユーザーが URL をクリックした、世界協定時刻 (UTC) での日時。|
|URL|Edm.String|はい|ユーザーがクリックした URL。|
|UserIp|Edm.String|はい|URL をクリックしたユーザーの IP アドレス。 IP アドレスは、IPv4 または IPv6 アドレスの形式で表示されます。|
|||||

### <a name="enum-urlclickaction---type-edmint32"></a>列挙値: URLClickAction - タイプ: Edm.Int32

#### <a name="urlclickaction"></a>URLClickAction

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|pbm-2|Blockpage|[Office 365 の ATP の安全なリンク機能](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links)により、ユーザーが URL に移動することがブロックされました。|
|1/3|PendingDetonationPage|[Office 365 の ATP の安全なリンク機能](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links)により、ユーザーに分析保留中のページが表示されました。|
|4 |BlockPageOverride|[Office 365 の ATP の安全なリンク機能](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links)により、ユーザーが URL に移動することがブロックされましたが、ユーザーは URL に移動するためにブロックをオーバーライドしました。|
|5 |PendingDetonationPageOverride|[Office 365 の ATP の安全なリンク機能](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links)により、ユーザーに分析保留中のページが表示されましたが、ユーザーは URL に移動するためにオーバーライドしました。|
|||||


### <a name="file-events"></a>ファイルのイベント

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|FileData|Self.[FileData](#filedata)|はい|イベントをトリガーしたファイルに関するデータ。|
|SourceWorkload|Self.[SourceWorkload](#sourceworkload)|はい|ファイルが見つかったワークロードやサービス (例: SharePoint Online、OneDrive for Business、Microsoft Teams など)
|DetectionMethod|Edm.String|はい|Office 365 の ATP で検出に使用されるメソッドまたはテクノロジ。|
|LastModifiedDate|Edm.Date|はい|ファイルが作成または最後に変更された、世界協定時刻 (UTC) での日時。|
|LastModifiedBy|Edm.String|はい|ファイルを作成または最後に変更したユーザーの識別子 (例: メール アドレス)。|
|EventDeepLink|Edm.String|はい|エクスプローラーのファイル イベントまたはセキュリティ/コンプライアンス センターのリアルタイム レポートへのディープリンク。|
|||||

### <a name="filedata-complex-type"></a>FileData 複合型

#### <a name="filedata"></a>FileData

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|DocumentId|Edm.String|はい|SharePoint、OneDrive、または Microsoft Teams のファイルの一意の識別子。|
|FileName|Edm.String|はい|イベントをトリガーしたファイルの名前。|
|FilePath|Edm.String|はい|SharePoint、OneDrive、または Microsoft Teams のファイルへのパス (場所)。|
|FileVerdict|Self.[FileVerdict](#fileverdict)|はい|ファイルのマルウェア判定。|
|MalwareFamily|Edm.String|いいえ|ファイルのマルウェア ファミリ。|
|SHA256|Edm.String|はい|ファイルの SHA256 ハッシュ。|
|FileSize|Edm.String|はい|ファイルのサイズ (バイト単位)。|
|||||

### <a name="enum-sourceworkload---type-edmint32"></a>列挙値: SourceWorkload - タイプ: Edm.Int32

#### <a name="sourceworkload"></a>SourceWorkload

|**値**|**メンバー名**|
|:-----|:-----|
|.0|SharePoint Online|
|1 |OneDrive for Business|
|pbm-2|Microsoft Teams|
|||||

## <a name="automated-investigation-and-response-events-in-office-365"></a>Office 365 の自動調査および対応イベント

[Office 365 の自動調査および応答 (AIR)](https://docs.microsoft.com/office365/securitycompliance/automated-investigation-response-office) イベントは、Office 365 Advanced Threat Protection Plan 2、または Office 365 E5 を含むサブスクリプションをお持ちの Office 365 のお客様が利用できます。 調査イベントは調査ステータスの変更に基づいてログに記録されます。 たとえば、管理者が [保留中のアクション] の調査ステータスを [完了] に変更する操作を行うと、イベントがログに記録されます。 

現在のところ、自動調査のみがログに記録されます (手動で生成された調査のイベントは間もなく発生します)。次のステータス値がログに記録されます。

- 調査の開始
- 脅威は検出されませんでした 
- システムにより終了
- 保留中のアクション 
- 脅威が検出されました 
- 修復済み 
- 失敗 
- スロットルで終了 
- ユーザーにより終了
- 実行中

### <a name="main-investigation-schema"></a>主要な調査スキーマ 

|名前    |種類    |説明  |
|----|----|----|
|InvestigationId    |Edm.String    |調査 ID/GUID |
|InvestigationName    |Edm.String    |調査名 |
|InvestigationType    |Edm.String    |調査の種類。 次のいずれかの値を指定できます。<br/>- ユーザーが報告したメッセージ<br/>- zapped マルウェア<br/>- zapped フィッシング<br/>- URL の判定変更<p>(現在手動調査は利用できません。まもなく提供開始予定です) |
|LastUpdateTimeUtc    |Edm.Date    |調査の最終更新の UTC 時刻 |
|StartTimeUtc    |Edm.Date    |調査の開始時刻 |
|状態     |Edm.String     |調査、実行中、保留中のアクションなどの状態。 |
|DeeplinkURL    |Edm.String    |Office 365 セキュリティ/コンプライアンス センターの調査へのディープ リンク URL |
|アクション |Collection (Edm.String)    |調査により推奨される操作のコレクション |
|データ    |Edm.String    |調査エンティティの詳細、調査に関連するアラートの情報が含まれているデータ文字列。 エンティティはデータ blob 内の個別のノードで使用できます。 |
||||

### <a name="actions"></a>Actions

|Field    |種類    |説明 |
|----|----|----|
|ID     |Edm.String    |操作 ID|
|ActionType    |Edm.String    |操作の種類 (メールの修復など) |
|ActionStatus    |Edm.String    |値は次のとおりです。 <br/>- 保留中<br/>- 実行中<br/>- リソースの待機中<br/>- 完了<br/>- 失敗 |
|ApprovedBy    |Edm.String    |自動承認された場合は null 値、それ以外の場合はユーザー名または ID (まもなく対応予定) |
|TimestampUtc    |Edm.DateTime    |操作ステータス変更のタイムスタンプ |
|ActionId    |Edm.String    |操作の一意の識別子 |
|InvestigationId    |Edm.String    |調査の一意の識別子 |
|RelatedAlertIds    |Collection(Edm.String)    |調査に関連するアラート |
|StartTimeUtc    |Edm.DateTime    |操作作成のタイムスタンプ |
|EndTimeUtc    |Edm.DateTime    |操作の最終ステータス更新のタイムスタンプ |
|リソース識別子     |Edm.String     |Azure Active Directory のテナント ID で構成されます。|
|Entities    |Collection(Edm.String)    |操作によって影響を受ける複数のエンティティのリスト |
|関連するアラート ID    |Edm.String    |調査に関連するアラート |
||||

### <a name="entities"></a>Entities

#### <a name="mailmessage-email"></a>MailMessage (電子メール) 

|Field    |種類    |説明  |
|----|----|----|
|Type    |Edm.String    |"mail-message"  |
|Files    |Collection (Self.File) |このメッセージの添付ファイルのファイルに関する詳細 |
|Recipient    |Edm.String    |メール メッセージの受信者 |
|Urls    |Collection(Self.URL) |このメール メッセージに含まれている URL  |
|Sender    |Edm.String    |送信者の電子メール アドレス  |
|SenderIP    |Edm.String    |送信者の IP アドレス  |
|ReceivedDate    |Edm.DateTime    |このメッセージの受信日  |
|NetworkMessageId    |Edm.Guid     |このメール メッセージのネットワーク メッセージ ID  |
|InternetMessageId    |Edm.String  |このメール メッセージのインターネット メッセージ ID |
|件名    |Edm.String    |このメール メッセージの件名  |
||||

#### <a name="ip"></a>IP

|Field    |種類    |説明  |
|----|----|----|
|Type    |Edm.String    |"ip" |
|Address    |Edm.String    |文字列としての IP アドレス (`127.0.0.1` など)
||||

#### <a name="url"></a>URL

|Field    |種類    |説明  |
|----|----|----|
|Type    |Edm.String    |"url" |
|Url    |Edm.String    |エンティティが指す完全な URL  |
||||

#### <a name="mailbox-also-equivalent-to-the-user"></a>Mailbox (ユーザーにも相当) 

|Field    |種類    |説明 |
|----|----|----|
|Type    |Edm.String    |"mailbox"  |
|MailboxPrimaryAddress    |Edm.String    |メールボックスのプライマリ アドレス  |
|DisplayName    |Edm.String    |メールボックスの表示名 |
|Upn    |Edm.String    |メールボックスの UPN  |
||||

#### <a name="file"></a>File

|Field    |種類    |説明  |
|----|----|----|
|Type    |Edm.String    |"file" |
|Name    |Edm.String    |パスのないファイル名 |
FileHashes |Collection (Edm.String)    |ファイルに関連付けられているファイル ハッシュ |
||||

#### <a name="filehash"></a>FileHash

|Field    |種類    |説明 |
|----|----|----|
|Type    |Edm.String    |"filehash" |
|Algorithm    |Edm.String    |ハッシュ アルゴリズムの種類は、次のいずれかの値になります。<br/>- Unknown<br/>- MD5<br/>- SHA1<br/>- SHA256<br/>- SHA256AC
|Value    |Edm.String    |ハッシュ値  |
||||

#### <a name="mailcluster"></a>MailCluster

|Field    |種類    |説明   |
|----|----|----|
|Type    |Edm.String    |"MailCluster" <br/>討議されているエンティティの種類を決定する |
|NetworkMessageIds    |Collection (Edm.String)    |メール クラスターに含まれているメール メッセージの ID のリスト |
|CountByDeliveryStatus    |Collections (Edm.String)    |DeliveryStatus の文字列表現によるメール メッセージの数 |
|CountByThreatType    |Collections (Edm.String) |ThreatType の文字列表現によるメール メッセージの数 |
|Threats    |Collections (Edm.String)    |メール クラスターに含まれているメール メッセージの脅威。 脅威にはフィッシングやマルウェアなどの値が含まれます。 |
|Query    |Edm.String    |メール クラスターのメッセージを特定するために使用されたクエリ  |
|QueryTime    |Edm.DateTime    |クエリ時間  |
|MailCount    |Edm.int    |メール クラスターに含まれているメール メッセージの数。  |
|ソース    |String    |メール クラスターのソース、クラスター ソースの値。 |
||||

## <a name="hygiene-events-schema"></a>検疫イベントスキーマ

検疫イベントは、送信スパム保護に関連しています。 これらのイベントは、電子メールの送信が制限されているユーザーに関連しています。 詳細については、以下を参照してください。

- [送信スパム保護](https://docs.microsoft.com/microsoft-365/security/office-365-security/outbound-spam-controls)

- [Office 365 の制限されたユーザー ポータルから、ブロックされたユーザーを削除する](https://docs.microsoft.com/microsoft-365/security/office-365-security/removing-user-from-restricted-users-portal-after-spam)

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|監査|Edm.String|いいえ|検疫イベントに関連するシステム情報。|
|イベント|Edm.String|いいえ|検疫イベントの種類。 このパラメーターの値は、**リスト**または**Delisted**です。|
|EventId|Edm.Int64|いいえ|検疫イベントの種類の ID。|
|EventValue|Edm.String|いいえ|影響を受けたユーザー。|
|理由|Edm.String|いいえ|検疫イベントに関する詳細。|
|||||

## <a name="power-bi-schema"></a>Power BI スキーマ

「[Office 365 プロテクション センターでの監査ログの検索](/power-bi/service-admin-auditing#activities-audited-by-power-bi)」にリストされている Power BI イベントは、このスキーマを使用します。

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
| AppName               | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | イベントが発生したアプリの名前です。 |
| DashboardName         | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | イベントが発生したダッシュ ボードの名前です。 |
| DataClassification    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | イベントが発生したダッシュボードの[データの分類](/power-bi/service-data-classification) (存在する場合)。 |
| DatasetName           | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | イベントが発生したデータセットの名前です。 |
| MembershipInformation | Collection([MembershipInformationType](#membershipinformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  いいえ  | グループのメンバーシップ情報。 |
| OrgAppPermission      | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | 組織のアプリのアクセス許可の一覧 (組織全体、特定のユーザー、特定のグループ)。 |
| ReportName            | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | イベントが発生したレポートの名前です。 |
| SharingInformation    | Collection([SharingInformationType](#sharinginformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"    |  いいえ  | 共有の招待を送るユーザーについての情報。 |
| SwitchState           | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | さまざまなテナント レベル切り替えの状態についての情報。 |
| WorkSpaceName         | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  いいえ  | イベントが発生したワークスペースの名前です。 |
|||||

### <a name="membershipinformationtype-complex-type"></a>MembershipInformationType 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
| MemberEmail | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  いいえ  | グループの電子メール アドレス。 |
| 状態      | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  いいえ  | 現在、入力されていません。 |
|||||

### <a name="sharinginformationtype-complex-type"></a>SharingInformationType 複合型

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
| RecipientEmail    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  いいえ  | 共有の招待の受信者の電子メール アドレス。 |
| RecipientName    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  いいえ  | 共有の招待の受信者の名前。 |
| ResharePermission | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  いいえ  | 受信者にアクセス許可が付与されています。 |
|||||

## <a name="dynamics-365-schema"></a>Dynamics 365 スキーマ

Dynamics 365 イベントのモデル駆動型アプリに関連するイベントの監査レコードは、基本操作スキーマとエンティティ操作スキーマの両方を使用します。 詳細については、「 [Enable and Use Activity Logging](https://docs.microsoft.com/power-platform/admin/enable-use-comprehensive-auditing#model-driven-apps-in-dynamics-365-schema)」を参照してください。

### <a name="dynamics-365-base-schema"></a>Dynamics 365 基本スキーマ

| **パラメーター**     | **Type**            | **必須かどうか?** | **説明**|
|:------------------ | :------------------ | :--------------|:--------------|
|CrmOrganizationUniqueName|Edm.String|はい|組織の一意の名前。|
|InstanceUrl|Edm.String|はい|インスタンスへの URL。|
|ItemUrl|Edm.String|不要|ログを出力するレコードの URL。|
|ItemType|Edm.String|不要|エンティティの naame。|
|UserAgent|Edm.String|不要|組織内のユーザー GUID の一意の識別子。|
|フィールド|Collection(Common.NameValuePair)|いいえ|作成または更新されたプロパティキーと値のペアを含む JSON オブジェクト。|
|||||

### <a name="dynamics-365-entity-operation-schema"></a>Dynamics 365 エンティティ操作スキーマ

Dynamics 365 のモデル駆動型アプリからのエンティティイベントこのスキーマを使用して Dynamics 365 基本スキーマを構築します。 このスキーマには、監査対象イベントを発生させたエンティティ操作に関する情報が含まれています。

| **パラメーター**     | **Type**            | **必須かどうか?** | **説明**|
|:------------------ | :------------------ | :--------------|:--------------|
|EntityId|Edm.Guid|いいえ|エンティティの一意識別子。|
|EntityName|Edm.String|はい|組織内のエンティティの名前。 エンティティの例 `contact` として、またはがあり `authentication` ます。|
|メッセージ|Edm.String|はい|このパラメーターには、エンティティに関連して実行された操作が含まれます。 たとえば、新しい連絡先が作成された場合、Message プロパティの値は `Create` となり、EntityName プロパティの対応する値はに `contact` なります。|
|Query|Edm.String|不要|FetchXML 操作の実行中に使用されたフィルタークエリのパラメーター。|
|PrimaryFieldValue|Edm.String|不要|エンティティのプライマリフィールドである属性の値を示します。|
|||||

## <a name="workplace-analytics-schema"></a>Workplace Analytics スキーマ

「[Office 365 セキュリティ/コンプライアンス センターでの監査ログの検索](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-workplace-analytics-activities)」にリストされている WorkPlace Analytics イベントは、このスキーマを使用します。

| **パラメーター**     | **Type**            | **必須かどうか?** | **説明**|
|:------------------ | :------------------ | :--------------|:--------------|
| WpaUserRole        | Edm.String | 不要     | アクションを実行したユーザーの Workplace Analytics ロール。|
| ModifiedProperties | コレクション (Common.ModifiedProperty) | いいえ | このプロパティには、変更されたプロパティの名前、変更されたプロパティの新しい値、および変更されたプロパティの以前の値が含まれています。|
| OperationDetails   | コレクション (Common.NameValuePair)    | いいえ | 変更された設定の拡張プロパティの一覧。 各プロパティには **Name** と **Value** があります。|
||||

## <a name="quarantine-schema"></a>検疫スキーマ

「[Office 365 セキュリティ/コンプライアンス センターでの監査ログの検索](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#quarantine-activities)」に記載されている検疫イベントは、このスキーマを使用します。 検疫の詳細については、「[Office 365 の検疫](https://docs.microsoft.com/microsoft-365/security/office-365-security/quarantine-email-messages)」を参照してください。

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|RequestType|Self.[RequestType](#enum-requesttype---type-edmint32)|いいえ|ユーザーによって実行された検疫要求の型。|
|RequestSource|Self.[RequestSource](#enum-requestsource---type-edmint32)|いいえ|検疫要求のソースは、セキュリティ/コンプライアンス センター (SCC)、コマンドレット、URLlink に由来する場合があります。|
|NetworkMessageId|Edm.String|いいえ|検疫されたメール メッセージのネットワーク メッセージ ID。|
|ReleaseTo|Edm.String|いいえ|メール メッセージの受信者。|
|||||

### <a name="enum-requesttype---type-edmint32"></a>Enum: RequestType - Type: Edm.Int32

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|Preview|これは、有害と見なされるメール メッセージをプレビューするように求める、ユーザーからの要求です。|
|1 |Delete|これは、有害と見なされるメール メッセージを削除するように求める、ユーザーからの要求です。|
|pbm-2|Release|これは、有害と見なされるメール メッセージを解放するように求める、ユーザーからの要求です。|
|1/3|Export|これは、有害と見なされるメール メッセージをエクスポートするように求める、ユーザーからの要求です。|
|4 |ViewHeader|これは、有害と見なされるメール メッセージのヘッダーを表示するように求める、ユーザーからの要求です。|
||||

### <a name="enum-requestsource---type-edmint32"></a>Enum: RequestSource - Type: Edm.Int32

|**値**|**メンバー名**|**説明**|
|:-----|:-----|:-----|
|.0|SCC|セキュリティ/コンプライアンス センター (SCC) が、有害な可能性のあるメール メッセージのプレビュー、削除、解放、エクスポート、ヘッダーの表示を求めるユーザーからの要求の発生元になりうるソースです。 |
|1 |コマンドレット|コマンドレットが、有害な可能性のあるメール メッセージのプレビュー、削除、解放、エクスポート、ヘッダーの表示を求めるユーザーからの要求の発生元になりうるソースです。|
|pbm-2|URLlink|これが、有害な可能性のあるメール メッセージのプレビュー、削除、解放、エクスポート、ヘッダーの表示を求めるユーザーからの要求の発生元になりうるソースです。|
||||

## <a name="microsoft-forms-schema"></a>Microsoft Forms スキーマ

「[Office 365 セキュリティ/コンプライアンス センターでの監査ログの検索](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-forms-activities)」に記載されている Micorosft Forms イベントは、このスキーマを使用します。

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|FormsUserTypes|Collection(Self.[FormsUserTypes](#formsusertypes))|はい|アクションを実行するユーザーの役割。  このパラメーターの値は、管理者、所有者、レスポンダー、または共同編集者です。|
|SourceApp|Edm.String|はい|アクションが Forms Web サイトからのものなのか、他のアプリからのものなのかを示します。|
|FormName|Edm.String|いいえ|現在のフォームの名前。|
|FormId |Edm.String|いいえ|対象フォームの ID。|
|FormTypes|Collection(Self.[FormTypes](#formtypes))|いいえ|これが、フォーム、クイズ、またはアンケートなのかを示します。|
|ActivityParameters|Edm.String|いいえ|アクティビティのパラメーターを含む JSON 文字列。 詳細については、「[Office 365 セキュリティ/コンプライアンス センターで監査ログを検索する](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#microsoft-forms-activities)」を参照してください。|
||||

### <a name="enum-formsusertypes---type-edmint32"></a>Enum: FormsUserTypes - Type: Edm.Int32

#### <a name="formsusertypes"></a>FormsUserTypes

|**値**|**フォーム ユーザーの種類**|**説明**|
|:-----|:-----|:-----|
|.0|管理者|フォームにアクセスできる管理者。|
|1 |Owner|フォームの所有者であるユーザー。|
|pbm-2|レスポンダー|フォームに応答を送信したユーザー。|
|1/3|共同編集者|フォームの所有者から提供された、フォームにログインして編集するための共同編集者リンクを使用したユーザー。|
||||

### <a name="enum-formtypes---type-edmint32"></a>Enum: FormTypes - Type: Edm.Int32

#### <a name="formtypes"></a>FormTypes

|**値**|**フォームの種類**|**説明**|
|:-----|:-----|:-----|
|.0|フォーム|[新しいフォーム] オプションを使用して作成されたフォーム。|
|1 |クイズ|[新しいクイズ] オプションを使用して作成されたクイズ。  クイズは特殊な種類のフォームで、点数、自動および手動採点、コメントなどの追加の機能が含まれるフォームです。|
|pbm-2|アンケート|[新しいアンケート] オプションを使用して作成されたアンケート。  アンケートは特殊な種類のフォームで、CMS 統合や Flow ルールのサポートなどの追加の機能が含まれるフォームです。|
||||

## <a name="mip-label-schema"></a>MIP ラベルのスキーマ

Microsoft Information Protection (MIP) ラベルのスキーマのイベントは、秘密度ラベルが適用されているトランスポート パイプラインのエージェントによって処理されたメール メッセージを Microsoft 365 が検出したときにトリガーされます。 秘密度ラベルは、手動または自動で、トランスポート パイプラインの内部または外部で適用されます。 秘密度ラベルは、ラベル ポリシーの自動適用により、メール メッセージに自動的に適用できます。

この監査スキーマの目的は、秘密度ラベルが適用されているすべてのメール アクティビティの合計を示すことです。 そのため、秘密度ラベルがいつどのように適用されたかに関係なく、秘密度ラベルが適用されている組織内のユーザー間で送受信されるメール メッセージごとに、監査のアクティビティが記録されます。 秘密度ラベルの詳細については、以下をご覧ください。

- [秘密度ラベルの詳細](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)

- [秘密度ラベルをコンテンツに自動的に適用する](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)

|**パラメーター**|**Type**|**必須かどうか?**|**説明**|
|:-----|:-----|:-----|:-----|
|Sender|Edm.String|不要|メール メッセージの差出人フィールドのメール アドレス。|
|Receivers|Collection(Edm.String)|いいえ|メール メッセージの [宛先]、[CC]、[BCC] フィールドにあるすべてのメール アドレス。|
|ItemName|Edm.String|不要|メール メッセージの件名フィールドの文字列。|
|LabelId|Edm.Guid|いいえ|メール メッセージに適用される秘密度ラベルの GUID。|
|LabelName|Edm.String|不要|メール メッセージに適用される秘密度ラベルの名前。|
|LabelAction|Edm.String|不要|メッセージがメールのトランスポート パイプラインに入る前にメール メッセージに適用された秘密度ラベルによって指定されたアクション。|
|LabelAppliedDateTime|Edm.Date|いいえ|メール メッセージに秘密度ラベルが適用された日付。|
|ApplicationMode|Edm.String|いいえ|メール メッセージに秘密度ラベルが適用された方法を指定します。 **Privileged** の値は、ラベルがユーザーによって手動で適用されたことを示します。 **Standard** の値は、ラベルがクライアント側またはサービス側のラベル付けのプロセスによって自動的に適用されたことを示します。|
|||||

## <a name="communication-compliance-exchange-schema"></a>通信コンプライアンス Exchange スキーマ

Office 365 監査ログに記載されている通信コンプライアンスイベントは、このスキーマを使用します。 これには、電子メールメッセージのコンテンツに、一致精度 = 99.5% のスパム対策モデルによって識別される不快な言語が含まれている場合に生成される**SupervisoryReviewOLAudit**操作の監査レコードが含まれてい \> ます。

|**パラメーター**  |**Type**|**必須かどうか?** |**説明**|
|:---------------|:-------|:--------------|:--------------|
| ExchangeDetails |[ExchangeDetails](#exchangedetails)|いいえ|SupervisoryReviewOLAudit イベントを発生させた電子メールメッセージのプロパティ。|
|||||

### <a name="enum-exchangedetails---type-exchangedetails"></a>列挙: ExchangeDetails-Type: ExchangeDetails

#### <a name="exchangedetails"></a>ExchangeDetails

| **メンバー名**   | **型**| **説明**|
|:----------------- | :-------|:---------------|
| NetworkMessageId  |Edm.Guid|電子メールメッセージのネットワークメッセージ ID。|
| InternetMessageId |Edm.String|電子メールメッセージのインターネットメッセージ ID。|
| AttachmentData|コレクション ([Attachmentdetails](#attachmentdetails))|電子メールメッセージに添付されたファイルに関する情報。|
| 受信者|Collection(Edm.String)|電子メールメッセージの [宛先]、[Cc]、および [Bcc] フィールドの電子メールアドレス。 |
| 件名|Edm.String|電子メールメッセージの [件名] フィールドのテキスト。|
| MessageTime|Edm.Date|電子メールメッセージが送信された日付と時刻。|
| 送信元| Edm.String|メール メッセージの差出人フィールドのメール アドレス。|
| 方向性|Edm.String|電子メールメッセージの発信元の状態。|
||||

### <a name="enum-attachmentdetails---type-edmint32"></a>Enum: AttachmentDetails-Type: Edm

#### <a name="attachmentdetails"></a>AttachmentDetails

| **メンバー名** | **型**   | **説明**|
|:--------------- |:---------- | :--------------|
| FileName        | Edm.String | 電子メールメッセージに添付されたファイルの名前。|
| FileType        | Edm.String | 電子メールメッセージに添付されたファイルのファイル拡張子。|
| SHA256          | Edm.String | 電子メールメッセージに添付されたファイルの SHA 256 ハッシュ。|
||||