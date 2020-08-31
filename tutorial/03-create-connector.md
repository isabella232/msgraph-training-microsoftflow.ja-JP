<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b583f-101">この演習では、Microsoft Power オートメーションまたは Azure ロジックアプリで使用できる新しいカスタムコネクタを作成します。</span><span class="sxs-lookup"><span data-stu-id="b583f-101">In this exercise, you will create a new custom connector which can be used in Microsoft Power Automate or in Azure Logic Apps.</span></span> <span data-ttu-id="b583f-102">OpenAPI 定義ファイルには、Microsoft Graph エンドポイントの正しいパス `$batch` と、簡易インポートを有効にするための追加設定があらかじめ用意されています。</span><span class="sxs-lookup"><span data-stu-id="b583f-102">The OpenAPI definition file is prebuilt with the correct path for the Microsoft Graph `$batch` endpoint and additional settings to enable simple import.</span></span>

<span data-ttu-id="b583f-103">Microsoft Graph 用のカスタムコネクタを作成するには、次の2つのオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="b583f-103">There are two options to create a custom connector for Microsoft Graph:</span></span>

- <span data-ttu-id="b583f-104">空白からの作成</span><span class="sxs-lookup"><span data-stu-id="b583f-104">Create from blank</span></span>
- <span data-ttu-id="b583f-105">OpenAPI ファイルをインポートする</span><span class="sxs-lookup"><span data-stu-id="b583f-105">Import an OpenAPI file</span></span>

## <a name="option-1-create-custom-connector-from-blank-template"></a><span data-ttu-id="b583f-106">オプション 1: 空のテンプレートからカスタムコネクタを作成する</span><span class="sxs-lookup"><span data-stu-id="b583f-106">Option 1: Create custom connector from blank template</span></span>

<span data-ttu-id="b583f-107">ブラウザーを開き、[ [Microsoft Power オートメーション](https://flow.microsoft.com)] に移動します。</span><span class="sxs-lookup"><span data-stu-id="b583f-107">Open a browser and navigate to [Microsoft Power Automate](https://flow.microsoft.com).</span></span> <span data-ttu-id="b583f-108">Office 365 テナント管理者アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="b583f-108">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="b583f-109">左側のメニューで [ **データ** ] を選択し、ドロップダウンメニューの [ **カスタムコネクタ** ] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-109">Choose **Data** on the left-hand side menu, and select the **Custom Connectors** item in the drop-down menu.</span></span>

![Microsoft Power 自動化のドロップダウンメニューのスクリーンショット](./images/custom-connectors.png)

<span data-ttu-id="b583f-111">[ **カスタムコネクタ** ] ページの右上にある [ **新しいカスタムコネクタ** ] リンクを選択し、ドロップダウンメニュー **から [空のアイテムを作成** する] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-111">On the **Custom Connectors** page choose the **New custom connector** link in the top right, then select the **Create from blank** item in the drop-down menu.</span></span>

![Microsoft Power 自動化の新しいカスタムコネクタドロップダウンメニューのスクリーンショット](./images/new-connector.png)

<span data-ttu-id="b583f-113">[ `MS Graph Batch Connector` **コネクタ名** ] テキストボックスにを入力します。</span><span class="sxs-lookup"><span data-stu-id="b583f-113">Enter `MS Graph Batch Connector` in the **Connector name** text box.</span></span> <span data-ttu-id="b583f-114">Choose **Continue**.</span><span class="sxs-lookup"><span data-stu-id="b583f-114">Choose **Continue**.</span></span>

<span data-ttu-id="b583f-115">[コネクタ構成の **全般** ] ページで、フィールドに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="b583f-115">On the connector configuration **General** page, fill in the fields as follows.</span></span>

- <span data-ttu-id="b583f-116">**スキーム**: HTTPS</span><span class="sxs-lookup"><span data-stu-id="b583f-116">**Scheme**: HTTPS</span></span>
- <span data-ttu-id="b583f-117">**ホスト**: `graph.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="b583f-117">**Host**: `graph.microsoft.com`</span></span>
- <span data-ttu-id="b583f-118">**ベース URL**: `/`</span><span class="sxs-lookup"><span data-stu-id="b583f-118">**Base URL**: `/`</span></span>

<span data-ttu-id="b583f-119">[ **セキュリティ** ] ボタンを選択して続行します。</span><span class="sxs-lookup"><span data-stu-id="b583f-119">Choose **Security** button to continue.</span></span>

![コネクタ構成の [全般] タブのスクリーンショット](./images/general-tab.png)

<span data-ttu-id="b583f-121">[ **セキュリティ** ] ページで、フィールドに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="b583f-121">On the **Security** page, fill in the fields as follows.</span></span>

- <span data-ttu-id="b583f-122">**API によって実装されている認証を選択し**ます。 `OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="b583f-122">**Choose what authentication is implemented by your API**: `OAuth 2.0`</span></span>
- <span data-ttu-id="b583f-123">**Id プロバイダー**: `Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="b583f-123">**Identity Provider**: `Azure Active Directory`</span></span>
- <span data-ttu-id="b583f-124">**クライアント id**: 前の手順で作成したアプリケーション id</span><span class="sxs-lookup"><span data-stu-id="b583f-124">**Client id**: the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="b583f-125">**クライアントシークレット**: 前の手順で作成したキー</span><span class="sxs-lookup"><span data-stu-id="b583f-125">**Client secret**: the key you created in the previous exercise</span></span>
- <span data-ttu-id="b583f-126">**ログイン url**: `https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="b583f-126">**Login url**: `https://login.windows.net`</span></span>
- <span data-ttu-id="b583f-127">**テナント ID**: `common`</span><span class="sxs-lookup"><span data-stu-id="b583f-127">**Tenant ID**: `common`</span></span>
- <span data-ttu-id="b583f-128">**リソース URL**: `https://graph.microsoft.com` (末尾がありません)</span><span class="sxs-lookup"><span data-stu-id="b583f-128">**Resource URL**: `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="b583f-129">**範囲**: 空白のままにする</span><span class="sxs-lookup"><span data-stu-id="b583f-129">**Scope**: Leave blank</span></span>

<span data-ttu-id="b583f-130">[ **定義** ] ボタンを選択して続行します。</span><span class="sxs-lookup"><span data-stu-id="b583f-130">Choose **Definition** button to continue.</span></span>

![コネクタ構成の [セキュリティ] タブのスクリーンショット](./images/security-tab.png)

<span data-ttu-id="b583f-132">[ **定義** ] ページで、[ **新しいアクション** ] を選択し、フィールドに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="b583f-132">On the **Definition** page, select **New Action** and fill in the fields as follows.</span></span>

- <span data-ttu-id="b583f-133">**概要**: `Batch`</span><span class="sxs-lookup"><span data-stu-id="b583f-133">**Summary**: `Batch`</span></span>
- <span data-ttu-id="b583f-134">**説明**: `Execute Batch with Delegate Permission`</span><span class="sxs-lookup"><span data-stu-id="b583f-134">**Description**: `Execute Batch with Delegate Permission`</span></span>
- <span data-ttu-id="b583f-135">**操作 ID**: `Batch`</span><span class="sxs-lookup"><span data-stu-id="b583f-135">**Operation ID**: `Batch`</span></span>
- <span data-ttu-id="b583f-136">**表示**: `important`</span><span class="sxs-lookup"><span data-stu-id="b583f-136">**Visibility**: `important`</span></span>

![コネクタ構成の [定義] タブのスクリーンショット](./images/definition-tab.png)

<span data-ttu-id="b583f-138">[ **Sample からインポート**] を選択し、フィールドに次のように入力して**要求**を作成します。</span><span class="sxs-lookup"><span data-stu-id="b583f-138">Create **Request** by selecting **Import from Sample** and fill in the fields as follows.</span></span>

- <span data-ttu-id="b583f-139">**動詞**: `POST`</span><span class="sxs-lookup"><span data-stu-id="b583f-139">**Verb**: `POST`</span></span>
- <span data-ttu-id="b583f-140">**URL**: `https://graph.microsoft.com/v1.0/$batch`</span><span class="sxs-lookup"><span data-stu-id="b583f-140">**URL**: `https://graph.microsoft.com/v1.0/$batch`</span></span>
- <span data-ttu-id="b583f-141">**ヘッダー**: 空白のままにする</span><span class="sxs-lookup"><span data-stu-id="b583f-141">**Headers**: Leave blank</span></span>
- <span data-ttu-id="b583f-142">**本文**: `{}`</span><span class="sxs-lookup"><span data-stu-id="b583f-142">**Body**: `{}`</span></span>

<span data-ttu-id="b583f-143">**[インポート]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-143">Select **Import**.</span></span>

![コネクタ構成の [インポート元サンプル] ダイアログのスクリーンショット](./images/import-sample.png)

<span data-ttu-id="b583f-145">右上にある [ **コネクタの作成** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-145">Choose **Create Connector** on the top-right.</span></span> <span data-ttu-id="b583f-146">コネクタが作成されたら、[**セキュリティ**] ページから、生成された**リダイレクト URL**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="b583f-146">After the connector has been created, copy the generated **Redirect URL** from **Security** page.</span></span>

![生成されたリダイレクト URL のスクリーンショット](./images/redirect-url.png)

<span data-ttu-id="b583f-148">前の手順で作成した [Azure Portal](https://aad.portal.azure.com) の登録済みアプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="b583f-148">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="b583f-149">左側のメニューで [ **認証** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-149">Select **Authentication** on the left-hand side menu.</span></span> <span data-ttu-id="b583f-150">**[プラットフォームを追加]** を選択して、**[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-150">Select **Add a platform**, then select **Web**.</span></span> <span data-ttu-id="b583f-151">**リダイレクト uri**の前の手順でコピーしたリダイレクト URL を入力し、[**構成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-151">Enter the redirect URL copied from the previous step in the **Redirect URIs**, then select **Configure**.</span></span>

![Azure portal の応答 Url ブレードのスクリーンショット](./images/update-app-reg.png)

## <a name="option-2-create-custom-connector-by-importing-openapi-file"></a><span data-ttu-id="b583f-153">オプション 2: OpenAPI ファイルをインポートしてカスタムコネクタを作成する</span><span class="sxs-lookup"><span data-stu-id="b583f-153">Option 2: Create custom connector by importing OpenAPI file</span></span>

<span data-ttu-id="b583f-154">テキストエディターを使用して、という名前の新しい空のファイルを作成 `MSGraph-Delegate-Batch.swagger.json` し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="b583f-154">Using a text editor, create a new empty file named `MSGraph-Delegate-Batch.swagger.json` and add the following code.</span></span>

[!code-json[](../LabFiles/MSGraph-Delegate-Batch.swagger.json)]

<span data-ttu-id="b583f-155">ブラウザーを開き、[ [Microsoft Power オートメーション](https://flow.microsoft.com)] に移動します。</span><span class="sxs-lookup"><span data-stu-id="b583f-155">Open a browser and navigate to [Microsoft Power Automate](https://flow.microsoft.com).</span></span> <span data-ttu-id="b583f-156">Office 365 テナント管理者アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="b583f-156">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="b583f-157">左側のメニューで [ **データ** ] を選択し、ドロップダウンメニューの [ **カスタムコネクタ** ] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-157">Choose **Data** on the left-hand side menu, and select the **Custom Connectors** item in the drop-down menu.</span></span>

<span data-ttu-id="b583f-158">[ **カスタムコネクタ** ] ページの右上にある [ **新しいカスタムコネクタ** ] リンクを選択し、ドロップダウンメニューから [ **openapi ファイルをインポートする** ] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-158">On the **Custom Connectors** page choose the **New custom connector** link in the top right, then select the **Import an OpenAPI file** item in the drop-down menu.</span></span>

<span data-ttu-id="b583f-159">[ `MS Graph Batch Connector` **コネクタ名** ] テキストボックスにを入力します。</span><span class="sxs-lookup"><span data-stu-id="b583f-159">Enter `MS Graph Batch Connector` in the **Connector name** text box.</span></span> <span data-ttu-id="b583f-160">[フォルダー] アイコンを選択して、OpenAPI ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="b583f-160">Choose the folder icon to upload the OpenAPI file.</span></span> <span data-ttu-id="b583f-161">作成したファイルを参照し `MSGraph-Delegate-Batch.swagger.json` ます。</span><span class="sxs-lookup"><span data-stu-id="b583f-161">Browse to the `MSGraph-Delegate-Batch.swagger.json` file you created.</span></span> <span data-ttu-id="b583f-162">[ **続行** ] を選択して、openapi ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="b583f-162">Choose **Continue** to upload the OpenAPI file.</span></span>

<span data-ttu-id="b583f-163">[コネクタの構成] ページで、ナビゲーションメニューの [ **セキュリティ** ] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-163">On the connector configuration page, choose the **Security** link in the navigation menu.</span></span> <span data-ttu-id="b583f-164">フィールドに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="b583f-164">Fill in the fields as follows.</span></span>

- <span data-ttu-id="b583f-165">**API によって実装されている認証を選択し**ます。 `OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="b583f-165">**Choose what authentication is implemented by your API**: `OAuth 2.0`</span></span>
- <span data-ttu-id="b583f-166">**Id プロバイダー**: `Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="b583f-166">**Identity Provider**: `Azure Active Directory`</span></span>
- <span data-ttu-id="b583f-167">**クライアント id**: 前の手順で作成したアプリケーション id</span><span class="sxs-lookup"><span data-stu-id="b583f-167">**Client id**: the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="b583f-168">**クライアントシークレット**: 前の手順で作成したキー</span><span class="sxs-lookup"><span data-stu-id="b583f-168">**Client secret**: the key you created in the previous exercise</span></span>
- <span data-ttu-id="b583f-169">**ログイン url**: `https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="b583f-169">**Login url**: `https://login.windows.net`</span></span>
- <span data-ttu-id="b583f-170">**テナント ID**: `common`</span><span class="sxs-lookup"><span data-stu-id="b583f-170">**Tenant ID**: `common`</span></span>
- <span data-ttu-id="b583f-171">**リソース URL**: `https://graph.microsoft.com` (末尾がありません)</span><span class="sxs-lookup"><span data-stu-id="b583f-171">**Resource URL**: `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="b583f-172">**範囲**: 空白のままにする</span><span class="sxs-lookup"><span data-stu-id="b583f-172">**Scope**: Leave blank</span></span>

<span data-ttu-id="b583f-173">右上にある [ **コネクタの作成** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-173">Choose **Create Connector** on the top-right.</span></span> <span data-ttu-id="b583f-174">コネクタが作成されたら、生成された **リダイレクト URL**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="b583f-174">After the connector has been created, copy the generated **Redirect URL**.</span></span>

![生成されたリダイレクト URL のスクリーンショット](./images/redirect-url.png)

<span data-ttu-id="b583f-176">前の手順で作成した [Azure Portal](https://aad.portal.azure.com) の登録済みアプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="b583f-176">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="b583f-177">左側のメニューで [ **認証** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-177">Select **Authentication** on the left-hand side menu.</span></span> <span data-ttu-id="b583f-178">**[プラットフォームを追加]** を選択して、**[Web]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-178">Select **Add a platform**, then select **Web**.</span></span> <span data-ttu-id="b583f-179">**リダイレクト uri**の前の手順でコピーしたリダイレクト URL を入力し、[**構成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b583f-179">Enter the redirect URL copied from the previous step in the **Redirect URIs**, then select **Configure**.</span></span>

![Azure portal の応答 Url ブレードのスクリーンショット](./images/update-app-reg.png)