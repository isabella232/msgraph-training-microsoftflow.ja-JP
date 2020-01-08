<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c4f96-101">この演習では、フローまたは Azure ロジックアプリで使用できる新しいカスタムコネクタを作成します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-101">In this exercise, you will create a new custom connector which can be used in Flow or in Azure Logic Apps.</span></span> <span data-ttu-id="c4f96-102">Open API 定義ファイルには、Microsoft Graph `$batch`エンドポイントの正しいパスと、簡易インポートを有効にするための追加設定があらかじめ用意されています。</span><span class="sxs-lookup"><span data-stu-id="c4f96-102">The Open API definition file is prebuilt with the correct path for the Microsoft Graph `$batch` endpoint and additional settings to enable simple import.</span></span>

<span data-ttu-id="c4f96-103">テキストエディターを使用して、という名前`MSGraph-Delegate-Batch.swagger.json`の新しい空のファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-103">Using a text editor, create a new empty file named `MSGraph-Delegate-Batch.swagger.json` and add the following code.</span></span>

[!code-json[](../LabFiles/MSGraph-Delegate-Batch.swagger.json)]

<span data-ttu-id="c4f96-104">ブラウザーを開き、[ [Microsoft Flow](https://flow.microsoft.com)] に移動します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-104">Open a browser and navigate to [Microsoft Flow](https://flow.microsoft.com).</span></span> <span data-ttu-id="c4f96-105">Office 365 テナント管理者アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="c4f96-105">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="c4f96-106">右上の歯車アイコンを選択し、ドロップダウンメニューの [**カスタムコネクタ**] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-106">Choose the gear icon in the upper right, and select the **Custom Connectors** item in the drop-down menu.</span></span>

![Microsoft Flow のドロップダウンメニューのスクリーンショット](./images/flow-conn1.png)

<span data-ttu-id="c4f96-108">[**カスタムコネクタ**] ページの右上にある [**カスタムコネクタの作成**] リンクを選択し、ドロップダウンメニューの [開いている**API ファイルをインポート**する] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-108">On the **Custom Connectors** page choose the **Create custom connector** link in the top right, then select the **Import an Open API file** item in the drop-down menu.</span></span>

 ![Microsoft Flow の [カスタムコネクタの作成] ドロップダウンメニューのスクリーンショット](./images/flow-conn2.png)

<span data-ttu-id="c4f96-110">[ `MS Graph Batch Connector` **カスタムコネクタ名**] テキストボックスにを入力します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-110">Enter `MS Graph Batch Connector` in the **Custom connector name** text box.</span></span> <span data-ttu-id="c4f96-111">[フォルダー] アイコンを選択して、開いている API ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="c4f96-111">Choose the folder icon to upload the Open API file.</span></span> <span data-ttu-id="c4f96-112">作成した`MSGraph-Delegate-Batch.swagger.json`ファイルを参照します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-112">Browse to the `MSGraph-Delegate-Batch.swagger.json` file you created.</span></span> <span data-ttu-id="c4f96-113">[**続行**] を選択して、開いている API ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="c4f96-113">Choose **Continue** to upload the Open API file.</span></span>

 ![[カスタムコネクタの作成] ダイアログのスクリーンショット](./images/flow-conn3.png)

<span data-ttu-id="c4f96-115">[コネクタの構成] ページで、ナビゲーションメニューの [**セキュリティ**] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-115">On the connector configuration page, choose the **Security** link in the navigation menu.</span></span> <span data-ttu-id="c4f96-116">フィールドに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-116">Fill in the fields as follows.</span></span>

- <span data-ttu-id="c4f96-117">**API によって実装されている認証を選択し**ます。`OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="c4f96-117">**Choose what authentication is implemented by your API**: `OAuth 2.0`</span></span>
- <span data-ttu-id="c4f96-118">**Id プロバイダー**:`Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="c4f96-118">**Identity Provider**: `Azure Active Directory`</span></span>
- <span data-ttu-id="c4f96-119">**クライアント id**: 前の手順で作成したアプリケーション id</span><span class="sxs-lookup"><span data-stu-id="c4f96-119">**Client id**: the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="c4f96-120">**クライアントシークレット**: 前の手順で作成したキー</span><span class="sxs-lookup"><span data-stu-id="c4f96-120">**Client secret**: the key you created in the previous exercise</span></span>
- <span data-ttu-id="c4f96-121">**ログイン url**:`https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="c4f96-121">**Login url**: `https://login.windows.net`</span></span>
- <span data-ttu-id="c4f96-122">**テナント ID**:`common`</span><span class="sxs-lookup"><span data-stu-id="c4f96-122">**Tenant ID**: `common`</span></span>
- <span data-ttu-id="c4f96-123">**リソース URL**: `https://graph.microsoft.com` (末尾がありません)</span><span class="sxs-lookup"><span data-stu-id="c4f96-123">**Resource URL**: `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="c4f96-124">**範囲**: 空白のままにする</span><span class="sxs-lookup"><span data-stu-id="c4f96-124">**Scope**: Leave blank</span></span>

<span data-ttu-id="c4f96-125">右上の [**コネクタの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-125">Choose **Create Connector** on the top-right</span></span>

![コネクタ構成の [セキュリティ] タブのスクリーンショット](./images/flow-conn4.png)

<span data-ttu-id="c4f96-127">コネクタが作成されたら、生成された**リダイレクト URL**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="c4f96-127">After the connector has been created, copy the generated **Redirect URL**.</span></span>

![生成されたリダイレクト URL のスクリーンショット](./images/flow-conn5.png)

<span data-ttu-id="c4f96-129">前の手順で作成した[Azure Portal](https://aad.portal.azure.com)の登録済みアプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="c4f96-129">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="c4f96-130">[**設定**] ブレードで [**返信 url** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-130">Select **Reply URLs** in the **Settings** blade.</span></span> <span data-ttu-id="c4f96-131">コピーした**リダイレクト url**を、追加の**応答 url**として追加します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-131">Add the **Redirect URL** you copied as an additional **Reply URL**.</span></span> <span data-ttu-id="c4f96-132">Azure Active Directory ポータルにアプリケーションを保存します。</span><span class="sxs-lookup"><span data-stu-id="c4f96-132">Save the application in Azure Active Directory portal.</span></span>

![Azure portal の応答 Url ブレードのスクリーンショット](./images/flow-conn6.png)
