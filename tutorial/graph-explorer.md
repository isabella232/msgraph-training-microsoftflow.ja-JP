<!-- markdownlint-disable MD002 MD041 -->

新しいコネクタを使用するフローを作成する前に、 [microsoft graph エクスプローラ](https://developer.microsoft.com/graph/graph-explorer)を使用して、microsoft graph での JSON バッチの機能の一部を確認してください。

ブラウザーで[Microsoft Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)を開きます。 Office 365 テナント管理者アカウントでサインインします。 左側のナビゲーションウィンドウの [**その他のサンプルを表示**する] リンクを選択し、**バッチ**処理および**Microsoft Teams (ベータ)** のサンプルを**オン**に切り替えます。

![Graph エクスプローラで [その他のサンプルを表示] ダイアログボックスのスクリーンショット](./images/graph-explore1.png)

左側のメニューで、[**並列実行**] サンプルクエリを選択します。 画面の右上にある [**クエリの実行**] ボタンをクリックします。

サンプルのバッチ操作は、3つの http GET 要求をバッチ処理して`/v1.0/$batch` 、Graph エンドポイントに対する1つの http POST を発行します。

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

返された応答は次のとおりです。 Microsoft Graph によって返される応答の配列をメモします。 バッチ処理された要求に対する応答は、投稿の要求の順序とは別の順序で表示されることがあります。 この`id`プロパティを使用して、個々のバッチ要求と特定のバッチ応答を関連付けます。

> [!NOTE]
> 読みやすくするために、応答は切り詰められています。

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

各応答には`id` `status`、、 `headers`、、 `body`およびプロパティが含まれます。 要求の`status`プロパティがエラーを示している場合、 `body`には、要求から返されたエラー情報が含まれています。

要求の操作の順序を確認するには、 [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property)プロパティを使用して個々の要求を順序付けできます。

JSON バッチは、シーケンス処理および依存操作に加えて、基本パスを想定し、相対パスからの要求を実行します。 各 batch 要求要素は、指定され`/v1.0/$batch`た`/beta/$batch`とおりにまたはのいずれかのエンドポイントから実行されます。 エンドポイントでは、エンドポイント`/beta`に返されない追加の出力が返される可能性が`/v1.0`あるため、これには大きな違いがあります。

たとえば、 [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)で次の2つのクエリを実行します。

1. url `/me`を`/v1.0/$batch`使用してエンドポイントに対してクエリを実行します (以下のコピーと貼り付け要求)。

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

![v 1.0 が選択された状態での Graph Explorer のバッチクエリのスクリーンショット](./images/graph-explore3.png)

次に、バージョン選択ドロップダウンを使用して`beta`エンドポイントに変更し、まったく同じ要求を行います。

![グラフ-4](./images/graph-explore4.png)

返される結果の違いは何ですか。 いくつかの相違点を特定するには、他のクエリを試してみてください。

`/v1.0`および`/beta`エンドポイントからの応答コンテンツに加えて、アクセス許可が付与されていないバッチ要求が行われた場合のエラーについて理解することが重要です。 たとえば、次に示すのは、OneNote ノートブックを作成するためのバッチ要求アイテムです。

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

ただし、OneNote ノートブックを作成するためのアクセス許可が付与されていない場合は、次の応答が受信されます。 状態コード`403 (Forbidden)`と、指定された OAuth トークンを示すエラーメッセージには、要求された操作を完了するために必要なスコープが含まれていないことに注意してください。

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

バッチ内の各要求は、状態コードと結果またはエラー情報を返します。 各応答を処理して、個々のバッチ操作の成功または失敗を判断する必要があります。