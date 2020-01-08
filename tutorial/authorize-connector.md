<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="25a6b-101">コネクタが使用できる状態になっていることを確認するための最後の構成手順は、キャッシュされた接続を作成するためにカスタムコネクタを承認およびテストすることです。</span><span class="sxs-lookup"><span data-stu-id="25a6b-101">The final configuration step to ensure the connector is ready for use is to authorize and test the custom connector to create a cached connection.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25a6b-102">次の手順では、管理者特権でログインしている必要があります。</span><span class="sxs-lookup"><span data-stu-id="25a6b-102">The following steps requires that you are logged in with administrator privileges.</span></span>

<span data-ttu-id="25a6b-103">[Microsoft Flow](https://flow.microsoft.com)で、[コネクタ構成] 画面に移動し、ナビゲーションメニューの [**テスト**] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="25a6b-103">In [Microsoft Flow](https://flow.microsoft.com), go to the Connector configuration screen and choose the **Test** link in the navigation menu.</span></span> <span data-ttu-id="25a6b-104">[**新しい接続**] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="25a6b-104">Choose the **New Connection** link.</span></span> <span data-ttu-id="25a6b-105">Office 365 テナント管理者の Azure Active Directory アカウントでサインインします。</span><span class="sxs-lookup"><span data-stu-id="25a6b-105">Sign in with your Office 365 tenant administrator's Azure Active Directory account.</span></span>

<span data-ttu-id="25a6b-106">要求されたアクセス許可の入力を求められたら、**組織に代わって同意**を確認し、[**同意**する] を選択してアクセス許可を承認します。</span><span class="sxs-lookup"><span data-stu-id="25a6b-106">When prompted for the requested permissions, check **Consent on behalf of your organization** and then choose **Accept** to authorize permissions.</span></span>

![アクセス許可のプロンプトのスクリーンショット](./images/flow-conn8.png)

<span data-ttu-id="25a6b-108">アクセス許可を承認すると、フローに接続が作成されます。</span><span class="sxs-lookup"><span data-stu-id="25a6b-108">After you authorize the permissions, a connection is created in Flow.</span></span>

![Microsoft Flow で作成された接続のスクリーンショット](./images/flow-conn9.png)

<span data-ttu-id="25a6b-110">これで、カスタムコネクタが構成され、有効になりました。</span><span class="sxs-lookup"><span data-stu-id="25a6b-110">The custom connector is now configured and enabled.</span></span> <span data-ttu-id="25a6b-111">アクセス許可が適用されて使用可能になるまでに遅延が発生することがありますが、コネクタは現在構成されています。</span><span class="sxs-lookup"><span data-stu-id="25a6b-111">There may be a delay in permissions being applied and available, but the connector is now configured.</span></span>
