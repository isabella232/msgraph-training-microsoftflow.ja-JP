<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1272d-101">新しいコネクタを使用するフローを作成する前に、 [Microsoft Graph エクスプローラ](https://developer.microsoft.com/graph/graph-explorer)を使用して、microsoft graph での JSON バッチの機能の一部を確認してください。</span><span class="sxs-lookup"><span data-stu-id="1272d-101">Before creating a Flow to consume the new connector, use [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to discover some of the capabilities and features of JSON batching in Microsoft Graph.</span></span>

<span data-ttu-id="1272d-102">ブラウザーで[Microsoft Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を開きます。</span><span class="sxs-lookup"><span data-stu-id="1272d-102">Open the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in your browser.</span></span> <span data-ttu-id="1272d-103">Office 365 テナント管理者アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="1272d-103">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="1272d-104">左側のナビゲーションウィンドウの [**その他のサンプルを表示**する] リンクを選択し、**バッチ**処理および**Microsoft Teams (ベータ)** のサンプルを**オン**に切り替えます。</span><span class="sxs-lookup"><span data-stu-id="1272d-104">Choose the **show more samples** link in the left navigation pane, and toggle the samples for **Batching** and **Microsoft Teams (beta)** to **On**.</span></span>

![Graph エクスプローラで [その他のサンプルを表示] ダイアログボックスのスクリーンショット](./images/graph-explore1.png)

<span data-ttu-id="1272d-106">左側のメニューで、[**並列実行**] サンプルクエリを選択します。</span><span class="sxs-lookup"><span data-stu-id="1272d-106">Select the **Perform parallel GETs** sample query in the left menu.</span></span> <span data-ttu-id="1272d-107">画面の右上にある [**クエリの実行**] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="1272d-107">Choose the **Run Query** button at the top right of the screen.</span></span>

<span data-ttu-id="1272d-108">サンプルのバッチ操作は、3つの HTTP GET 要求をバッチ処理して`/v1.0/$batch` 、Graph エンドポイントに対する1つの http POST を発行します。</span><span class="sxs-lookup"><span data-stu-id="1272d-108">The sample batch operation batches three HTTP GET requests and issues a single HTTP POST to the `/v1.0/$batch` Graph endpoint.</span></span>

```json
{
  "requests": [
    {
      "url": "/me?$select=displayName,jobTitle,userPrincipalName",
      "method": "GET",
      "id": "1"
    },
    {
      "url": "/me/messages?$filter=importance eq 'high'&$select=from,subject,receivedDateTime,bodyPreview",
      "method": "GET",
      "id": "2"
    },
    {
      "url": "/me/events",
      "method": "GET",
      "id": "3"
    }
  ]
}
```

<span data-ttu-id="1272d-109">返された応答は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="1272d-109">The response returned is shown below.</span></span> <span data-ttu-id="1272d-110">Microsoft Graph によって返される応答の配列をメモします。</span><span class="sxs-lookup"><span data-stu-id="1272d-110">Note the array of responses that is returned by Microsoft Graph.</span></span> <span data-ttu-id="1272d-111">バッチ処理された要求に対する応答は、投稿の要求の順序とは別の順序で表示されることがあります。</span><span class="sxs-lookup"><span data-stu-id="1272d-111">The responses to the batched requests may appear in a different order than the order of the requests in the POST.</span></span> <span data-ttu-id="1272d-112">この`id`プロパティを使用して、個々のバッチ要求と特定のバッチ応答を関連付けます。</span><span class="sxs-lookup"><span data-stu-id="1272d-112">The `id` property should be used to correlate individual batch requests with specific batch responses.</span></span>

> [!NOTE]
> <span data-ttu-id="1272d-113">読みやすくするために、応答は切り詰められています。</span><span class="sxs-lookup"><span data-stu-id="1272d-113">The response has been truncated for readability.</span></span>

```json
{
  "responses": [
    {
      "id": "1",
      "status": 200,
      "headers": {...},
      "body": {...}
    },
    {
      "id": "3",
      "status": 200,
      "headers": {...},
      "body": {...}
    }
    {
      "id": "2",
      "status": 200,
      "headers": {...},
      "body": {...}
    }
  ]
}
```

<span data-ttu-id="1272d-114">各応答には`id` `status`、、 `headers`、、 `body`およびプロパティが含まれます。</span><span class="sxs-lookup"><span data-stu-id="1272d-114">Each response contains an `id`, `status`, `headers`, and `body` property.</span></span> <span data-ttu-id="1272d-115">要求の`status`プロパティがエラーを示している場合、 `body`には、要求から返されたエラー情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1272d-115">If the `status` property for a request indicates a failure, the `body` contains any error information returned from the request.</span></span>

<span data-ttu-id="1272d-116">要求の操作の順序を確認するには、 [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property)プロパティを使用して個々の要求を順序付けできます。</span><span class="sxs-lookup"><span data-stu-id="1272d-116">To ensure an order of operations for the requests, individual requests can be sequenced using the [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) property.</span></span>

<span data-ttu-id="1272d-117">JSON バッチは、シーケンス処理および依存操作に加えて、基本パスを想定し、相対パスからの要求を実行します。</span><span class="sxs-lookup"><span data-stu-id="1272d-117">In addition to sequencing and dependency operations, JSON batching assumes a base path and executes the requests from a relative path.</span></span> <span data-ttu-id="1272d-118">各 batch 要求要素は、指定され`/v1.0/$batch`た`/beta/$batch`とおりにまたはのいずれかのエンドポイントから実行されます。</span><span class="sxs-lookup"><span data-stu-id="1272d-118">Each batch request element is executed from either the `/v1.0/$batch` OR `/beta/$batch` endpoints as specified.</span></span> <span data-ttu-id="1272d-119">エンドポイントでは、エンドポイント`/beta`に返されない追加の出力が返される可能性が`/v1.0`あるため、これには大きな違いがあります。</span><span class="sxs-lookup"><span data-stu-id="1272d-119">This can have significant differences as the `/beta` endpoint may return additional output which may NOT be returned in the `/v1.0` endpoint.</span></span>

<span data-ttu-id="1272d-120">たとえば、 [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)で次の2つのクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="1272d-120">For example, execute the following two queries in the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).</span></span>

1. <span data-ttu-id="1272d-121">Url `/me`を`/v1.0/$batch`使用してエンドポイントに対してクエリを実行します (以下のコピーと貼り付け要求)。</span><span class="sxs-lookup"><span data-stu-id="1272d-121">Query the `/v1.0/$batch` endpoint using the url `/me` (copy and paste request below).</span></span>

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/me",
      "method": "GET"
    }
  ]
}
```

![V 1.0 が選択された状態での Graph Explorer のバッチクエリのスクリーンショット](./images/graph-explore3.png)

<span data-ttu-id="1272d-123">次に、バージョン選択ドロップダウンを使用して`beta`エンドポイントに変更し、まったく同じ要求を行います。</span><span class="sxs-lookup"><span data-stu-id="1272d-123">Now use the version selector drop-down to change to the `beta` endpoint, and make the exact same request.</span></span>

![グラフ-4](./images/graph-explore4.png)

<span data-ttu-id="1272d-125">返される結果の違いは何ですか。</span><span class="sxs-lookup"><span data-stu-id="1272d-125">What are the differences in the results returned?</span></span> <span data-ttu-id="1272d-126">いくつかの相違点を特定するには、他のクエリを試してみてください。</span><span class="sxs-lookup"><span data-stu-id="1272d-126">Try some other queries to identify some of the differences.</span></span>

<span data-ttu-id="1272d-127">`/v1.0`および`/beta`エンドポイントからの応答コンテンツに加えて、アクセス許可が付与されていないバッチ要求が行われた場合のエラーについて理解することが重要です。</span><span class="sxs-lookup"><span data-stu-id="1272d-127">In addition to different response content from the `/v1.0` and `/beta` endpoints, it is important to understand the possible errors when a batch request is made for which permission consent has not been granted.</span></span> <span data-ttu-id="1272d-128">たとえば、次に示すのは、OneNote ノートブックを作成するためのバッチ要求アイテムです。</span><span class="sxs-lookup"><span data-stu-id="1272d-128">For example, the following is a batch request item to create a OneNote Notebook.</span></span>

```json
{
  "id": 1,
  "url": "/groups/65c5ecf9-3311-449c-9904-29a2c76b9a50/onenote/notebooks",
  "headers": {
    "Content-Type": "application/json"
  },
  "method": "POST",
  "body": {
    "displayName": "Meeting Notes"
  }
}
```

<span data-ttu-id="1272d-129">ただし、OneNote ノートブックを作成するためのアクセス許可が付与されていない場合は、次の応答が受信されます。</span><span class="sxs-lookup"><span data-stu-id="1272d-129">However, if the permissions to create OneNote Notebooks has not been granted, the following response is received.</span></span> <span data-ttu-id="1272d-130">状態コード`403 (Forbidden)`と、指定された OAuth トークンを示すエラーメッセージには、要求された操作を完了するために必要なスコープが含まれていないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="1272d-130">Note the status code `403 (Forbidden)` and the error message which indicates the OAuth token provided does not include the scopes required to completed the requested action.</span></span>

```json
{
  "responses": [
    {
      "id": "1",
      "status": 403,
      "headers": {
        "Cache-Control": "no-cache"
      },
      "body": {
        "error": {
          "code": "40004",
          "message": "The OAuth token provided does not have the necessary scopes to complete the request.
            Please make sure you are including one or more of the following scopes: Notes.ReadWrite.All,
            Notes.Read.All (you provided these scopes: Group.Read.All,Group.ReadWrite.All,User.Read,User.Read.All)",
          "innerError": {
            "request-id": "92d50317-aa06-4bd7-b908-c85ee4eff0e9",
            "date": "2018-10-17T02:01:10"
          }
        }
      }
    }
  ]
}
```

<span data-ttu-id="1272d-131">バッチ内の各要求は、状態コードと結果またはエラー情報を返します。</span><span class="sxs-lookup"><span data-stu-id="1272d-131">Each request in your batch will return a status code and results or error information.</span></span> <span data-ttu-id="1272d-132">各応答を処理して、個々のバッチ操作の成功または失敗を判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1272d-132">You must process each of the responses in order to determine success or failure of the individual batch operations.</span></span>
