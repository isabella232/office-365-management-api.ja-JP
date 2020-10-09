---
ms.technology: o365-service-communications
ms.TocTitle: Get started with Office 365 Management APIs
title: Office 365 Management API の使用を開始する
description: この API では、Azure AD を使用してサービスへのアクセス権をアプリケーションに付与するための認証サービスを提供します。
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: d11644a4a9985096c14ad4ae265471159243b65b
ms.sourcegitcommit: ec60dbd5990cfc61b8c000b423e7ade25fa613a8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397448"
---
# <a name="get-started-with-office-365-management-apis"></a><span data-ttu-id="5398d-103">Office 365 Management API の使用を開始する</span><span class="sxs-lookup"><span data-stu-id="5398d-103">Get started with Office 365 Management APIs</span></span>

<span data-ttu-id="5398d-p101">Office 365 Management API と同じようにセキュリティで保護されたサービスへのアクセスを必要とするアプリケーションを作成するときは、アプリケーションがサービスへのアクセス権を保持しているかを確認する方法をサービスに提供する必要があります。Office 365 Management API では、Azure AD を使用してサービスへのアクセス権をアプリケーションに付与するための認証サービスを提供します。</span><span class="sxs-lookup"><span data-stu-id="5398d-p101">When you create an application that needs access to secured services like the Office 365 Management APIs, you need to provide a way to let the service know if your application has rights to access it. The Office 365 Management APIs use Azure AD to provide authentication services that you can use to grant rights for your application to access them.</span></span> 

<span data-ttu-id="5398d-106">以下の 4 つの手順があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-106">There are four key steps:</span></span>

1. <span data-ttu-id="5398d-p102">**Azure AD でアプリケーションを登録する**。アプリケーションが Office 365 Management API にアクセスできるようにするには、アプリケーションを Azure AD に登録する必要があります。これにより、アプリケーションの ID を設定して、API へのアクセスに必要なアクセス許可レベルを指定できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5398d-p102">**Register your application in Azure AD**. To allow your application access to the Office 365 Management APIs, you need to register your application in Azure AD. This allows you to establish an identity for your application and specify the permission levels it needs to access the APIs.</span></span>
    
2. <span data-ttu-id="5398d-p103">**Office 365 テナント管理者の同意を得る**。Office 365 Management API を使用してアプリケーションがテナントのデータにアクセスする許可への同意を、Office 365 テナント管理者が明示的に付与する必要があります。同意プロセスでは、テナント管理者がブラウザーを操作して **Azure AD の同意 UI** にサインインし、アプリケーションが要求するアクセス許可を確認して要求を許可または拒否します。同意が与えられると、UI は認証コードを含めた URL を使用してユーザーをアプリケーションにリダイレクトします。アプリケーションは Azure AD にサービス間の呼び出しを行い、この認証コードをテナント管理者とアプリケーションの両方に関する情報が含まれているアクセス トークンと交換します。テナント ID はアクセス トークンから抽出して、将来使用するために格納しておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-p103">**Get Office 365 tenant admin consent**. An Office 365 tenant admin must explicitly grant consent to allow your application to access their tenant data by means of the Office 365 Management APIs. The consent process is a browser-based experience that requires the tenant admin to sign in to the **Azure AD consent UI** and review the access permissions that your application is requesting, and then either grant or deny the request. After consent is granted, the UI redirects the user back to your application with an authorization code in the URL. Your application makes a service-to-service call to Azure AD to exchange this authorization code for an access token, which contains information about both the tenant admin and your application. The tenant ID must be extracted from the access token and stored for future use.</span></span>
    
3. <span data-ttu-id="5398d-p104">**Azure AD からアクセス トークンを要求する**。Azure AD で設定されているアプリケーションの資格情報を使用すると、アプリケーションは、テナント管理者の追加の操作を必要とすることなく、継続的に同意済みのテナントの追加のアクセス トークンを要求します。これらのアクセス トークンはテナント管理者に関する情報が含まれていないため、アプリ専用トークンと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p104">**Request access tokens from Azure AD**. Using your application's credentials as configured in Azure AD, your application requests additional access tokens for a consented tenant on an ongoing basis, without the need for further tenant admin interaction. These access tokens are called app-only tokens because they do not include information about the tenant admin.</span></span>
    
4. <span data-ttu-id="5398d-p105">**Office 365 Management API の呼び出し**。アプリケーションを認証して承認するため、アプリ専用アクセス トークンが Office 365 Management API に渡されます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p105">**Call the Office 365 Management APIs**. The app-only access tokens are passed to the Office 365 Management APIs to authenticate and authorize your application.</span></span>
    
<span data-ttu-id="5398d-121">次の図は、同意とアクセス トークンの要求のシーケンスを示しています。</span><span class="sxs-lookup"><span data-stu-id="5398d-121">The following diagram shows the sequence of consent and access token requests.</span></span>

![管理 API が承認フローを開始する](images/authorization-flow.png)

> [!IMPORTANT]
> <span data-ttu-id="5398d-123">Office 365 管理アクティビティ API を介してデータにアクセスする前に、Office 365 組織の統合監査ログを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-123">Before you can access data through the Office 365 Management Activity API, you must enable unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="5398d-124">これを実行するには、Office 365 監査ログをオンにします。</span><span class="sxs-lookup"><span data-stu-id="5398d-124">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="5398d-125">手順については、「[Office 365 監査ログの検索を有効または無効にする](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5398d-125">For instructions, see [Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span></span> <br/><br/><span data-ttu-id="5398d-126">Office 365 サービス通信 API のみを使用している場合は、統合監査ログを有効にする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="5398d-126">Enabling unified audit logging isn't required if you're only using the Office 365 Service Communications API.</span></span>

## <a name="register-your-application-in-azure-ad"></a><span data-ttu-id="5398d-127">Azure AD でアプリケーションを登録する</span><span class="sxs-lookup"><span data-stu-id="5398d-127">Register your application in Azure AD</span></span>

<span data-ttu-id="5398d-p107">Office 365 Management API は、Office 365 テナント データに対し、Azure AD を使用してセキュリティ保護された認証を行います。Office 365 Management API にアクセスするには、アプリを Azure AD で登録する必要があり、構成の一部としてアプリが API にアクセスするために必要なアクセス許可レベルを指定します。</span><span class="sxs-lookup"><span data-stu-id="5398d-p107">The Office 365 Management APIs use Azure AD to provide secure authentication to Office 365 tenant data. To access the Office 365 Management APIs, you need to register your app in Azure AD, and as part of the configuration, you will specify the permission levels your app needs to access the APIs.</span></span>


### <a name="prerequisites"></a><span data-ttu-id="5398d-130">前提条件</span><span class="sxs-lookup"><span data-stu-id="5398d-130">Prerequisites</span></span>

<span data-ttu-id="5398d-p108">Azure AD でアプリを登録するには、Office 365 サブスクリプションと、Office 365 サブスクリプションに関連付けられている Azure のサブスクリプションが必要です。開始するには、Office 365 と Azure の両方に、試用版のサブスクリプションを使用できます。詳細については、「[Office 365 開発者プログラムへようこそ](https://docs.microsoft.com/office/developer-program/office-365-developer-program)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5398d-p108">To register your app in Azure AD, you need a subscription to Office 365 and a subscription to Azure that has been associated with your Office 365 subscription. You can use trial subscriptions to both Office 365 and Azure to get started. For more details, see [Welcome to the Office 365 Developer Program](https://docs.microsoft.com/office/developer-program/office-365-developer-program).</span></span>


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a><span data-ttu-id="5398d-134">Azure の管理ポータルを使用してアプリケーションを Azure AD で登録する</span><span class="sxs-lookup"><span data-stu-id="5398d-134">Use the Azure Management Portal to register your application in Azure AD</span></span>

<span data-ttu-id="5398d-135">適切なサブスクリプションを持つ Microsoft のテナントがあれば、Azure AD でアプリケーションを登録できます。</span><span class="sxs-lookup"><span data-stu-id="5398d-135">After you have a Microsoft tenant with the proper subscriptions, you can register your application in Azure AD.</span></span>

1. <span data-ttu-id="5398d-p109">使用する Office 365 サブスクリプションを持つ Microsoft のテナントの資格情報を使用して、[Azure の管理ポータル](https://manage.windowsazure.com/)にサインインします。Azure の管理ポータルには、[Office の管理ポータル](https://portal.office.com/)の左側のナビゲーション ペインに表示されるリンク経由でアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p109">Sign into the [Azure management portal](https://manage.windowsazure.com/), using the credential of your Microsoft tenant that has the subscription to Office 365 you wish to use. You can also access the Azure Management Portal via a link that appears in the left navigation pane in the [Office admin portal](https://portal.office.com/).</span></span>
    
2. <span data-ttu-id="5398d-p110">左側のナビゲーション パネルで、[Active Directory] (1) を選択します。[ディレクトリ] タブ (2) が選択されていることを確認してから、ディレクトリ名 (3) を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-p110">In the left navigation panel, choose Active Directory (1). Make sure the Directory tab (2) is selected, and then select the directory name (3).</span></span>
    
   ![O365 の [サインアップ] ページ](images/o365-sign-up-page.png)
    
    
3. <span data-ttu-id="5398d-p111">ディレクトリのページで、**[アプリケーション]** を選択します。Azure AD により、現在テナントにインストールされているアプリケーションの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p111">On the directory page, select **Applications**. Azure AD displays a list of the applications currently installed in your tenancy.</span></span>
    
4. <span data-ttu-id="5398d-143">**[追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-143">Choose **Add**.</span></span>
    
   ![Office 365 の [管理] ページ](images/o365-admin-page.png)
    
    
5. <span data-ttu-id="5398d-145">**[所属組織が開発しているアプリケーションの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-145">Select **Add an application my organization is developing**.</span></span>
    
6. <span data-ttu-id="5398d-146">アプリケーションの**名前**を入力し、**[タイプ]** に [Web アプリケーション] または [WEB API] を指定します。</span><span class="sxs-lookup"><span data-stu-id="5398d-146">Enter the **NAME** of your application and specify the **Type** as WEB APPLICATION AND/OR WEB API.</span></span>
    
7. <span data-ttu-id="5398d-147">適切なアプリのプロパティを入力します。</span><span class="sxs-lookup"><span data-stu-id="5398d-147">Enter the appropriate App properties:</span></span>
    
   - <span data-ttu-id="5398d-p112">**サインオン URL**。ユーザーがサインインし、アプリを使用している URL です。必要に応じて後から変更することができます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p112">**SIGN-ON URL**. The URL where users can sign in and use your app. You can change this later as needed.</span></span>
    
   - <span data-ttu-id="5398d-p113">**アプリ ID URI**。アプリの一意の論理識別子として使用される URI です。URI は、アプリに Windows Azure AD 内のデータにアクセスする権限を付与する外部ユーザーの検証済みのカスタム ドメインでなければなりません。たとえば、Microsoft のテナントが **contoso.onmicrosoft. com** の場合、アプリ ID URI は **https://app.contoso.onmicrosoft.com** などになります。</span><span class="sxs-lookup"><span data-stu-id="5398d-p113">**APP ID URI**. The URI used as a unique logical identifier for your app. The URI must be in a verified custom domain for an external user to grant your app access to their data in Windows Azure AD. For example, if your Microsoft tenant is **contoso.onmicrosoft.com**, the APP ID URI could be **https://app.contoso.onmicrosoft.com**.</span></span>
    
8. <span data-ttu-id="5398d-p114">アプリが Azure AD に登録されて、クライアント ID が割り当てられます。ただし、構成しなければならない、アプリの重要な側面がまだ残っています。</span><span class="sxs-lookup"><span data-stu-id="5398d-p114">Your app is now registered with Azure AD, and has been assigned a client ID. However, there are several important aspects of your app left to configure.</span></span>
    

### <a name="configure-your-application-properties-in-azure-ad"></a><span data-ttu-id="5398d-157">Azure AD でアプリケーションのプロパティを構成する</span><span class="sxs-lookup"><span data-stu-id="5398d-157">Configure your application properties in Azure AD</span></span>

<span data-ttu-id="5398d-158">アプリケーションを登録すると、いくつかの重要なプロパティを指定する必要があります。プロパティでは、Azure AD 内でアプリケーションがどのように機能するか、また、テナント管理者が Office 365 Management API を使用してアプリケーションにテナント データへのアクセス許可に同意する方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="5398d-158">Now that your application is registered, there are several important properties you must specify that determine how your application functions within Azure AD and how tenant admins will grant consent to allow your application to access their data by using the Office 365 Management APIs.</span></span>

<span data-ttu-id="5398d-159">Azure AD アプリケーションの全般的なアプリケーション構成の詳細については、「[Application オブジェクトのプロパティ](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5398d-159">For more information about Azure AD application configuration in general, see [Application Object Properties](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects).</span></span>


1. <span data-ttu-id="5398d-p115">**クライアント ID**。この値は Azure AD で自動的に生成されます。アプリケーションは、テナント管理者に同意を求めるとき、および Azure AD からアプリ専用トークンを要求するときに、この値を使用します。</span><span class="sxs-lookup"><span data-stu-id="5398d-p115">**CLIENT ID**. This value is automatically generated by Azure AD. Your application will use this value when requesting consent from tenant admins and when requesting app-only tokens from Azure AD.</span></span>
    
2. <span data-ttu-id="5398d-p116">**アプリケーションはマルチ テナントです**。テナント管理者が Office 365 Management API を使用してアプリケーションにテナント データへのアクセス許可に同意するには、このプロパティは **[はい]** に設定する必要があります。このプロパティが **[いいえ]** に設定されている場合、アプリケーションは、独自のテナント データにしかアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="5398d-p116">**APPLICATION IS MULTI-TENANT**. This property must be set to **YES** to allow tenant admins to grant consent to your app to access their data by using the Office 365 Management APIs. If this property is set to **NO**, your application will only be able to access your own tenant's data.</span></span>
    
3. <span data-ttu-id="5398d-p117">**応答 URL**。これは、Office 365 Management API を使用してアプリケーションのデータへのアクセス許可に同意した後にテナント管理者がリダイレクトされる URL です。必要に応じて、複数の応答 URL を設定できます。Azure は、アプリケーションを作成する際、指定したサインオン URL に最初に一致した URL を自動的に設定しますが、必要に応じてこの値を変更することができます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p117">**REPLY URL**. This is the URL that a tenant admin will be redirected to after granting consent to allow your application to access their data by using the Office 365 Management APIs. You can configure multiple reply URLs as needed. Azure automatically sets the first one to match the sign-on URL you specified when you created the application, but you can change this value as needed.</span></span>
    
<span data-ttu-id="5398d-170">これらのプロパティを変更した後は、必ず **[保存]** をクリックしてください。</span><span class="sxs-lookup"><span data-stu-id="5398d-170">Be sure to choose **Save** after making any changes to these properties.</span></span>


### <a name="generate-a-new-key-for-your-application"></a><span data-ttu-id="5398d-171">アプリケーションの新しいキーを生成する</span><span class="sxs-lookup"><span data-stu-id="5398d-171">Generate a new key for your application</span></span>

<span data-ttu-id="5398d-172">キー (クライアント シークレットとも呼ばれます) は、アクセス トークンの認証コードを交換するときに使用されます。</span><span class="sxs-lookup"><span data-stu-id="5398d-172">Keys, also known as client secrets, are used when exchanging an authorization code for an access token.</span></span>


1. <span data-ttu-id="5398d-p118">Azure 管理ポータルで、アプリケーションを選択し、上部メニューの **[構成]** を選択します。**[キー]** までスクロールダウンします。</span><span class="sxs-lookup"><span data-stu-id="5398d-p118">In the Azure Management Portal, select your application and choose **Configure** in the top menu. Scroll down to **keys**.</span></span>
    
2. <span data-ttu-id="5398d-175">キーの期間を選択し、**[保存]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="5398d-175">Select the duration for your key, and choose **Save**.</span></span>
    
   ![[Azure サブスクリプション] ページ](images/azure-subscription-page.png)
    
    
3. <span data-ttu-id="5398d-p119">Azure では、保存後にのみアプリケーション シークレットが表示されます。クリップボード アイコンをクリックして、クライアント シークレットをクリップボードにコピーします。</span><span class="sxs-lookup"><span data-stu-id="5398d-p119">Azure displays the app secret only after saving it. Select the Clipboard icon to copy the client secret to the Clipboard.</span></span>
    
   ![Azure ポータル ページ](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > <span data-ttu-id="5398d-p120">Azure は、クライアント シークレットを最初に生成したときにのみ表示します。その後で、このページに戻って、クライアント シークレットを取得することはできません。</span><span class="sxs-lookup"><span data-stu-id="5398d-p120">Azure only displays the client secret at the time you initially generate it. You cannot navigate back to this page and retrieve the client secret later.</span></span>

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a><span data-ttu-id="5398d-182">サービス間の呼び出しを有効にする X.509 証明書を構成します。</span><span class="sxs-lookup"><span data-stu-id="5398d-182">Configure an X.509 certificate to enable service-to-service calls</span></span>

<span data-ttu-id="5398d-183">デーモンやサービスなど、バックグラウンドで実行されているアプリケーションは、最初の同意が与えられた後、繰り返しテナント管理者に同意を求めることがなく、アプリ専用アクセス トークン要求にクライアントの資格情報を使用できます。</span><span class="sxs-lookup"><span data-stu-id="5398d-183">An application that is running in the background, such as a daemon or service, can use client credentials to request app-only access tokens without repeatedly requesting consent from the tenant admin after initial consent is granted.</span></span> 

<span data-ttu-id="5398d-184">詳細については、「[クライアント資格情報を使用したサービス間の呼び出し](https://msdn.microsoft.com/library/azure/dn645543.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5398d-184">For more information, see [Service to Service Calls Using Client Credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

<span data-ttu-id="5398d-p121">Azure AD からアプリ専用アクセス トークンを要求するときは、X.509 証明書をクライアントの資格情報として使用するよう、アプリケーションを構成しなければなりません。プロセスは 2 つの手順で行います。</span><span class="sxs-lookup"><span data-stu-id="5398d-p121">You must configure an X.509 certificate with your application to be used as client credentials when requesting app-only access tokens from Azure AD. There are two steps to the process:</span></span>

- <span data-ttu-id="5398d-p122">X.509 証明書を取得する。自己署名証明書または公的に信頼された証明機関によって発行された証明書を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p122">Obtain an X.509 certificate. You can use a self-signed certificate or a certificate issued by publicly trusted certificate authority.</span></span>
    
- <span data-ttu-id="5398d-189">拇印と、証明書の公開キーを含むようにアプリケーション マニフェストを変更します。</span><span class="sxs-lookup"><span data-stu-id="5398d-189">Modify your application manifest to include the thumbprint and public key of your certificate.</span></span>
    
<span data-ttu-id="5398d-190">次の手順は、Visual Studio または Windows SDK _makecert_ ツールを使用して自己署名証明書を生成し、base64 でエンコードされたファイルに公開キーをエクスポートする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="5398d-190">The following instructions show you how to use the Visual Studio or Windows SDK _makecert_ tool to generate a self-signed certificate and export the public key to a base64-encoded file.</span></span>


1. <span data-ttu-id="5398d-191">コマンド ラインから、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="5398d-191">From the command line, run the following:</span></span>
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > <span data-ttu-id="5398d-192">X.509 証明書の生成時に、キーの長さが 2048 以上になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="5398d-192">When you are generating the X.509 certificate, make sure the key length is at least 2048.</span></span> <span data-ttu-id="5398d-193">キーの長さがそれより短い場合は、有効なキーとして受け入れられません。</span><span class="sxs-lookup"><span data-stu-id="5398d-193">Shorter key lengths are not accepted as valid keys.</span></span>

2. <span data-ttu-id="5398d-194">証明書 MMC スナップインを開き、自分のユーザー アカウントに接続します。</span><span class="sxs-lookup"><span data-stu-id="5398d-194">Open the Certificates MMC snap-in and connect to your user account.</span></span> 
    
3. <span data-ttu-id="5398d-195">個人用フォルダーで新しい証明書を検索し、base64 でエンコードされたファイル (mycompanyname.cer など) に公開キーをエクスポートします。</span><span class="sxs-lookup"><span data-stu-id="5398d-195">Find the new certificate in the Personal folder and export the public key to a base64-encoded file (for example, mycompanyname.cer).</span></span> <span data-ttu-id="5398d-196">アプリケーションは、この証明書を Azure AD との通信に使用するため、秘密キーへのアクセスも確実に維持されるようになります。</span><span class="sxs-lookup"><span data-stu-id="5398d-196">Your application will use this certificate to communicate with Azure AD, so make sure you retain access to the private key as well.</span></span>
    
   > [!NOTE] 
   > <span data-ttu-id="5398d-197">Windows PowerShell を使用すると、拇印および Base64 でエンコードされた公開キーを抽出できます。</span><span class="sxs-lookup"><span data-stu-id="5398d-197">You can use Windows PowerShell to extract the thumbprint and base64-encoded public key.</span></span> <span data-ttu-id="5398d-198">その他のプラットフォームには、証明書のプロパティを取得する同様のツールがあります。</span><span class="sxs-lookup"><span data-stu-id="5398d-198">Other platforms provide similar tools to retrieve properties of certificates.</span></span>

4. <span data-ttu-id="5398d-199">Windows PowerShell プロンプトから、次を入力して実行します。</span><span class="sxs-lookup"><span data-stu-id="5398d-199">From the Windows PowerShell prompt, type and run the following:</span></span>
    
   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. <span data-ttu-id="5398d-200">`$base64Thumbprint`、`$base64Value`、および `$keyid` の値を保存します。これらの値は、次の一連の手順でアプリケーション マニフェストを更新するときに必要になります。</span><span class="sxs-lookup"><span data-stu-id="5398d-200">Store the values for `$base64Thumbprint`, `$base64Value`, and `$keyid` to be used when you update your application manifest in the next set of steps.</span></span>
    
   <span data-ttu-id="5398d-201">ここで、証明書から抽出された値と、生成されたキー ID を使用して、Azure AD のアプリケーション マニフェストを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-201">Using the values extracted from the certificate and the generated key ID, you must now update your application manifest in Azure AD.</span></span>
    
6. <span data-ttu-id="5398d-202">Azure 管理ポータルで、アプリケーションを選択し、上部メニューの **[構成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-202">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span>
    
7. <span data-ttu-id="5398d-203">コマンド バーの **[管理マニフェスト]** を選択してから、**[マニフェストをダウンロード]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-203">In the command bar, choose **Manage manifest**, and then choose **Download Manifest**.</span></span>
    
   ![コマンド ライン証明書の表示](images/command-line-certificate-display.png)
    
    
8. <span data-ttu-id="5398d-205">編集するためにダウンロードしたマニフェストを開き、空の KeyCredentials プロパティを次の JSON で置き換えます。</span><span class="sxs-lookup"><span data-stu-id="5398d-205">Open the downloaded manifest for editing and replace the empty KeyCredentials property with the following JSON:</span></span>
    
   ```json
      "keyCredentials": [
        {
            "customKeyIdentifier" : "$base64Thumbprint_from_above",
            "keyId": "$keyid_from_above",
            "type": "AsymmetricX509Cert",
            "usage": "Verify",
            "value": "$base64Value_from_above"
        }
    ],
   ```


   > [!NOTE] 
   > <span data-ttu-id="5398d-206">[KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) プロパティは、ロール オーバー シナリオでは複数の X.509 証明書のアップロードを可能にする、または漏えいシナリオでは証明書を削除することを可能にするコレクションです。</span><span class="sxs-lookup"><span data-stu-id="5398d-206">The [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) property is a collection, making it possible to upload multiple X.509 certificates for rollover scenarios or delete certificates for compromise scenarios.</span></span>

9. <span data-ttu-id="5398d-207">変更内容を保存します。コマンド バーの **[管理マニフェスト]** を選択して **[マニフェストをアップロード]** を選択し、更新したマニフェスト ファイルを参照してそのファイルを選択することで、更新済みのマニフェストをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="5398d-207">Save your changes and upload the updated manifest by choosing **Manage manifest** in the command bar, choosing **Upload manifest**, browsing to your updated manifest file, and then selecting it.</span></span>
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a><span data-ttu-id="5398d-208">アプリが Office 365 Management APIにアクセスするために必要な許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="5398d-208">Specify the permissions your app requires to access the Office 365 Management APIs</span></span>

<span data-ttu-id="5398d-p126">最後に、Office 365 Management API でアプリがどのようなアクセス許可を必要とするかを具体的に指定する必要があります。これを行うには、アプリに Office 365 Management API へのアクセスを追加して、必要なアクセス許可を指定します。</span><span class="sxs-lookup"><span data-stu-id="5398d-p126">Finally, you need to specify exactly what permissions your app requires of the Office 365 Management APIs. To do so, you add access to the Office 365 Management APIs to your app, and then you specify the permission(s) you need.</span></span>


1. <span data-ttu-id="5398d-211">Azure 管理ポータルで、アプリケーションを選択して、上部メニューの **[構成]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-211">In the Azure Management Portal, select your application, and choose **Configure** in the top menu.</span></span> <span data-ttu-id="5398d-212">**[他のアプリケーションに対するアクセス許可]** までスクロール ダウンして、**[アプリケーションの追加]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-212">Scroll down to **permissions to other applications**, and choose **Add application**.</span></span>
    
   ![Azure AD のページ](images/azure-ad-page.png)
    
    
2. <span data-ttu-id="5398d-214">**Office 365 Management API** を選択して (1) **[選択済み]** 列に表示し、(2) 右下のチェック マークを選択して (3) 選択内容を保存し、アプリケーションのメインの構成ページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="5398d-214">Select the **Office 365 Management APIs** (1) so that it appears in the **Selected** column (2), and then select the check mark in the lower right (3) to save your selection and return to the main configuration page for your application.</span></span>
    
   ![[Azure AD アプリ] ページ](images/azure-ad-apps-page.png)
    
    
3. <span data-ttu-id="5398d-216">これで、目的のアプリケーションがアクセス許可を必要とするアプリケーションの一覧に、Office Management API が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5398d-216">The Office Management APIs now appear in the list of applications to which your application requires permissions.</span></span> <span data-ttu-id="5398d-217">**[アプリケーションのアクセス許可]** と **[デリゲートされたアクセス許可]** の両方で、アプリケーションで必要なアクセス許可を選択します。</span><span class="sxs-lookup"><span data-stu-id="5398d-217">Under both **Application Permissions** and **Delegated Permissions**, select the permissions your application requires.</span></span> <span data-ttu-id="5398d-218">各アクセス許可の詳細については、それぞれ特定の API リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="5398d-218">Refer to the specific API reference for more details about each permission.</span></span>  

   > [!NOTE] 
   > <span data-ttu-id="5398d-219">活動レポートおよび将来的に削除される脅威インテリジェンスと関連した、未使用のアクセス許可が現在 4 つあります。</span><span class="sxs-lookup"><span data-stu-id="5398d-219">There are currently four unused permissions related to activity reports and threat intelligence that will be removed in the future.</span></span> <span data-ttu-id="5398d-220">これらのアクセス許可は不要なため、いずれも選択しないでください。</span><span class="sxs-lookup"><span data-stu-id="5398d-220">Do not select any of these permissions because they are unnecessary.</span></span>
    
   ![[アプリケーションの追加] ダイアログ](images/add-an-application-dialog.png)
    
    
4. <span data-ttu-id="5398d-222">**[保存]** を選択して、構成を保存します。</span><span class="sxs-lookup"><span data-stu-id="5398d-222">Choose **Save** to save the configuration.</span></span>
    

## <a name="get-office-365-tenant-admin-consent"></a><span data-ttu-id="5398d-223">Office 365 テナント管理者の同意を得る</span><span class="sxs-lookup"><span data-stu-id="5398d-223">Get Office 365 tenant admin consent</span></span>

<span data-ttu-id="5398d-224">アプリケーションに Office 365 Management API を使用するために必要なアクセス許可が構成されたため、テナント管理者は、アプリケーションが API を使用してテナントのデータにアクセスするために、これらのアクセス許可を明示的に与える必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-224">Now that your application is configured with the permissions it needs to use the Office 365 Management APIs, a tenant admin must explicitly grant your application these permissions in order to access their tenant's data by using the APIs.</span></span> <span data-ttu-id="5398d-225">同意を与えるには、テナント管理者が、次に示す特別に作成された URL を使用して、Azure AD にサインインする必要があります。この URL では、アプリケーションの要求したアクセス許可を確認することができます。</span><span class="sxs-lookup"><span data-stu-id="5398d-225">To grant consent, the tenant admin must sign in to Azure AD by using the following specially constructed URL, where they can review your application's requested permissions.</span></span> <span data-ttu-id="5398d-226">自分が所有するテナントのデータにアクセスするために API を使用する場合、この手順は必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="5398d-226">This step is not required when using the APIs to access data from your own tenant.</span></span>


```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

<span data-ttu-id="5398d-227">リダイレクト URL は、Azure AD でアプリケーション用に構成された応答 URL のいずれかと一致するか、サブ パスである必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-227">The redirect URL must match or be a sub-path under one of the Reply URLs configured for your application in Azure AD.</span></span>

<span data-ttu-id="5398d-228">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="5398d-228">For example:</span></span>

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

<span data-ttu-id="5398d-229">同意 URL をテストするには、その URL をブラウザーに貼り付けて、アプリケーションの登録に使用したテナント以外のテナントの Office 365 管理者の資格情報を使用してサインインします。</span><span class="sxs-lookup"><span data-stu-id="5398d-229">You can test the consent URL by pasting it into a browser and signing in using the credentials of an Office 365 admin for a tenant other than the tenant that you used to register the application.</span></span> <span data-ttu-id="5398d-230">Office Management API を使用するために必要なアプリケーションのアクセス許可を付与する要求が表示されます。</span><span class="sxs-lookup"><span data-stu-id="5398d-230">You will see the request to grant your application permission to use the Office Management APIs.</span></span>


![Azure AD アプリの追加ページ](images/azure-ad-app-added-page.png)

<span data-ttu-id="5398d-232">**[承諾]** を選択すると、指定のページにリダイレクトされます。ページにはクエリ文字列でコードが記載されています。</span><span class="sxs-lookup"><span data-stu-id="5398d-232">After choosing **Accept**, you are redirected to the specified page, and there will be a code in the query string.</span></span> 

<span data-ttu-id="5398d-233">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="5398d-233">For example:</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="5398d-234">アプリケーションは、この認証コードを使用して Azure AD からアクセス トークンを取得します。そのトークンからテナント ID を抽出できます。</span><span class="sxs-lookup"><span data-stu-id="5398d-234">Your application uses this authorization code to obtain an access token from Azure AD, from which the tenant ID can be extracted.</span></span> <span data-ttu-id="5398d-235">テナント ID を抽出して格納すると、テナント管理者のサインインを必要とすることなく、その後のアクセス トークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="5398d-235">After you have extracted and stored the tenant ID, you can obtain subsequent access tokens without requiring the tenant admin to sign in.</span></span>


## <a name="request-access-tokens-from-azure-ad"></a><span data-ttu-id="5398d-236">Azure AD からアクセス トークンを要求する</span><span class="sxs-lookup"><span data-stu-id="5398d-236">Request access tokens from Azure AD</span></span>

<span data-ttu-id="5398d-237">Azure AD からアクセス トークンを要求する方法は 2 つです。</span><span class="sxs-lookup"><span data-stu-id="5398d-237">There are two methods for requesting access tokens from Azure AD:</span></span>

- <span data-ttu-id="5398d-p133">[承認コードの許可フロー](https://msdn.microsoft.com/library/azure/dn645542.aspx)では、テナント管理者が明示的な同意を与え、それによりアプリケーションに認証コードが返されます。その後、アプリケーションはアクセス トークンの認証コードを交換します。このメソッドは、アプリケーションが API を使用してテナントのデータにアクセスするために必要な初期の同意を取得するために必要です。また、この初期の同意は、テナント ID を取得し、保存するために必要です。</span><span class="sxs-lookup"><span data-stu-id="5398d-p133">The [Authorization Code Grant Flow](https://msdn.microsoft.com/library/azure/dn645542.aspx) involves a tenant admin granting explicit consent, which returns an authorization code to your application. Your application then exchanges the authorization code for an access token. This method is required to obtain the initial consent that your application needs to access the tenant data by using the API, and this first access token is needed in order to obtain and store the tenant ID.</span></span>
    
- <span data-ttu-id="5398d-241">[クライアント資格情報の許可フロー](https://msdn.microsoft.com/library/azure/dn645543.aspx)では、古いアクセス トークンが期限切れになったときに、テナント管理者がサインインして同意を明示的に与える必要なしで、アプリケーションは以降のアクセス トークンを要求できるようになります。</span><span class="sxs-lookup"><span data-stu-id="5398d-241">The [Client Credentials Grant Flow](https://msdn.microsoft.com/library/azure/dn645543.aspx) allows your application to request subsequent access tokens as old ones expire, without requiring the tenant admin to sign in and explicitly grant consent.</span></span> <span data-ttu-id="5398d-242">このメソッドは、初期テナント管理者の同意が与えられた後、API を呼び出すバックグラウンドで継続的に実行するアプリケーションで使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-242">This method must be used for applications that run continuously in the background calling the APIs once the initial tenant admin consent has been granted.</span></span>
    

### <a name="request-an-access-token-using-the-authorization-code"></a><span data-ttu-id="5398d-243">承認コードを使用してアクセス トークンを要求する</span><span class="sxs-lookup"><span data-stu-id="5398d-243">Request an access token using the authorization code</span></span>

<span data-ttu-id="5398d-244">テナント管理者が同意を与えると、テナント管理者が Azure AD によって指定の URL にリダイレクトされるときに、アプリケーションはクエリ文字列パラメーターとして認証コードを受け取ります。</span><span class="sxs-lookup"><span data-stu-id="5398d-244">After a tenant admin grants consent, your application receives an authorization code as a query string parameter when Azure AD redirects the tenant admin to your designated URL.</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="5398d-245">アプリケーションはアクセス トークンの認証コードを交換するために Azure AD に HTTP REST POST を実行します。</span><span class="sxs-lookup"><span data-stu-id="5398d-245">Your application makes an HTTP REST POST to Azure AD to exchange the authorization code for an access token.</span></span> <span data-ttu-id="5398d-246">テナント ID がまだ不明であるため、POST は「共通」のエンドポイントに送られます。このエンドポイントの URL にはテナント ID が埋め込まれていません。</span><span class="sxs-lookup"><span data-stu-id="5398d-246">Because the tenant ID is not yet known, the POST will be to the "common" endpoint, which does not have the tenant ID embedded in the URL:</span></span>

```http
https://login.windows.net/common/oauth2/token
```

<span data-ttu-id="5398d-247">POST の本文には、次の記述が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5398d-247">The body of the POST contains the following:</span></span>

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a><span data-ttu-id="5398d-248">要求の例</span><span class="sxs-lookup"><span data-stu-id="5398d-248">Sample request</span></span>

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

<span data-ttu-id="5398d-249">アクセス トークンを含むいくつかのプロパティには、応答の本文が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5398d-249">The body of the response will include several properties, including the access token.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="5398d-250">応答例</span><span class="sxs-lookup"><span data-stu-id="5398d-250">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

<span data-ttu-id="5398d-p136">返されるアクセス トークンは、同意とアクセスを要求するアプリケーションの両方に関する情報が含まれる JWT トークンです。エンコードされていないトークンの例を次に示します。アプリケーションは、このトークンからテナント ID「tid」を抽出し、期限切れの際に管理者のさらなる介入なしに追加のアクセス トークンを要求するために使用できるよう、保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-p136">The access token that is returned is a JWT token that includes information about both the admin that granted consent and the application requesting access. The following shows an example of an un-encoded token. Your application must extract the tenant ID "tid" from this token and store it so that it can be used to request additional access tokens as they expire, without further admin interaction.</span></span>

#### <a name="sample-token"></a><span data-ttu-id="5398d-254">トークンの例</span><span class="sxs-lookup"><span data-stu-id="5398d-254">Sample token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1427246416,
  "nbf": 1427246416,
  "exp": 1427250316,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "amr": [
    "pwd"
  ],
  "oid": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
  "upn": "admin@contoso.onmicrosoft.com",
  "puid": "1003BFFD8EC47CA6",
  "sub": "7XpD5OWAXM1OWmKiVKh1FOkKXV4N3OSRol6mz1pxxhU",
  "given_name": "John",
  "family_name": "Doe",
  "name": "Contoso, Inc.",
  "unique_name": "admin@contoso.onmicrosoft.com",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1",
  "scp": "ActivityFeed.Read ServiceHealth.Read",
  "acr": "1"
}
```

### <a name="request-an-access-token-by-using-client-credentials"></a><span data-ttu-id="5398d-255">クライアントの資格情報を使用してアクセス トークンを要求する</span><span class="sxs-lookup"><span data-stu-id="5398d-255">Request an access token by using client credentials</span></span>

<span data-ttu-id="5398d-256">テナント ID が判明すると、アプリケーションは、Azure AD にサービス間の呼び出しを行い、期限切れの際に追加のアクセス トークンを要求することができます。</span><span class="sxs-lookup"><span data-stu-id="5398d-256">After the tenant ID is known, your application can make service-to-service calls to Azure AD to request additional access tokens as they expire.</span></span> <span data-ttu-id="5398d-257">これらのトークンには、同意を許可した管理者ではなく、要求元のアプリケーションについてのみ情報が含まれます。</span><span class="sxs-lookup"><span data-stu-id="5398d-257">These tokens include information only about the requesting application and not about the admin that originally granted consent.</span></span> <span data-ttu-id="5398d-258">サービス間の呼び出しでは、アプリケーションが X.509 証明書を使用して、base64 でエンコードされ、SHA256 で署名されている JWT ベアラー トークンの形式でクライアントのアサーションを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-258">Service-to-service calls require that your application use an X.509 certificate to create client assertion in the form of a base64-encoded, SHA256 signed JWT bearer token.</span></span>

<span data-ttu-id="5398d-p138">.NET でアプリケーションを開発するときには、[Azure AD Authentication Library (ADAL)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-libraries) を使用してクライアントのアサーションを作成できます。他の開発プラットフォームにも同様のライブラリが必要です。</span><span class="sxs-lookup"><span data-stu-id="5398d-p138">When you are developing your application in .NET, you can use the [Azure AD Authentication Library (ADAL)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-libraries) to create client assertions. Other development platforms should have similar libraries.</span></span>

<span data-ttu-id="5398d-261">エンコードされていない JWT トークンは、次のプロパティを持つヘッダーとペイロードで構成されます。</span><span class="sxs-lookup"><span data-stu-id="5398d-261">An un-encoded JWT token consists of a header and payload that have the following properties.</span></span>

```json
HEADER:

{
  "alg": "RS256",
  "x5t": "{thumbprint of your X.509 certificate used to sign the token",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/{tenantid}/oauth2/token",
  "iss": "{your app client ID}",
  "sub": "{your app client ID}"
  "jti": "{random GUID}",
  "nbf": {epoch time, before which the token is not valid},
  "exp": {epoch time, after which the token is not valid},
}

```

#### <a name="sample-jwt-token"></a><span data-ttu-id="5398d-262">JWT トークンの例</span><span class="sxs-lookup"><span data-stu-id="5398d-262">Sample JWT token</span></span>


```json
HEADER:

{
  "alg": "RS256",
  "x5t": "YyfshJC3rPQ-kpGo5dUaiY5t3iU",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token",
  "iss": "a6099727-6b7b-482c-b509-1df309acc563",
  "sub": "a6099727-6b7b-482c-b509-1df309acc563"
  "jti": "0ce254c4-81b1-4a2e-8436-9a8c3b49dfb9",
  "nbf": 1427248048,
  "exp": 1427248648,
}
```

<span data-ttu-id="5398d-p139">クライアントのアサーションは、アクセス トークンを要求するサービス間の呼び出しの一部として Azure AD に渡されます。クライアントの資格情報を使用してアクセス トークンを要求する際は、HTTP POST をテナント固有のエンドポイントに使用してください。このエンドポイントのURL には、以前に抽出され、格納されたテナント ID が埋め込まれています。</span><span class="sxs-lookup"><span data-stu-id="5398d-p139">The client assertion is then passed to Azure AD as part of a service-to-service call to request an access token. When using client credentials to request an access token, use an HTTP POST to a tenant-specific endpoint, where the previously extracted and stored tenant ID is embedded in the URL.</span></span>


```http
https://login.windows.net/{tenantid}/oauth2/token
```

<span data-ttu-id="5398d-265">POST の本文には、次の記述が含まれています。</span><span class="sxs-lookup"><span data-stu-id="5398d-265">The body of the POST contains the following:</span></span>


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a><span data-ttu-id="5398d-266">要求の例</span><span class="sxs-lookup"><span data-stu-id="5398d-266">Sample request</span></span>

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

<span data-ttu-id="5398d-267">応答は前と同じになりますが、トークンは同じプロパティを持ちません。同意を許可する管理者のプロパティが含まれていないためです。</span><span class="sxs-lookup"><span data-stu-id="5398d-267">The response will be the same as before, but the token will not have the same properties, because it does not contain properties of the admin that granted consent.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="5398d-268">応答例</span><span class="sxs-lookup"><span data-stu-id="5398d-268">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a><span data-ttu-id="5398d-269">アクセス トークンの例</span><span class="sxs-lookup"><span data-stu-id="5398d-269">Sample access token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1431655194,
  "nbf": 1431655194,
  "exp": 1431659094,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "roles": [
    "ServiceHealth.Read",
    "ActivityFeed.Read"
  ],
  "oid": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "sub": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "idp": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1"
}
```


## <a name="build-your-app"></a><span data-ttu-id="5398d-270">アプリを作成する</span><span class="sxs-lookup"><span data-stu-id="5398d-270">Build your app</span></span>

<span data-ttu-id="5398d-p140">Azure AD でアプリを登録して、必要なアクセス許可を構成したため、これでアプリを作成する準備ができました。以下は、アプリを設計し、作成する際に考慮すべき重要な側面の一部です。</span><span class="sxs-lookup"><span data-stu-id="5398d-p140">Now that you have registered your app in Azure AD and configured it with the necessary permissions, you're ready to build your app. The following are some of the key aspects to consider when designing and building your app:</span></span>

- <span data-ttu-id="5398d-p141">**同意エクスペリエンス**。お客様からの同意を得るには、ブラウザーにAzure AD の Web サイトに移動させる必要があります。前述の特別に作成された URL を使用し、同意を得た後に Azure AD がリダイレクトする Web サイトを準備する必要があります。この Web サイトは URL から認証コードを抽出し、それを使用してテナント ID を取得するアクセス トークンを要求する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-p141">**The consent experience**. To obtain consent from your customers, you must direct them in a browser to the Azure AD website, using the specially constructed URL described previously, and you must have a website to which Azure AD will redirect the admin once they grant consent. This website must extract the authorization code from the URL and use it to request an access token from which it can obtain the tenant ID.</span></span>
    
- <span data-ttu-id="5398d-p142">**システムにテナント ID を格納する**。Azure AD からアクセス トークンを要求するとき、および Office Management API を呼び出すときに必要となります。</span><span class="sxs-lookup"><span data-stu-id="5398d-p142">**Store the tenant ID in your system**. This will be needed when requesting access tokens from Azure AD and when calling the Office Management APIs.</span></span>
    
- <span data-ttu-id="5398d-p143">**アクセス トークンを管理する**。必要に応じてアクセス トークンを要求および管理するコンポーネントが必要です。アプリが定期的に API を呼び出す場合、トークンをオンデマンドで要求することができます。また、データ取得のために継続的に API を呼び出す場合は、定期的な間隔 (たとえば、45 分ごと) でトークンを要求することができます。</span><span class="sxs-lookup"><span data-stu-id="5398d-p143">**Managing access tokens**. You will need a component that requests and manages access tokens as needed. If your app calls the APIs periodically, it can request tokens on demand, or if it calls the APIs continuously to retrieve data, it can request tokens at regular intervals (for example, every 45 minutes).</span></span>
    
- <span data-ttu-id="5398d-281">必要に応じて使用している特定の API により **Webhook リスナーを実装する**。</span><span class="sxs-lookup"><span data-stu-id="5398d-281">**Implement a webhook listener** as needed by the particular API you are using.</span></span>
    
- <span data-ttu-id="5398d-p144">**データを取得し、格納する**。使用している特定の API によって、連続的なポーリングを使用して、または Webhook 通知への応答として、各テナントのデータを取得するコンポーネントが必要があります。</span><span class="sxs-lookup"><span data-stu-id="5398d-p144">**Data retrieval and storage**. You'll need a component that retrieves data for each tenant, either by using continuous polling or in response to webhook notifications, depending on the particular API you are using.</span></span>
    
