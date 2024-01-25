---
title: "Node.jsで手元ChatGPT環境を作成しよう"
---

## 実装前に

大枠はOpenAIの公式ドキュメントであるクイックスタートの章を参考に実装しています。

今回はあえてドキュメントの記載内容に沿って実装するにあたり、いくつかエラーが発生する為、それらも踏まえつつ実装を進めていきます。

https://platform.openai.com/docs/quickstart?context=node

トライ & エラーの連続ですが、楽しみながらやっていきましょう！

~~余談ですが、```Node.js```の標準入力の最適解がネットのどこを漁っても見当たらなかったので、半ば強引に実装していますごめんなさい。。~~

## プロジェクトの作成
まずは```Node.js```のプロジェクトを新規作成します。

お好きな階層にお好きな名前で空ディレクトリを作成します。
私の場合は```gpt_apitest_node```というディレクトリをCドライブ直下に配置しました。

![](/images/node-1.png)

前章の```Node.js```の導入時に上2つにチェックマークを入れていた場合、エクスプローラのディレクトリ内で以下の操作を実施するとVisual Studio Codeが開きます。

```右クリック > その他のオプションを確認 > Codeで開く```

![](/images/node-2.png)

![](/images/node-3.png)

![](/images/node-4.png)

チェック忘れたよ…って方は通常右クリックから```ターミナルで開く```をクリックします。

![](/images/node-5.png)

PowerShellが開くと思うので、以下のコマンドを入力します。(">"は除いて入力してください)

```> code .```

![](/images/node-6.png)

この方法でもVisual Studio Codeが開きます。

![](/images/node-4.png)

おまけにVisual Studio Code内からターミナルでコマンド実行できるようにしておきましょう。

画面上部の```表示```タブから```ターミナル```をクリックします。

![](/images/node-7.png)

PowerShellのターミナルが画面下部に開きます。現在いるディレクトリに移動された状態で表示されます。

![](/images/node-8.png)

念のため```Node.js```が入っているか確認しておきましょう。
表示したターミナルで以下コマンドを入力します。

```terminal:terminal
> node -v
```

導入した```Node.js```のバージョンが表示されていればOKです！

![](/images/node-9.png)

続いてプロジェクトを作成します。以下コマンドを入力します。

```terminal:terminal
> npm init -y
```

![](/images/node-10.png)

![](/images/node-11.png)

新たに```package.json```という名前のファイルが生成されていればOKです。

次に、モジュール環境でimport文を使用するため、```package.json```を一部編集します。

```diff JSON:package.json
{
  "name": "gpt_apitest_node",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
+ "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

![](/images/node-12.png)

次に今回使用するOpenAIのライブラリをインストールします。
以下のコマンドを入力します。

```terminal:terminal
> npm install --save openai
```

![](/images/node-13.png)

package.jsonを開き、以下のような表示になっていればライブラリのインストールは完了です。

```diff JSON:package.json
{
  "name": "gpt_apitest_node",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
+ "dependencies": {
+   "openai": "^4.25.0"
+ }
}
```

## JavaScriptを書いていく

続いて今回のメインであるJSですね！
新しく```index.js```というファイルを作成しましょう。

![](/images/node-14.png)

早速公式ドキュメントのQuickstartを見てみましょう。

QuickstartのStep3に```Sending your first API request```とのタイトルで実際のサンプルコードが掲載されています。

https://platform.openai.com/docs/quickstart/step-3-sending-your-first-api-request

一旦まずはコピーしたコードの内、```content:```部分を```こんにちは！```に修正して実行してみましょう。

```javascript:index.js
import OpenAI from "openai";

const openai = new OpenAI();

async function main() {
  const completion = await openai.chat.completions.create({
    messages: [{ role: "system", content: "こんにちは！" }],
    model: "gpt-3.5-turbo",
  });

  console.log(completion.choices[0]);
}

main();
```

ターミナルに以下のコマンドを入力し、実行します。

```terminal:terminal
> node index.js
```

![](/images/node-15.png)

するとどうやらエラーが出たみたいです。確認してみましょう。

![](/images/node-16.png)

```
OpenAIError: The OPENAI_API_KEY environment variable is missing or empty; either provide it, or instantiate the OpenAI client with an apiKey option, like new OpenAI({ apiKey: 'My API Key' }).
```

英語に強い方は薄々お気付きかもしれませんが、前章で取得したAPIキーを設定していない為、認証部分で「APIキーが空だよ！」とエラーを吐いています。

では実際に取得したAPIキーを設定してみましょう。以下コード内のダブルクォーテーション内に、取得したAPIキーを貼り付けます。

:::message alert
今回はAPIキーを直接ソースコード内に設定(ハードコーディング)していますが、一般的には```.env```等のファイルで環境変数として設定するのが望ましいです。

Node.jsでは```dotenv```と呼ばれるライブラリで実現できます。

https://www.npmjs.com/package/dotenv

:::

```js:index.js
import OpenAI from "openai";

const openai = new OpenAI({
  // ココを追加！取得したAPIキーの部分を、ご自身で取得したAPIキーに設定してください！
  apiKey: "取得したAPIキー",
});

async function main() {
  const completion = await openai.chat.completions.create({
    messages: [{ role: "system", content: "こんにちは！" }],
    model: "gpt-3.5-turbo",
  });

  console.log(completion.choices[0]);
}

main();
```

追記が完了しましたら、再度以下のコマンドを入力します。

```terminal:terminal
> node index.js
```

![](/images/node-17.png)

ん、よく分からない表記になってますね…。
本来表示させたい部分は```content: 'こんにちは ~~'```の部分だけで良いのですが…。

実は現状のコード内にある以下の記述が悪さをしています。

```js:index.js
console.log(completion.choices[0]);
```

ここで再度APIリファレンスを確認してみます。

https://platform.openai.com/docs/api-reference/chat/create

APIへのリクエストが正常に通った場合、返却されるレスポンスは以下のような内容になると説明しました。

```JSON
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

レスポンスの内、中盤辺りに記載されている箇所のみがごっそり抜き取られて表示されています。

つまり以下のコードでは、**choicesの配列要素[0]番目のみ**を表示しているといった状態になっています。

```js:index.js
console.log(completion.choices[0]);
```

```JSON
{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "\n\nHello there, how may I assist you today?",
    },
    "logprobs": null,
    "finish_reason": "stop"
  }
```

今回表示させたい部分は```content:```の部分だけです。
となると記述はどのように書いてあげると取得できそうでしょうか。

そうです。以下のような感じで書いてあげると良いのです！

```js:index.js
console.log(completion.choices[0].message.content);
```

修正した```index.js```は以下になります。

```js:index.js
import OpenAI from "openai";

const openai = new OpenAI({
  // ココを追加！取得したAPIキーの部分を、ご自身で取得したAPIキーに設定してください！
  apiKey: "取得したAPIキー",
});

async function main() {
  const completion = await openai.chat.completions.create({
    messages: [{ role: "system", content: "こんにちは！" }],
    model: "gpt-3.5-turbo",
  });

  console.log(completion.choices[0].message.content);
}

main();
```

コマンドを実行して動きを確認してみましょう。

画像のような表示になっていればOKです！

```terminal:terminal
> node index.js
```


ただ今の状態では毎度コマンドを実行する度、質問内容は「こんにちは！」が固定の状態です。

質問は自分で考えて送ってこそChatGPTですよね…。

そうです。これを標準入力を使って実現してみましょう！

## 好きな質問を投げれるように修正する

早速**標準入力**を使ってみましょう。
ターミナルから質問を入力して実行(Enterキー)を押すと、質問の下の行に回答を表示させてみます。

以下のコードを```index.js```に実装してください。
(コピペでOKです。APIキーの部分は変更してくださいね。)

```javascript:index.js
import OpenAI from "openai";

// 1.
import readLine from 'readline';

const openai = new OpenAI({
  apiKey: "取得したAPIキー",
});

async function main() {

  // 2.
  var reader = readLine.createInterface({
    //2.1
    input: process.stdin,
    //2.2
    output: process.stdout
  })
  
  // 3.
  var input_string = '';

  // 4. 
  reader.on('line', async (line) => {
    // 4.1
    input_string = line;
    // 4.2
    reader.close();
    
    // 5.
    const completion = await openai.chat.completions.create({
        messages: [{ role: "system", content: input_string}],
        model: "gpt-3.5-turbo",
    });

    // 6.
    console.log(completion.choices[0].message.content);
    
  });

}

main();
```

コードがグッと難しくなりましたね。。
コードの番号と以下の番号が照らし合わせれるように解説を差し込んだので、是非確認して頂けると幸いです。

1. Node.jsのreadlineモジュールをimportします。readlineモジュールはNode.jsにて標準入出力を扱うことができます
2. インターフェースを設定します。今回は読み込みたいストリームを2.1、書き出したいストリームを2.2に設定します。
3. 入力内容を保持する空の変数を定義します。
4. 入力内容を1行ずつ処理しています。今回入力は1行だけなので、入力内容を4.1に格納した時点で処理をCloseしました(4.2)
5. 入力した内容に応じて質問を動的に変更したいため、```content:```に```input_word```を指定することで、入力内容に応じた質問を含めたリクエストを送信できます。
6. 返却されたレスポンスをコンソールに表示します。

余談ですが、Javaとかであれば標準入力は以下のような書き方になります。

```Java
  Scanner sc = new Scanner(System.in);
  String input_word = sc.nextLine();
```

2行で完結してしまうんですよね。。
~~そう考えるとNode.jsの標準入力、実装量多過ぎでしょ……。参考情報も少ないし……~~

実装が完了しましたら、以下コマンドを入力して起動します。

```terminal:terminal
> node index.js
```

以下のようにターミナルがフリーズ状態になっていれば問題ありません。
何か壊れた訳では無く、ユーザーの入力受付を待っている状態になっています。

![](/images/node-19.png)

ターミナルに```こんにちは！```と入力してEnterキーを押してみましょう。

![](/images/node-20.png)

すると少し待機時間を経てから、ターミナルに返信が返ってくることが確認できると思います！

![](/images/node-21.png)

以上で実装は終了です！お疲れ様でした！

## おまけ
ところで実装時にはあまり触れなかったのですが、ChatGPTのAPIはModelが複数提供されています。

公式ドキュメントのModelのページを見てみましょう。

https://platform.openai.com/docs/models

今回扱ったModelは**gpt-3.5-turbo**というモデルです。
以下のページから確認できます。

https://platform.openai.com/docs/models/gpt-3-5

直近ではGPT-4のModelも登場しました。

https://platform.openai.com/docs/models/gpt-4-and-gpt-4-turbo

GPT3.5系と4系の主な違いは大きく以下の2点です。

- いつまでのデータを学習しているかが違う
GPT3.5系は2021年9月までの情報に対して、GPT4系は最新のModelだと2023年4月まで学習しています。
- 料金体系が違う
回答1トークン辺りの値段が変わってきます。以下が料金体系を掲載している公式ページになります。
ザックリですが、GPT4の1トークン辺りの金額は、GPT3.5の15倍程度に相当します。

  https://openai.com/pricing

他にも画像生成のModelであるDALLや音声認識のModelであるWhisperなど、様々なModelが用意されています。

ご自身の学習用途に合わせて使用してみてくださいね。