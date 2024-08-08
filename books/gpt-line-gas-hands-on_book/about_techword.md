---
title: "今回登場する主な技術について"
---

## OpenAI API(ChatGPT API)
ChatGPTの開発元はOpenAIという企業が運営しています。(半年ほど前にMicrosoftに買収されましたが)
一時期CEOであるサム・アルトマン氏が解任するという出来事もありましたが、今はCEOに復帰してマイクロソフト傘下で生成AIの開発に携わっています。

https://wired.jp/article/microsoft-emerges-as-the-winner-in-openai-chaos/

https://xtech.nikkei.com/atcl/nxt/column/18/00257/00037/

ChatGPTはあくまでOpenAIが開発したAIサービスの名称です。
そのため、OpenAIが開発した各種生成AIに関するAPIを総称して**OpenAI API**と呼んでいます。

OpenAIは様々なAPIを提供しています。
以下はその一例です。

- [チャット機能](https://platform.openai.com/docs/guides/chat-completions)
- [画像生成機能](https://platform.openai.com/docs/guides/images/usage)
- [テキスト->音声変換機能](https://platform.openai.com/docs/guides/text-to-speech)
- [音声->テキスト変換機能](https://platform.openai.com/docs/guides/speech-to-text)

この中でも私が使用したことがあるのは**チャット機能**と**画像生成機能**になります。

https://qiita.com/Keichan_15/items/a4facca87d178f356397

https://qiita.com/Keichan_15/items/9a2b7f6192704a122df3

特に画像生成機能は使用して非常に画期的な機能だと思いました。
商用として利用する場合、権利がどこに帰属するのかがよく分かっていませんが、誰でも自分の希望のままに画像を生成できるとは……凄い社会になりました。

今回は前回の勉強会に引き続き、**チャット機能**を使用して開発を行っていきます。

## Google App Script(GAS)

https://workspace.google.com/intl/ja/products/apps-script/

**Google App Script**(以下GAS)はGoogle社が開発したJavaScriptベースのスクリプトプラットフォームです。

普通のJavaScriptと何が違うんだ・・？と疑問を持たれる方もいらっしゃることでしょう。
いくつか特徴はありますが、今回は何点かに絞ってご紹介します。

### ①各種Google提供サービスとの連携
まずは何といっても**Googleが提供している各種サービスとの連携が可能である**という点です。

例えば[Googleスプレッドシート](https://workspace.google.com/intl/ja/products/sheets/)と連携を行うと、
スプレッドシート内の特定のシートやセルに対して自動で任意の操作を行うことができます。([参考](https://ex-ture.com/blog/2022/12/21/google-app-script%E3%81%A8google%E3%82%B9%E3%83%97%E3%83%AC%E3%83%83%E3%83%89%E3%82%B7%E3%83%BC%E3%83%88%E3%82%92%E9%80%A3%E6%90%BA%E3%81%95%E3%81%9B%E3%82%8B/))

またGmailなどと連携をすれば、自動でユーザーに対して定型文を含めたメールを送信するといったことも実現できます。([参考](https://note.com/su3_hokkaido/n/n6213a6dec475))

先述の通り、GASはGoogleが開発したスクリプトプラットフォームなので、各種Googleサービスと連携ができるのは納得できますね。
では逆にGoogle以外の外部サービスとは連携できるのでしょうか・・？

結論、**できます！**

### ②外部サービスとも連携可能
外部サービスって例えば何があるんだろう……となったときに、皆さんであれば最初に思いつくのはMicrosoft Teamsではないでしょうか。

Microsoft関連のサービスであればPower Automateが真っ先に思いつくところではあるのですが、勿論GASはMicrosoft Teamsとも連携可能です。
それ以外にもSlackやX、Salesforceといった様々な外部サービスとも連携ができます。

Slackとの連携は私もいくつかやったことがありますが、意外と仕組みは簡単で実装が大変・・ということはありませんでした。
皆さんの環境でSlackを導入されているところがあれば、簡単なツールとして含めてみるのも良いかもしれませんね。

https://qiita.com/Keichan_15/items/355ce2bf271bba4fe0eb

https://qiita.com/Keichan_15/items/a4facca87d178f356397

実は今回の勉強会で取り扱うChatGPTやLINEも、**GAS側からみると外部サービス**になります。
GASは様々なサービスと連携し、自動化を行うツールとして非常に優れていると言えますね。

### ③デプロイをGAS側が管理してくれる
個人的にはこの③が一番メリットなのかなと感じています(笑)

まずデプロイについて簡単に説明します。
デプロイとは、**作成したサービスを実際に他の一般ユーザーが使用できるように公開すること**です。

これはいらすとやさんの絵をお借りして作成してみました。

![](/images/deploy_introduction.png)

右下のエンジニアの方はあるウェブサイトを作成し、インターネット上に公開したいと考えています。
そこでデプロイをすることでインターネット上に自分が作成したウェブサイトが公開され、左下のユーザーがそのウェブサイトを閲覧することができるのです。

デプロイを行わないと、自身の環境のみでしか使用・閲覧することができません。
基本的に自分の環境のみでしか使用できないツールやアプリケーションというのはあまり考えられないので、基本的にはツールの作成・公開にはこのデプロイが付きまとうことになります。

デプロイを実際に他サービスで行ったことがある方は、このデプロイという操作が如何に**面倒**で**うまくいかない**かを実感されているのかなと思います。
ここからは私がプライベートでは主にWeb領域の内容について触れているので、それらをベースにお話ししていきます。

フロントエンド領域ではReactのフレームワークである[Next.js](https://nextjs.org/)などが有名ですが、Next.jsのデプロイは[Vercel](https://vercel.com/)を使用します。

https://nextjs.org/

https://vercel.com/

Vercelの場合は基本的にNext.jsのアプリケーションを[GitHub](https://github.co.jp/)に配置していれば、VercelはそのGitHubリポジトリを参照してデプロイをしてくれます。割とこれは神だなあと使用して思いました。

https://github.co.jp/

バックエンド領域では[Ruby on Rails](https://rubyonrails.org/)などでしょうか。
小規模のサービスであれば[fly.io](https://fly.io/)といったアプリケーションを解析してDockerfileを生成し、そのDockerfileをもとにデプロイする機能などもありますが、大規模サービスとなると[EC2](https://aws.amazon.com/jp/ec2/)や[ECS](https://aws.amazon.com/jp/ecs/), [RDS](https://aws.amazon.com/jp/rds/)といったサービスを組み合わせる必要があり、AWS様のお力を全面的に借りることになるでしょう。(オンプレの話は一旦スルーします、、)

https://rubyonrails.org/

https://aws.amazon.com/jp/ec2/

https://aws.amazon.com/jp/ecs/

https://aws.amazon.com/jp/rds/

つまり領域によってはこのデプロイまでの手順が非常に面倒で、かつ工数も増えるといった側面があります。

ですが、GASの場合は**ボタンを数回クリックし、必要な情報を少し入力すればデプロイが完了**します。
他のアプリケーションをデプロイした経験がある方は、この単純操作に正直驚かれる方もいるのではないかと思います。

あと、GASは**デプロイしても基本的に金額は発生しません。**
これは嬉しいところですよね。**サーバー管理・維持費がタダ**ということです。自分は基本的にこういったツール系にお金をかけるのはバカバカしいと感じるタチなので、無料という言葉にあやかれるのであればあやかりたい、、そんな怠惰な人間です。

## LINE Messaging API
最後に[LINE Messaging API](https://developers.line.biz/ja/services/messaging-api/)についても触れておきましょう。

第1回の勉強会に参加された方は、APIとはどのようなモノでどのように使用するかをハンズオンで行っていただきました。

https://zenn.dev/keichan_15/books/gpt-api_nodejs_book

OpenAIがChatGPTのAPIを提供してくれているのと同様に、LINEがLINE Bot作成のためのAPIを提供してくれています。
中でもLINEのメッセージ機能にフォーカスしたのが、この**LINE Messaging API**です。

ドキュメントにLINE Messaging APIの仕組みについて解説してくださっているので、こちらを引用させていただきました。([引用元](https://developers.line.biz/ja/docs/messaging-api/overview/#how-messaging-api-works))

> 1. ユーザーがLINE公式アカウントにメッセージを送信します。
> 2. LINEプラットフォームからボットサーバーのWebhook URLにWebhookイベントが送信されます。
> 3. ボットサーバーはWebhookイベントを確認し、LINEプラットフォームを通じてユーザーに応答します。

上記の内、`ボットサーバー`は今回ではGASのことを指します。デプロイを行って継続的なサーバーとして動かしているからですね。
また、見慣れない単語である`Webhook`が出てきました。少しWebhookについても見ていきましょう。

### Webhookとは？
> webhook（ウェブフック）は、web開発でカスタムのコールバックを用いてウェブページやウェブアプリケーションの動作を追加または変更するための方法である。
> (Wikipedia参照)
……？って感じですよね(笑)

Webhookは**リクエストなどの更新情報をリアルタイムで他のアプリケーションに通知する機能**です。
例えば、Microsoft Teamsで相手のチャットにリアクションを送ると、相手から文面で「ありがとう！」というチャットを返す機能をGASで作成していたとしましょう。

GASの場合、Webhookに引っかかるとGASの`doPost(e)`という関数をコールしにいきます。
これは後ほどコードを実装する際にも説明します。

つまり諸々の処理についてはこの`doPost(e)`という関数の中に実装していくことになります。
流れとしては以下です。

①AさんがBさんのチャットにリアクションを送る
②Webhookがリアクションされたことを検知し、GASの`doPost(e)`関数を呼び出す
③`doPost(e)`関数内でBさんがAさんにありがとうと送る処理を実行する
④BさんがAさんにチャットで「ありがとう！」と送る

これもせっかくなので図で理解してみましょう。
今回作成しようとしているBotは以下のような仕組みで動いています。Webhookの理解のついでに見ておきましょう。

![](/images/api_flow.png)

画像内の番号は、以下の番号と紐付いています。

①ユーザーはLINE Botに対して質問をします
②LINE Botは登録されたWebhook URLから質問が来たことを通知します
③WebhookがGASの`doPost(e)`関数を呼び出します
④GASの処理内で、chatGPT APIに質問内容を投げかけます
⑤質問内容に対する回答をchatGPT APIから受け取ります
⑥回答をLINE Botに受け渡します
⑦LINE Botがユーザーのトークに回答を送ります

図を見ると難しいことをやっているように見えるのですが、実際はかなりシンプルなのでご安心ください。
いわばWebhookはLINE BotとGASのボットサーバーとの橋渡しを行ってくれているものと思っていただければここでは大丈夫です。

それでは早速実装を行っていきましょう！