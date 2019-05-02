<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="aa89e-101">この演習では、前の手順で作成したカスタムコネクタを使用して Microsoft teams を作成して構成するフローを作成します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-101">In this exercise, you will create a Flow to use the custom connector you created in previous exercises to create and configure a Microsoft Team.</span></span> <span data-ttu-id="aa89e-102">このフローでは、カスタムコネクタを使用して、Office 365 統合グループを作成するために POST 要求を送信します。グループの作成が完了するまで待機し、その後、PUT 要求を送信して、グループを Microsoft チームに関連付けます。</span><span class="sxs-lookup"><span data-stu-id="aa89e-102">The Flow will use the custom connector to send a POST request to create an Office 365 Unified Group, will pause for a delay while the group creation completes, and then will send a PUT request to associate the group with a Microsoft Team.</span></span>

<span data-ttu-id="aa89e-103">最終的に、フローは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="aa89e-103">In the end your Flow will look similar to the following image:</span></span>

![完了したフローのスクリーンショット](./images/flow-team1.png)

<span data-ttu-id="aa89e-105">ブラウザーで[Microsoft Flow](https://flow.microsoft.com)を開き、Office 365 テナント管理者アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="aa89e-105">Open [Microsoft Flow](https://flow.microsoft.com) in your browser and sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="aa89e-106">左側のナビゲーションで [**マイフロー** ] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-106">Choose **My Flows** in the left-hand navigation.</span></span> <span data-ttu-id="aa89e-107">[**新規**作成] を選択し、[新規**作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-107">Choose **New**, then **Create from blank**.</span></span> <span data-ttu-id="aa89e-108">[**新規から作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-108">Choose **Create from blank**.</span></span> <span data-ttu-id="aa89e-109">検索`Manual`ボックスにを入力し、**手動でフロートリガーをトリガー**します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-109">Enter `Manual` in the search box and add the **Manually trigger a flow** trigger.</span></span>

<span data-ttu-id="aa89e-110">[**入力を追加**] を選択して`Name` 、[**テキスト**] を選択し、タイトルとしてを入力します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-110">Choose **Add an input**, select **Text** and enter `Name` as the title.</span></span>

![フロートリガーを手動でトリガーするスクリーンショット](./images/flow-team6.png)

<span data-ttu-id="aa89e-112">[**新しい手順**] を`Batch`選択し、検索ボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-112">Choose **New step** and type `Batch` in the search box.</span></span> <span data-ttu-id="aa89e-113">[ **MS Graph バッチコネクタ**] アクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-113">Add the **MS Graph Batch Connector** action.</span></span> <span data-ttu-id="aa89e-114">省略記号を選択して、この`Batch POST-groups`アクションの名前をに変更します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-114">Choose the ellipsis and rename this action to `Batch POST-groups`.</span></span>

<span data-ttu-id="aa89e-115">アクションの**本文**テキストボックスに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-115">Add the following code into the **body** text box of the action.</span></span>

```json
{
  "requests": [
    {
      "url": "/groups",
      "method": "POST",
      "id": 1,
      "headers": { "Content-Type": "application/json" },
      "body": {
        "description": "REPLACE",
        "displayName": "REPLACE",
        "groupTypes": ["Unified"],
        "mailEnabled": true,
        "mailNickname": "REPLACE",
        "securityEnabled": false
      }
    }
  ]
}
```

<span data-ttu-id="aa89e-116">[**動的コンテンツの追加**] `Name`メニューから手動トリガーの値を選択して、各`REPLACE`プレースホルダーを置き換えます。</span><span class="sxs-lookup"><span data-stu-id="aa89e-116">Replace each `REPLACE` placeholder by selecting the `Name` value from the manual trigger from the **Add dynamic content** menu.</span></span>

![Microsoft Flow の [動的コンテンツ] メニューのスクリーンショット](./images/flow-team2.png)

<span data-ttu-id="aa89e-118">[**新しい手順**] を選択`delay`し、**遅延**アクションを検索して追加して、1分間構成します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-118">Choose **New step**, search for `delay` and add a **Delay** action and configure for 1 minute.</span></span>

<span data-ttu-id="aa89e-119">[**新しい手順**] を`Batch`選択し、検索ボックスに入力します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-119">Choose **New step** and type `Batch` in the search box.</span></span> <span data-ttu-id="aa89e-120">[ **MS Graph バッチコネクタ**] アクションを追加します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-120">Add the **MS Graph Batch Connector** action.</span></span> <span data-ttu-id="aa89e-121">省略記号を選択して、この`Batch PUT-team`アクションの名前をに変更します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-121">Choose the ellipsis and rename this action to `Batch PUT-team`.</span></span>

<span data-ttu-id="aa89e-122">アクションの**本文**テキストボックスに次のコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-122">Add the following code into the **body** text box of the action.</span></span>

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/groups/REPLACE/team",
      "method": "PUT",
      "headers": {
        "Content-Type": "application/json"
      },
      "body": {
        "memberSettings": {
          "allowCreateUpdateChannels": true
        },
        "messagingSettings": {
          "allowUserEditMessages": true,
          "allowUserDeleteMessages": true
        },
        "funSettings": {
          "allowGiphy": true,
          "giphyContentRating": "strict"
        }
      }
    }
  ]
}
```

<span data-ttu-id="aa89e-123">`REPLACE`プレースホルダーを選択し、[動的コンテンツ] ウィンドウで [**式**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-123">Select the `REPLACE` placeholder, then select **Expression** in the dynamic content pane.</span></span> <span data-ttu-id="aa89e-124">次の数式を**式**に追加します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-124">Add the following formula into the **Expression**.</span></span>

```js
body('Batch_POST-groups').responses[0].body.id
```

![[動的コンテンツ] ウィンドウ内の式のスクリーンショット](./images/flow-formula.png)

<span data-ttu-id="aa89e-126">この式では、最初のアクションの結果からグループ ID を使用することを指定します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-126">This formula specifies that we want to use the group ID from the result of the first action.</span></span>

![更新されたアクション本文のスクリーンショット](./images/flow-team3.png)

<span data-ttu-id="aa89e-128">[**保存**] を選択してからフローを選択し、[**テスト**] を選択してフローを実行します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-128">Choose **Save**, then Flow and choose **Test** to execute the Flow.</span></span>

> [!TIP]
> <span data-ttu-id="aa89e-129">このような`The template validation failed: 'The action(s) 'Batch_POST-groups' referenced by 'inputs' in action 'Batch_2' are not defined in the template'`エラーが表示される場合は、式が正しくないため、検索できないフローアクションが参照されている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="aa89e-129">If you receive an error like `The template validation failed: 'The action(s) 'Batch_POST-groups' referenced by 'inputs' in action 'Batch_2' are not defined in the template'`, the expression is incorrect and likely references a Flow action it cannot find.</span></span> <span data-ttu-id="aa89e-130">参照しているアクション名が正確に一致することを確認します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-130">Ensure that the action name you are referencing matches exactly.</span></span>

<span data-ttu-id="aa89e-131">[トリガーアクションを**実行する**] ラジオボタンを選択し、[ **Save & Test**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-131">Choose the **I'll perform the trigger** action radio button and choose **Save & Test**.</span></span> <span data-ttu-id="aa89e-132">ダイアログの [**続行**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-132">Choose **Continue** in the dialog.</span></span> <span data-ttu-id="aa89e-133">スペースを含まない名前を指定し、[**実行フロー** ] を選択してチームを作成します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-133">Provide a name without spaces, and choose **Run flow** to create a Team.</span></span>

![[実行フロー] ダイアログのスクリーンショット](./images/flow-team4.png)

<span data-ttu-id="aa89e-135">最後に、[ **flow run アクティビティを参照して**ください] リンクを選択し、実行中のフローを選択してアクティビティログを表示します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-135">Finally, choose the **See flow run activity** link, then select the running Flow to see the activity log.</span></span>

> [!NOTE]
> <span data-ttu-id="aa89e-136">フローの実行を表示するには、[実行履歴] の一覧で実行中のフローインスタンスをクリックする必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="aa89e-136">You may have to click on your running Flow instance in the Run history list to view your Flow execution.</span></span>

<span data-ttu-id="aa89e-137">フローが完了すると、Office 365 グループとチームが構成されました。</span><span class="sxs-lookup"><span data-stu-id="aa89e-137">Once the Flow completes, your Office 365 Group and Team have been configured.</span></span> <span data-ttu-id="aa89e-138">バッチアクションアイテムを選択して、JSON バッチ呼び出しの結果を表示します。</span><span class="sxs-lookup"><span data-stu-id="aa89e-138">Select the Batch action items to view the results of the JSON Batch calls.</span></span> <span data-ttu-id="aa89e-139">アクションの状態コードは、 `outputs`次の図のようなチームの関連付けを成功させるために201の状態コードである必要があります。 `Batch PUT-team`</span><span class="sxs-lookup"><span data-stu-id="aa89e-139">The `outputs` of the `Batch PUT-team` action should have a status code of 201 for a successful Team association similar to the image below.</span></span>

![成功したフローアクティビティログのスクリーンショット](./images/flow-team5.png)