<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="f58d6-101">この演習では、カスタムコネクタに対して委任されたアクセス許可を提供するために使用される新しい Azure Active Directory アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-101">In this exercise, you will create a new Azure Active Directory Application which will be used to provide the delegated permissions for the custom connector.</span></span>

<span data-ttu-id="f58d6-102">ブラウザーを開き、 [Azure Active Directory 管理センター](https://aad.portal.azure.com)に移動します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-102">Open a browser and navigate to [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="f58d6-103">左側のナビゲーションメニューで [ **azure active directory** ] リンクを選択し、 **azure active directory**ブレードの [**管理**] セクションで [**アプリの登録**] エントリを選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-103">Choose the **Azure Active Directory** link in the left navigation menu, then choose the **App registrations** entry in the **Manage** section of the **Azure Active Directory** blade.</span></span>

![azure active directory 管理センターの azure active directory ブレードのスクリーンショット](./images/app-reg1.png)

<span data-ttu-id="f58d6-105">**アプリ登録**ブレードの上部にある [**新しいアプリケーション登録**] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-105">Choose the **New application registration** menu item at the top of the **App Registrations** blade.</span></span>

![Azure Active Directory 管理センターのアプリ登録ブレードのスクリーンショット](./images/app-reg2.png)

<span data-ttu-id="f58d6-107">[ `MS Graph Batch App` **名前**] フィールドにと`https://localhost.com/$batch`入力し、[**サインオン URL** ] フィールドにと入力して、[**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-107">Enter `MS Graph Batch App` in the **Name** field, and `https://localhost.com/$batch` in the **Sign-on URL** field and choose **Create**.</span></span>

![Azure Active Directory 管理センターで新しいアプリを登録するための作成フォームのスクリーンショット](./images/app-reg3.png)

<span data-ttu-id="f58d6-109">[ **MS Graph バッチアプリ**] ページで、アプリケーションの**アプリケーション ID**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="f58d6-109">On the **MS Graph Batch App** page, copy the **Application ID** of the application.</span></span> <span data-ttu-id="f58d6-110">次の手順でこれを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f58d6-110">You'll need this in the next exercise.</span></span>

![登録済みアプリケーションページのスクリーンショット](./images/app-reg4.png)

<span data-ttu-id="f58d6-112">[アプリケーション名] の下にある**設定**ギアを選択し、[設定] ブレードの [**必要なアクセス許可**] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-112">Choose the **Settings** gear under the application name, then choose the **Required Permissions** menu item in the Settings blade.</span></span> <span data-ttu-id="f58d6-113">**必要なアクセス許可**のブレードの上部にある [**追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-113">Choose **Add** at the top of the **Required Permissions** blade.</span></span>

![必要なアクセス許可ブレードのスクリーンショット](./images/app-perms1.png)

<span data-ttu-id="f58d6-115">[ **Add api access** blade] で [ **api の選択**] オプションを選択し、[ **Microsoft Graph** ] 項目を選択して、ブレードの下部にある **[選択**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-115">Choose the **Select an API** option in the **Add API access** blade, then select the **Microsoft Graph** item and choose **Select** at the bottom of the blade.</span></span>

![[API ブレードの選択] のスクリーンショット](./images/app-perms2.png)

<span data-ttu-id="f58d6-117">[**アクセスを有効にする**] ブレードで、[委任された**アクセス許可**] セクションまで下にスクロールします。</span><span class="sxs-lookup"><span data-stu-id="f58d6-117">On the **Enable Access** blade, scroll down to the **Delegated Permissions** section.</span></span> <span data-ttu-id="f58d6-118">[**すべてのグループの読み取りと書き込み**] アクセス許可を選択し、ブレードの下部にある **[選択]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-118">Select the **Read and write all groups** delegated permission, then choose **Select** at the bottom of the blade.</span></span> <span data-ttu-id="f58d6-119">**Add API access** blade の下部にある [**完了**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-119">Choose **Done** at the bottom of the **Add API access** blade.</span></span>

 ![アクセスブレードを有効にするためのスクリーンショット](./images/app-perms3.png)

<span data-ttu-id="f58d6-121">**Settings** blade で [ **Keys** ] メニュー項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-121">Choose the **Keys** menu item on the **Settings** blade.</span></span> <span data-ttu-id="f58d6-122">キー `forever`の**説明**にを入力し、[**期間**] ドロップダウンメニューから [**無期限**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-122">Enter `forever` in the **Key description** and select **Never expires** from the **Duration** drop down menu.</span></span> <span data-ttu-id="f58d6-123">[**キー** ] ブレードの上部にある [**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-123">Choose **Save** at the top of the **Keys** blade.</span></span> <span data-ttu-id="f58d6-124">新しいキーのキー値をコピーします。</span><span class="sxs-lookup"><span data-stu-id="f58d6-124">Copy the key value for the new key.</span></span> <span data-ttu-id="f58d6-125">次の手順でこれを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f58d6-125">You'll need this in the next exercise.</span></span>

![キーブレードのスクリーンショット](./images/app-key1.png)

> [!IMPORTANT]
> <span data-ttu-id="f58d6-127">この手順は、このブレードを閉じるとキーにアクセスできなくなるため、重要です。</span><span class="sxs-lookup"><span data-stu-id="f58d6-127">This step is critical as the key will not be accessible once you close this blade.</span></span> <span data-ttu-id="f58d6-128">このキーを、今後の演習で使用するテキストエディターに保存します。</span><span class="sxs-lookup"><span data-stu-id="f58d6-128">Save this key to a text editor for use in upcoming exercises.</span></span>

<span data-ttu-id="f58d6-129">Teams プロパティなど、Microsoft Graph からアクセスできる追加のサービスの管理を有効にするには、特定のサービスの管理を有効にするために、追加の適切なスコープを選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f58d6-129">To enable management of additional services accessible via the Microsoft Graph, including Teams properties, you would need to select additional, appropriate scopes to enable managing specific services.</span></span> <span data-ttu-id="f58d6-130">たとえば、OneNote ノートブックまたはプランナープラン、バケット、タスクの作成を可能にするソリューションを拡張するには、関連する api に必要なアクセス許可スコープを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f58d6-130">For example, to extend our solution to enable creating OneNote Notebooks or Planner plans, buckets and tasks you would need to add the required permission scopes for the relevant APIs.</span></span>