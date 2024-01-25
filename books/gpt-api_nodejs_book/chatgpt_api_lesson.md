---
title: "ChatGPT-APIに触れてみる"
---

## OpenAI アカウント作成
さて準備が整ったところで、早速ChatGPT-APIを触っていきましょう。
まずAPIに触れるにはOpenAIのアカウント作成が必要になります。

OpenAIの[公式サイト](https://openai.com/)にアクセスしましょう。

https://openai.com/


![](/images/gpt-1.png)

画面右上の```Log in```ボタンをクリックします。
すると```Welcome back```と表示されたログイン画面が表示されます。

![](/images/gpt-2.png)

画面中央部の```サインアップ```のリンクをクリックします。

![](/images/gpt-3.png)

```Create your account```と表示されている画面に遷移したことを確認後、中央部のメールアドレス入力欄にご自身の好きなメールアドレスを入力してください。

![](/images/gpt-4.png)

次にパスワードを入力します。
長さ12文字以上が少ししんどいですが。。

入力内容に誤りが無ければ、```続ける```ボタンをクリックします。

![](/images/gpt-5.png)

![](/images/gpt-6.png)

完了後、登録したメールアドレス宛に認証メールが届いています。

中央部の```Verify email address```ボタンをクリックします。

![](/images/gpt-7.png)

次にあなたの情報を教えてくれ～とせがまれます。
必要に応じて入力してください。

生年月日の入力が特殊で、```日/月/年```の順番に入力する必要があります。
例えば2001/1/5生であれば、```05/01/2001```となります。慣れないなあこの書き方。。

![](/images/gpt-8.png)

入力が完了し、以下の画面が表示されていればアカウント作成は完了です！
お疲れ様でした！

![](/images/gpt-9.png)

## APIを叩いてみよう！
今回のゴールは自身のコンソールから質問を投げかけて、コンソールにその返答を表示する、といったものとなります。

まずはアカウントを作成することで取得できるAPIキーを使用して、Visual Studio Codeの拡張機能からAPIを叩いてみましょう！

### APIキーの発行

先ほどの画面より、```API```ボタンをクリックします。

![](/images/gpt-10.png)

左側の歯車マークを押下します。

![](/images/gpt-11.png)

一覧の中から```API Keys```を選択します。

![](/images/gpt-12.png)

電話番号の認証を行います。
出た当初は必要なかったんですが、、悪用する人が増えたのが原因かもですね。。

![](/images/gpt-13.png)

SMSで認証番号が送信されるので、番号を入力します。
入力する箇所を撮り忘れていましたすみません。。。

![](/images/gpt-14.png)

電話番号認証が完了すると、APIキーを発行できるようになります。
```Create new secret key```を押下します。

![](/images/gpt-15.png)

今回は```testKey```という名前で作成しました。
名前は基本的にどの命名でも問題ありません。

![](/images/gpt-16.png)

APIキーが作成されます。

![](/images/gpt-17.png)

右側のクリップボードアイコンをクリックします。
この際、**コピーしたAPIキーはどこかに必ずメモしておいてください！**

:::message alert
**この画面を消すとAPIキーは再確認出来ません！**
**必ずメモしたことを確認してください！**
:::

![](/images/gpt-18.png)

新しいAPIキーが追加されていることを確認します。

![](/images/gpt-19.png)

### Thunder ClientでAPIを叩いてみる
APIキーが発行できたところで、Thunder Clientを使ってAPIを実際に叩いてみましょう！

まずは該当箇所のAPIリファレンスを確認します。

https://platform.openai.com/docs/api-reference/chat/create

今回はChatGPTにメッセージ付でリクエストを送ると、メッセージに沿った回答を返却してくれるChat機能を使用します。

このリファレンスでは、該当URLにリクエストを投げると、どのようなレスポンス(データ)を返却してくれるかが記載されています。

リファレンスにあるCurlコマンドを例とすると、以下が投げるリクエストになり、、
v
```terminal
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ]
  }'
```

投げたリクエストに対して返却されるデータは以下になります。

```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "model": "gpt-3.5-turbo-0613",
  "system_fingerprint": "fp_44709d6fcb",
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "\n\nHello there, how may I assist you today?",
    },
    "logprobs": null,
    "finish_reason": "stop"
  }],
  "usage": {
    "prompt_tokens": 9,
    "completion_tokens": 12,
    "total_tokens": 21
  }
}
```

カンの良いエンジニアの皆さんですと、上記のレスポンスのどの部分がChatGPTによる回答部分になるか分かっちゃいましたかね。。？

このCurlコマンドを入力して確認するのも良いのですが、せっかくVisual Studio Codeを入れたのであれば、Thunder Clientを使って確認してみたいですよね。。

ということで早速Thunder Clientを使ってみましょう！

まずは前章で導入したVisual Studio Codeを開き、Thunder Clientのアイコンをクリックします。

![](/images/gpt-20.png)

```New Request```をクリックします。
クリック後、以下のような画面が表示されます。

![](/images/gpt-21.png)

まず、URLの左側にあるプルダウンを```GET```から```POST```に変更しましょう。

次にURL入力部分に以下のURLを貼り付けます。

```
https://api.openai.com/v1/chat/completions
```
更にURLの下のタブから```Headers```を選択し、以下のように入力します。

```Content-Type``` / ```application/json```
```Authorization``` / ```Bearer 前章で取得したAPIキー```

以下の画像が入力例となります。

![](/images/gpt-22.png)

次に同タブから```Body```を選択し、更にその中のタブから```JSON```を選択します。
JSON Contentと記載のフォームが表示されたら、以下のコードをそのフォームにそのまま貼り付けましょう。

```JSON
{
    "model": "gpt-3.5-turbo",
    "messages": [
      {
        "role": "system",
        "content": "こんにちは"
      }
    ]
  }
```

以下の画像が入力例となります。

![](/images/gpt-23.png)

入力が完了したら、URLの右に表示されている```Send```ボタンをクリックします。
クリック後、Statusが```200 OK``` と表示されており、```Response```タブ内に以下の画像のようなレスポンスが表示されていればOKです！

![](/images/gpt-24.png)

ここで抑えて頂きたい所としては2つあります。

先ほどのリクエストとレスポンスの関係性を思い出してみましょう。

まず以下がリクエストになります。

```JSON
{
    "model": "gpt-3.5-turbo",
    "messages": [
      {
        "role": "system",
        "content": "こんにちは"
      }
    ]
  }
```

そして以下がレスポンスです。

```JSON
{
  "id": "chatcmpl-8kBbriUacx6HCSmdkda0YK2o90Vic",
  "object": "chat.completion",
  "created": 1706018407,
  "model": "gpt-3.5-turbo-0613",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "こんにちは！どのようなご用件でしょうか？"
      },
      "logprobs": null,
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 8,
    "completion_tokens": 17,
    "total_tokens": 25
  },
  "system_fingerprint": null
}
```

それぞれ```content```と書かれている部分を分かりやすく日本語で設定しました。

1. リクエスト側の```content```に記載されている内容が、**ChatGPTに対して質問したい内容**になります。

2. レスポンス側の```content```は、**リクエスト側の```content```の内容を取得**し、**それに沿った回答を出力**しています。

ここまで分かれば後は非常にシンプルで、それぞれ以下のように設定してあげることで自分で比較的自由自在に質問を投げることができるようになります！

- リクエスト側の```content```は**ユーザーが入力した文字列**を設定する
- レスポンス側の```content```を取得すれば、リクエストで送信した文字列に沿った回答を取得できる

そうです、上記の仕組みを最後に**Node.jsで実現してみよう**というのが今回の本題になります！
繋がってきましたかね？これが伏線ってヤツですヨ。。

尚ChatGPTのAPIは他にも様々なサービスが用意されています。
お時間のある際にリファレンスを一通り読み込んで頂くと、新たな発見があるかもしれません！

それでは最後にNode.jsを使用して、オリジナルのリクエストを送ってみましょう！