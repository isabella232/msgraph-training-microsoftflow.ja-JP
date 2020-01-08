<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="af7c7-101">この演習では、フローまたは Azure ロジックアプリで使用できる新しいカスタムコネクタを作成します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-101">In this exercise, you will create a new custom connector which can be used in Flow or in Azure Logic Apps.</span></span> <span data-ttu-id="af7c7-102">Open API 定義ファイルには、Microsoft Graph `$batch`エンドポイントの正しいパスと、簡易インポートを有効にするための追加設定があらかじめ用意されています。</span><span class="sxs-lookup"><span data-stu-id="af7c7-102">The Open API definition file is prebuilt with the correct path for the Microsoft Graph `$batch` endpoint and additional settings to enable simple import.</span></span>

<span data-ttu-id="af7c7-103">テキストエディターを使用して、という名前`MSGraph-Delegate-Batch.swagger.json`の新しい空のファイルを作成し、次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-103">Using a text editor, create a new empty file named `MSGraph-Delegate-Batch.swagger.json` and add the following code.</span></span>

[!code-json[](../LabFiles/MSGraph-Delegate-Batch.swagger.json)]

<span data-ttu-id="af7c7-104">ブラウザーを開き、[ [Microsoft Flow](https://flow.microsoft.com)] に移動します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-104">Open a browser and navigate to [Microsoft Flow](https://flow.microsoft.com).</span></span> <span data-ttu-id="af7c7-105">Office 365 テナント管理者アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="af7c7-105">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="af7c7-106">左側のメニューで [**データ**] を展開し、[**カスタムコネクタ**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-106">In the left-hand menu, expand **Data** and choose **Custom connectors**.</span></span>

![Microsoft Flow のカスタムコネクタメニュー項目のスクリーンショット](./images/flow-conn1.png)

<span data-ttu-id="af7c7-108">[**カスタムコネクタ**] ページの右上にある [**新しいカスタムコネクタ**] リンクを選択し、ドロップダウンメニューから [ **openapi ファイルをインポートする**] 項目を選択します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-108">On the **Custom connectors** page choose the **New custom connector** link in the top right, then select the **Import an OpenAPI file** item in the drop-down menu.</span></span> <span data-ttu-id="af7c7-109">[ `MS Graph Batch Connector` **コネクタ名**] テキストボックスにを入力します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-109">Enter `MS Graph Batch Connector` in the **Connector name** text box.</span></span> <span data-ttu-id="af7c7-110">[**インポート**] ボタンを選択して、開いている API ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="af7c7-110">Choose **Import** button to upload the Open API file.</span></span> <span data-ttu-id="af7c7-111">作成した`MSGraph-Delegate-Batch.swagger.json`ファイルを参照します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-111">Browse to the `MSGraph-Delegate-Batch.swagger.json` file you created.</span></span> <span data-ttu-id="af7c7-112">[**続行**] を選択して、openapi ファイルをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="af7c7-112">Choose **Continue** to upload the OpenAPI file.</span></span>

 ![[カスタムコネクタの作成] ダイアログのスクリーンショット](./images/flow-conn3.png)

<span data-ttu-id="af7c7-114">[コネクタの構成] ページで、ナビゲーションメニューの [**セキュリティ**] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-114">On the connector configuration page, choose the **Security** link in the navigation menu.</span></span> <span data-ttu-id="af7c7-115">フィールドに次のように入力します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-115">Fill in the fields as follows.</span></span>

- <span data-ttu-id="af7c7-116">**API によって実装されている認証を選択し**ます。`OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="af7c7-116">**Choose what authentication is implemented by your API**: `OAuth 2.0`</span></span>
- <span data-ttu-id="af7c7-117">**Id プロバイダー**:`Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="af7c7-117">**Identity Provider**: `Azure Active Directory`</span></span>
- <span data-ttu-id="af7c7-118">**クライアント id**: 前の手順で作成したアプリケーション id</span><span class="sxs-lookup"><span data-stu-id="af7c7-118">**Client id**: the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="af7c7-119">**クライアントシークレット**: 前の手順で作成したキー</span><span class="sxs-lookup"><span data-stu-id="af7c7-119">**Client secret**: the key you created in the previous exercise</span></span>
- <span data-ttu-id="af7c7-120">**ログイン url**:`https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="af7c7-120">**Login url**: `https://login.windows.net`</span></span>
- <span data-ttu-id="af7c7-121">**テナント ID**:`common`</span><span class="sxs-lookup"><span data-stu-id="af7c7-121">**Tenant ID**: `common`</span></span>
- <span data-ttu-id="af7c7-122">**リソース URL**: `https://graph.microsoft.com` (末尾がありません)</span><span class="sxs-lookup"><span data-stu-id="af7c7-122">**Resource URL**: `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="af7c7-123">**範囲**: 空白のままにする</span><span class="sxs-lookup"><span data-stu-id="af7c7-123">**Scope**: Leave blank</span></span>

<span data-ttu-id="af7c7-124">右上の [**コネクタの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-124">Choose **Create Connector** on the top-right</span></span>

![コネクタ構成の [セキュリティ] タブのスクリーンショット](./images/flow-conn4.png)

<span data-ttu-id="af7c7-126">コネクタが作成されたら、生成された**リダイレクト URL**をコピーします。</span><span class="sxs-lookup"><span data-stu-id="af7c7-126">After the connector has been created, copy the generated **Redirect URL**.</span></span>

![生成されたリダイレクト URL のスクリーンショット](./images/flow-conn5.png)

<span data-ttu-id="af7c7-128">前の手順で作成した[Azure Portal](https://aad.portal.azure.com)の登録済みアプリケーションに戻ります。</span><span class="sxs-lookup"><span data-stu-id="af7c7-128">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="af7c7-129">**MS Graph バッチアプリ**ブレードの [**概要**] を選択し、[**リダイレクト URI の追加**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-129">Select **Overview** on the **MS Graph Batch App** blade, then select **Add a Redirect URI**.</span></span> <span data-ttu-id="af7c7-130">**リダイレクト URI**フィールドにコピーした**リダイレクト URL**を追加し、[**保存**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="af7c7-130">Add the **Redirect URL** you copied in the **Redirect URI** field and choose **Save**.</span></span>

![Azure portal の応答 Url ブレードのスクリーンショット](./images/flow-conn-preview6.png)
