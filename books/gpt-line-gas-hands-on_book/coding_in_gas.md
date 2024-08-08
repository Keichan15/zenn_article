---
title: "GAS実装"
---

## スクリプトプロパティの設定
以前の勉強会でNode.jsを使用したChatGPT環境を構築しましたが、その際に取得したAPIキーをソースコードに直接記入する方式を採用していました。
ただこの方法はセキュリティ観点から非常によろしくなく、別途環境変数として管理するのが一般的です。

GASにはこの環境変数の仕組みとして**スクリプトプロパティ**があります。

まずはこのスクリプトプロパティに前章で取得したそれぞれのAPIキーを設定しましょう。

まずは左側から歯車マークの設定アイコンをクリックします。

![](/images/image-22.png)

少し下にスクロールすると**スクリプトプロパティ**の項目があるので、
```スクリプト プロパティを追加```をクリックします。

![](/images/image-23.png)

クリックするとこのようにプロパティと値のセットで登録ができるフォームが出現します。

![](/images/image-24.png)

今回はOpenAI APIキーとチャンネルアクセストークンを設定するので、
```スクリプト プロパティを追加```をもう一度クリックして2つ入力できる状態にしておきましょう。

![](/images/image-25.png)

それぞれ以下の条件でトークンを設定します。
- **OPEN_AI_API_KEY**
  - 前章で取得した**OpenAIのAPIキー**
- **LINE_CHANNEL_ACCESS_TOKEN**
  - 前章で取得した**LINE developersのチャンネルアクセストークン**

実際の入力例は以下になります。
問題なければ```スクリプト プロパティを保存```をクリック。

![](/images/image-26.png)

設定が完了した再度コーディング画面に戻り、元々定義されている関数を削除して、
以下のコードをそのまますべてコピーし、貼り付けましょう。

```javascript
const LINE_CHANNEL_ACCESS_TOKEN = PropertiesService.getScriptProperties().getProperty('LINE_CHANNEL_ACCESS_TOKEN');
const OPEN_AI_API_KEY = PropertiesService.getScriptProperties().getProperty('OPEN_AI_API_KEY');

const LINE_ENDPOINT = 'https://api.line.me/v2/bot/message/reply';
const OPENAI_API_URL = 'https://api.openai.com/v1/chat/completions';

function doPost(e) {
  try {
    const json = JSON.parse(e.postData.contents);
    const replyToken = json.events[0].replyToken;
    const userMessage = json.events[0].message.text;

    if (typeof replyToken === 'undefined') {
      throw new Error('undefinded error');
    }

    const replyMessage = getChatGptResponse(userMessage);
    sendLineReply(replyToken, replyMessage);

  } catch (error) {
    Logger.log('Error in doPost: ' + error.message);
  }
}

// OpenAIのChatGPTにメッセージを送信し、応答を取得
function getChatGptResponse(message) {
  const messages = [{'role': 'user', 'content': message}];
  const headers = {
    'Authorization': 'Bearer ' + OPEN_AI_API_KEY,
    'Content-type': 'application/json'
  };
  const options = {
    'muteHttpExceptions': true,
    'headers': headers,
    'method': 'POST',
    'payload': JSON.stringify({
      'model': 'gpt-3.5-turbo',
      'messages': messages
    })
  };

  try {
    const response = UrlFetchApp.fetch(OPENAI_API_URL, options);
    const jsonResponse = JSON.parse(response.getContentText());
    return jsonResponse.choices[0].message.content;
  } catch (error) {
    Logger.log('Error in getChatGptResponse: ' + error.message);
    return 'Sorry, I couldn\'t process your request.';
  }
}

// LINEにメッセージを返信
function sendLineReply(replyToken, message) {
  const payload = {
    'replyToken': replyToken,
    'messages': [{
      'type': 'text',
      'text': message
    }]
  };
  const headers = {
    'Content-Type': 'application/json; charset=UTF-8',
    'Authorization': 'Bearer ' + LINE_CHANNEL_ACCESS_TOKEN
  };
  const options = {
    'method': 'POST',
    'headers': headers,
    'payload': JSON.stringify(payload)
  };

  try {
    UrlFetchApp.fetch(LINE_ENDPOINT, options);
  } catch (error) {
    Logger.log('Error in sendLineReply: ' + error.message);
  }
}
```
今回は処理が冗長である(2つのAPIにリクエストを投げる)関係上、関数を定義して処理を分割しています。
順にみていきましょう。

```javascript
const LINE_CHANNEL_ACCESS_TOKEN = PropertiesService.getScriptProperties().getProperty('LINE_CHANNEL_ACCESS_TOKEN');
const OPEN_AI_API_KEY = PropertiesService.getScriptProperties().getProperty('OPEN_AI_API_KEY');

const LINE_ENDPOINT = 'https://api.line.me/v2/bot/message/reply';
const OPENAI_API_URL = 'https://api.openai.com/v1/chat/completions';
```
ここで各種変数、エンドポイント等のURL情報を設定しています。

```PropertiesService.getScriptProperties().getProperty()```の記述で、先ほど設定したスクリプトプロパティから値を取得することができます。
末尾の```getProperty()```のカッコ内に、スクリプトプロパティのプロパティ名を入力することで値を取得できます。

https://developers.google.com/apps-script/guides/properties?hl=ja

取得した値は左側の変数に格納されるといった仕組みですね。

```javascript
const LINE_ENDPOINT = 'https://api.line.me/v2/bot/message/reply';
const OPENAI_API_URL = 'https://api.openai.com/v1/chat/completions';
```

続いて上記の2つはそれぞれのAPIにリクエストを投げる際のURLを変数に格納しています。

今回はLINEBotへChatGPTから受け取ったメッセージを送るためのエンドポイント```POST https://api.line.me/v2/bot/message/reply```、
ChatGPTにユーザーが入力した質問を投げるためのエンドポイント```POST https://api.openai.com/v1/chat/completions```を定義します。

https://developers.line.biz/ja/reference/messaging-api/#send-reply-message

https://platform.openai.com/docs/api-reference/chat/create


```javascript
function doPost(e) {
  try {
    const json = JSON.parse(e.postData.contents);
    const replyToken = json.events[0].replyToken;
    const userMessage = json.events[0].message.text;

    if (typeof replyToken === 'undefined') {
      throw new Error('undefinded error');
    }

    const replyMessage = getChatGptResponse(userMessage);
    sendLineReply(replyToken, replyMessage);

  } catch (error) {
    Logger.log('Error in doPost: ' + error.message);
  }
}
```

続いて```doPost(e)```関数についてみていきましょう。

```doPost(e)```は先述の通り、Webhook側が検知をすると呼び出す関数になります。
つまり処理の起点はここから始まるということですね。

引数の```e```の中身は[こちら](https://developers.google.com/apps-script/guides/web?hl=ja#request_parameters)で定義されており、

https://developers.google.com/apps-script/guides/web?hl=ja#request_parameters

```javascript
    const json = JSON.parse(e.postData.contents);
    const replyToken = json.events[0].replyToken;
    const userMessage = json.events[0].message.text;
```

```e```の中身からメッセージ送信に必要な```replyToken```とユーザーが実際に入力したメッセージである```message.text```を取得します。
リクエストの例は以下です。LINE developersのAPIリファレンスにも書いています。

```json
curl -v -X POST https://api.line.me/v2/bot/message/reply \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {channel access token}' \
-d '{
    "replyToken":"nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
    "messages":[
        {
            "type":"text",
            "text":"Hello, user"
        },
        {
            "type":"text",
            "text":"May I help you?"
        }
    ]
}'
```

次を見ていきましょう。

```javascript
    if (typeof replyToken === 'undefined') {
      throw new Error('undefinded error');
    }
```

> 応答メッセージを送るには、Webhookイベントオブジェクトに含まれる応答トークンが必要です。
とあるように、応答トークンの発行ができなければメッセージが送信できません。

よって何らかの問題で発行できなかった場合はこの時点でエラーを吐かせるようにしています。

```javascript
const replyMessage = getChatGptResponse(userMessage);
```

```getChatGptResponse()```というオリジナル関数を呼び出し、その処理結果を```replyMessage```の変数に格納しています。
引数にはユーザーがLINEで入力した```userMessage```を設定しています。

```javascript
function getChatGptResponse(message) {
  const messages = [{'role': 'user', 'content': message}];
  const headers = {
    'Authorization': 'Bearer ' + OPEN_AI_API_KEY,
    'Content-type': 'application/json'
  };
  const options = {
    'muteHttpExceptions': true,
    'headers': headers,
    'method': 'POST',
    'payload': JSON.stringify({
      'model': 'gpt-3.5-turbo',
      'messages': messages
    })
  };

  try {
    const response = UrlFetchApp.fetch(OPENAI_API_URL, options);
    const jsonResponse = JSON.parse(response.getContentText());
    return jsonResponse.choices[0].message.content;
  } catch (error) {
    Logger.log('Error in getChatGptResponse: ' + error.message);
    return 'Sorry, I couldn\'t process your request.';
  }
}
```

この辺りの処理は第1回の勉強会資料が参考になります。

詳細説明は以下の資料を参考いただければと思いますが、ざっくり行っていることは以下です。

https://zenn.dev/keichan_15/books/gpt-api_nodejs_book/viewer/nodejs_coding#javascript%E3%82%92%E6%9B%B8%E3%81%84%E3%81%A6%E3%81%84%E3%81%8F

①LINEに入力したメッセージをもとにOpenAI APIへのリクエストを作成
②OpenAI側からレスポンスを受け取る。
③レスポンスから回答部分を抽出し、変数に格納する

コード自体は難しそうに見えるのですが、やってることは案外シンプルです。

またここで重要になるのが```UrlFetchApp```です。
実はGASではGASからHTTPリクエストを送るための関数が定義されています。便利ですよね。

https://developers.google.com/apps-script/reference/url-fetch/url-fetch-app?hl=ja

```javascript
function sendLineReply(replyToken, message) {
  const payload = {
    'replyToken': replyToken,
    'messages': [{
      'type': 'text',
      'text': message
    }]
  };
  const headers = {
    'Content-Type': 'application/json; charset=UTF-8',
    'Authorization': 'Bearer ' + LINE_CHANNEL_ACCESS_TOKEN
  };
  const options = {
    'method': 'POST',
    'headers': headers,
    'payload': JSON.stringify(payload)
  };

  try {
    UrlFetchApp.fetch(LINE_ENDPOINT, options);
  } catch (error) {
    Logger.log('Error in sendLineReply: ' + error.message);
  }
}
```

最後に取得した回答をLINEへ送信するための関数です。

これもほぼOpenAI APIへのリクエスト時と同じですね。
APIの叩き方は種類は違えど原則は同じなので、1つのAPIを叩けるようになれば他のAPIも自然と叩けるようになってきます。

これで実装が完了しました！