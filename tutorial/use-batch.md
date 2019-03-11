<!-- markdownlint-disable MD002 MD041 -->

前の手順で作成したフローでは`$batch` 、API を使用して、Microsoft Graph に対する2つの個別の要求を行います。 この方法`$batch`を使用してエンドポイントを呼び出すと、いくつかの利点`$batch`と柔軟性が得られますが、1回`$batch`の呼び出しで Microsoft Graph に複数の要求を実行するときに、エンドポイントの本当の威力を発揮します。 この演習では、統合グループの作成例を拡張し、1つ`$batch`の要求でチームに複数の既定のチャネルを作成するようにチームを関連付けます。

ブラウザーで[Microsoft Flow](https://flow.microsoft.com)を開き、Office 365 テナント管理者アカウントでサインインします。 前の手順で作成したフローを選択し、[**編集**] を選択します。

[**新しい手順**] を`Batch`選択し、検索ボックスに入力します。 [ **MS Graph バッチコネクタ**] アクションを追加します。 省略記号を選択して、この`Batch POST-channels`アクションの名前をに変更します。

アクションの**本文**テキストボックスに次のコードを追加します。

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Marketing Collateral",
        "description": "Marketing collateral and documentation."
      }
    },
    {
      "id": 2,
      "dependsOn": [
        "1"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Vendor Contracts",
        "description": "Vendor documents, contracts, agreements and schedules."
      }
    },
    {
      "id": 3,
      "dependsOn": [
        "2"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "General Client Agreements",
        "description": "General Client documents and agreements."
      }
    }
  ]
}
```

上記の3つの要求は、シーケンスの順序を指定するために[dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property)プロパティを使用していて、それぞれが新しいチームで新しいチャネルを作成するために POST 要求を実行することに注意してください。

`REPLACE`プレースホルダーの各インスタンスを選択し、[動的コンテンツ] ウィンドウで [**式**] を選択します。 次の数式を**式**に追加します。

```js
body('Batch_PUT-team').responses[0].body.id
```

![[動的コンテンツ] ウィンドウ内の式のスクリーンショット](./images/flow-channel1.png)

[**保存**] を選択し、[**テスト**] を選択してフローを実行します。 [トリガーアクションを**実行**する] ラジオボタンを選択し、[ **Save & Test**] を選択します。 [**名前**] フィールドにスペースを入れずに一意のグループ名を入力し、[**実行フロー** ] を選択してフローを実行します。

![[実行フロー] ダイアログのスクリーンショット](./images/flow-channel3.png)

フローが開始されたら、[ **flow run アクティビティを参照**] リンクを選択し、実行中のフローを選択してアクティビティログを表示します。

フローが完了すると、 `Batch POST-channels`アクションの最終出力には、作成された各チャネルに対して 201 HTTP 状態応答があります。

![成功したフローアクティビティログのスクリーンショット](./images/flow-channel2.png)

[Microsoft Teams](https://teams.microsoft.com)を参照して、Office 365 テナント管理者アカウントでサインインします。 作成したチームが表示されることと、 `$batch`要求によって作成された3つのチャネルが含まれていることを確認します。

![新しいチームとチャネルが表示されている Teams アプリのスクリーンショット](./images/team-channels.png)

このチュートリアルで`Batch POST-channels`は、この操作は個別のアクションとして実装されていましたが、チャネルを作成する呼び出しは`Batch PUT-team` 、アクションに追加の呼び出しとして追加されている可能性があります。 これにより、1回のバッチ呼び出しでチームとすべてのチャネルが作成されます。 自分で試してみてください。

最後に、 [JSON のバッチ](https://docs.microsoft.com/graph/json-batching)呼び出しは、要求ごとに HTTP 状態コードを返すことに注意してください。 運用プロセスでは、結果の事後処理を[`Apply to each`](https://docs.microsoft.com/flow/apply-to-each)アクションと組み合わせて、個々の応答に201状態コードがあることを検証したり、受信した他の状態コードを補正したりできます。