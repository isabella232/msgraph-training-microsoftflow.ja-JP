<!-- markdownlint-disable MD002 MD041 -->

この演習では、カスタムコネクタに対して委任されたアクセス許可を提供するために使用される新しい Azure Active Directory アプリケーションを作成します。

ブラウザーを開き、 [Azure Active Directory 管理センター](https://aad.portal.azure.com)に移動します。 左側のナビゲーションメニューで [ **azure active directory** ] リンクを選択し、 **azure active directory**ブレードの [**管理**] セクションで [**アプリの登録 (プレビュー)** ] を選択します。

![azure active directory 管理センターの azure active directory ブレードのスクリーンショット](./images/app-reg-preview1.png)

**アプリ登録 (プレビュー)** ブレードの上部にある [**新しい登録**] メニュー項目を選択します。

![Azure Active Directory 管理センターのアプリ登録ブレードのスクリーンショット](./images/app-reg-preview2.png)

[ `MS Graph Batch App` **名前**] フィールドにを入力します。 [**サポートされているアカウントの種類**] セクションで、**任意の組織ディレクトリの [アカウント**] を選択します。 [**リダイレクト URI** ] セクションを空白のままにして、[**登録**] を選択します。

![Azure Active Directory 管理センターでアプリケーションブレードを登録するスクリーンショット](./images/app-reg-preview3.png)

**MS Graph バッチアプリ**ブレードで、**アプリケーション (クライアント) ID**をコピーします。 次の手順でこれを行う必要があります。

![登録済みアプリケーションページのスクリーンショット](./images/app-reg-preview4.png)

**MS Graph バッチアプリ**ブレードの [**管理**] セクションで、 **API アクセス許可**エントリを選択します。 [ **API アクセス許可**] の下で [**アクセス許可の追加**] を選択します。

![API アクセス許可ブレードのスクリーンショット](./images/app-perms-preview1.png)

[ **API アクセス許可の要求**] ブレードで、 **Microsoft Graph**を選択し、[委任された**アクセス許可**] を選択します。 [検索`group`] を選択し、[**すべてのグループの読み取りと書き込み**] アクセス許可を選択します。 ブレードの下部にある [**アクセス許可の追加**] を選択します。

 ![API アクセス許可ブレードの要求のスクリーンショット](./images/app-perms-preview2.png)

**MS Graph バッチアプリ**ブレードの [**管理**] セクションで、[**証明書と秘密**] エントリを選択し、[**新しいクライアントシークレット**] を選択します。 説明`forever`にを**** 入力し、[**期限切れ**] の下で [**なし**] を選択します。 [**追加**] をクリックします。

![証明書とシークレットブレードのスクリーンショット](./images/app-key-preview1.png)

新しいキーのキー値をコピーします。 次の手順でこれを行う必要があります。

![新しいクライアントシークレットのスクリーンショット](./images/app-key-preview2.png)

> [!IMPORTANT]
> この手順は、このブレードを閉じるとキーにアクセスできなくなるため、重要です。 このキーを、今後の演習で使用するテキストエディターに保存します。

Teams プロパティなど、Microsoft Graph からアクセスできる追加のサービスの管理を有効にするには、特定のサービスの管理を有効にするために、追加の適切なスコープを選択する必要があります。 たとえば、OneNote ノートブックまたはプランナープラン、バケット、タスクの作成を可能にするソリューションを拡張するには、関連する api に必要なアクセス許可スコープを追加する必要があります。