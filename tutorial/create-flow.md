<!-- markdownlint-disable MD002 MD041 -->

この演習では、前の手順で作成したカスタムコネクタを使用して Microsoft teams を作成して構成するフローを作成します。 このフローでは、カスタムコネクタを使用して、Office 365 統合グループを作成するために POST 要求を送信します。グループの作成が完了するまで待機し、その後、PUT 要求を送信して、グループを Microsoft チームに関連付けます。

最終的に、フローは次のようになります。

![完了したフローのスクリーンショット](./images/flow-team1.png)

ブラウザーで[Microsoft Flow](https://flow.microsoft.com)を開き、Office 365 テナント管理者アカウントでサインインします。 左側のナビゲーションで [**マイフロー** ] を選択します。 [**新規**作成] を選択し、[新規**作成**] を選択します。 [**新規から作成**] を選択します。 検索`Manual`ボックスにを入力し、**手動でフロートリガーをトリガー**します。

[**入力を追加**] を選択して`Name` 、[**テキスト**] を選択し、タイトルとしてを入力します。

![フロートリガーを手動でトリガーするスクリーンショット](./images/flow-team6.png)

[**新しい手順**] を`Batch`選択し、検索ボックスに入力します。 [ **MS Graph バッチコネクタ**] アクションを追加します。 省略記号を選択して、この`Batch POST-groups`アクションの名前をに変更します。

アクションの**本文**テキストボックスに次のコードを追加します。

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

[**動的コンテンツの追加**] `Name`メニューから手動トリガーの値を選択して、各`REPLACE`プレースホルダーを置き換えます。

![Microsoft Flow の [動的コンテンツ] メニューのスクリーンショット](./images/flow-team2.png)

[**新しい手順**] を選択`delay`し、**遅延**アクションを検索して追加して、1分間構成します。

[**新しい手順**] を`Batch`選択し、検索ボックスに入力します。 [ **MS Graph バッチコネクタ**] アクションを追加します。 省略記号を選択して、この`Batch PUT-team`アクションの名前をに変更します。

アクションの**本文**テキストボックスに次のコードを追加します。

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

`REPLACE`プレースホルダーを選択し、[動的コンテンツ] ウィンドウで [**式**] を選択します。 次の数式を**式**に追加します。

```js
body('Batch_POST-groups').responses[0].body.id
```

![[動的コンテンツ] ウィンドウ内の式のスクリーンショット](./images/flow-formula.png)

この式では、最初のアクションの結果からグループ ID を使用することを指定します。

![更新されたアクション本文のスクリーンショット](./images/flow-team3.png)

[**保存**] を選択してからフローを選択し、[**テスト**] を選択してフローを実行します。

> [!TIP]
> このような`The template validation failed: 'The action(s) 'Batch_POST-groups' referenced by 'inputs' in action 'Batch_2' are not defined in the template'`エラーが表示される場合は、式が正しくないため、検索できないフローアクションが参照されている可能性があります。 参照しているアクション名が正確に一致することを確認します。

[トリガーアクションを**実行する**] ラジオボタンを選択し、[ **Save & Test**] を選択します。 ダイアログの [**続行**] を選択します。 スペースを含まない名前を指定し、[**実行フロー** ] を選択してチームを作成します。

![[実行フロー] ダイアログのスクリーンショット](./images/flow-team4.png)

最後に、[ **flow run アクティビティを参照して**ください] リンクを選択し、実行中のフローを選択してアクティビティログを表示します。

> [!NOTE]
> フローの実行を表示するには、[実行履歴] の一覧で実行中のフローインスタンスをクリックする必要がある場合があります。

フローが完了すると、Office 365 グループとチームが構成されました。 バッチアクションアイテムを選択して、JSON バッチ呼び出しの結果を表示します。 アクションの状態コードは、 `outputs`次の図のようなチームの関連付けを成功させるために201の状態コードである必要があります。 `Batch PUT-team`

![成功したフローアクティビティログのスクリーンショット](./images/flow-team5.png)